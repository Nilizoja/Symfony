Créer un formulaire de A à Z
===

Générer un entityType

        >php bin/console doctrine:generate:form AppBundle:Societe
        (generer un SocieteType dans un dossier form du bundle indiqué)

Méthode dans le controller, mis ici dans l'action add de SocieteController
SocieteType::class renvoie la classe à laquelle se rapporte SocieteType (ici AppBundle/.../Societe)

        public function addAction(Request $request) #class Request de httpFoundation
        {
            $form = $this->createForm(SocieteType::class);
    
            $form->handleRequest($request);
    
            if ($form->isValid()) {
                $societe = $form->getData();
                $em = $this->getDoctrine()->getEntityManager();
    
                $em->persist($societe);
                $em->flush();
    
                return $this->redirectToRoute('app_societe_show', ['id' => $societe->getId()]);
            }
    
            return $this->render('AppBundle:Societe:add.html.twig', array(
                'societeForm' => $form->createView()
            ));
        }
        
La validation peut être gérée dans l'entity, on l'on précise des conditions pour chaque attribut sous forme d'annotations

    use Symfony\Component\Validator\Constraints as Assert;
    
     /**
         * @var string
         *
         * @ORM\Column(name="nom", type="string", length=40)
         * @Assert\NotBlank(message="Le nom est obligatoire")
         * @Assert\Length(min="2",max="40")
     */
        private $nom;

Le twig contiendra la forme du formulaire <br>
form_end génére aussi tous les éléments "oubliés"

        {{ form_start(societeForm, {'attr':{'novalidate': 'novalidate'}}) }}
        {{  form_row(societeForm.nom) }}
        {{ form_row(societeForm.ville) }}
        <div class="row">
            <div class="col-sm-10 col-sm-offset-2">
                <button type="submit" class="btn-primary">
                    Ajouter
                </button>
            </div>
        </div>
        {{ form_end(societeForm) }}
        
Dans chaque entityType, on peut modifier la méthode buildForm pour déterminer les attribut qui apparaîtront ou pas dans le formulaire.

     public function buildForm(FormBuilderInterface $builder, array $options)
        {
            $builder->add('nom')->add('ville')->add('autre_attribut')        ;
        }
        
        
        
Ajouter un champ "choix"
---
https://symfony.com/doc/current/reference/forms/types/choice.html
Passer par un tableau associatif est obligatoire, si l'on passe par un tableau numéroté, les clés apparaîtront en choix (1,2,3 etc...) et pas les valeurs

    ->add('contrat', ChoiceType::class, array(
                    'choices'  => array(
                       'CDI' => 'CDI',
                       'CDD' => 'CDD',
                       'Stage' => 'Stage',
                       'Freelance' => 'Freelance')));
                        
Transmettre des données sans passer par un champ du formulaire
---
On peut créer une fonction avec l'annotation "PrePersist" pour que celle-ci soit exécutée avant le persist() (fonction générant la requête SQL) dans le controller<br>
Pour que cette annotation fonctionne, il faut ajouter HasLifecycleCallbacks()
http://docs.doctrine-project.org/projects/doctrine-orm/en/latest/reference/events.html#lifecycle-callbacks

    /**
     * Offre
     *
     * @ORM\Table(name="offre")
     * @ORM\Entity(repositoryClass="AppBundle\Repository\OffreRepository")
     * @ORM\HasLifecycleCallbacks()
     */
    class Offre
    {
        /**
        * @ORM\PrePersist()
        */
        public function fillDate()
            {
                if (!$this->id){
                    $this->date = new \DateTime();
                }
            }
    }
    
Formulaire de choix affichant le contenu d'une table
---

Après avoir crée un entityType "categorie", et ajouté à l'entité principale (ici 'offre') un attribut "categories"

    /**
     *@ORM\ManyToMany(targetEntity="AppBundle\Entity\Categorie")
     */
    protected $categories = [];
    
On laisse doctrine générer la table intermédiaire.
Dans le buildForm() de offreType, on peut se contenter d'appeller un add sur cet attribut

    ->add('categories')

Ou détailler un entityType form, pour pouvoir choisir les caractéristiques (affichage select ou checkbox).

    ->add('categories', EntityType::class, array(
    
                    'class' => 'AppBundle:Categorie',
    
                    'choice_label' => 'nom',
    
                    'multiple' => true,
                    'expanded' => true
                ))
                
