
Une route (une page) est l'association entre une URL et une fonction.

Adresse standard : addressbook.sf3/list

Adresse mode dev : adressbook.sf3/app_dev.php/list

 
    
Conflit de routes
---

        /**
         * @Route("/contacts/{id}")
         */
        public function showAction($id)
        {
            return $this->render('AppBundle:Contact:show.html.twig', array(
                // ...
            ));
        }
    
        /**
         * @Route("/contacts/ajouter")
         */
        public function addAction()
        {
            return $this->render('AppBundle:Contact:add.html.twig', array(
                // ...
            ));
        }
        
"/ajouter" est interprété comme un /{id} et l'url renvoie donc la fonction showAction.
Pour éviter ça on peut placer l'action ajouter devant l'action shw (la première rencontrée à priorité)
Ou limiter les valeurs possibles de /{id} via regex (expression régulière)

    /**
         * @Route("/contacts/{id}",requirements={"id":"[1-9][0-9]*"})
     */
Cette expression régulière oblige l'id à commencer par un chiffre de 1 à 9, ce chiffre est suivit par *(0 à n) chiffres, chacun allant de 0 à 9

<br>
Lien vers route
On tape le nom du bundle sans Bundle (AppBundle -> app)
le nom du controller sans controller (SocieteController -> societe)
le nom de l'action sans action (showAction -> show)

    app_societe_show
    
    <li><a href="{{ path('app_contact_list') }}">Lister</a></li>


