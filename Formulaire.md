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
        
