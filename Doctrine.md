

Docu Doctrine : http://docs.doctrine-project.org/projects/doctrine-orm/en/latest/

Pour voir les commandes doctrine :

    >php bin/console

Affiche les commandes console, y compris les commandes doctrine

    doctrine
      doctrine:cache:clear-collection-region  Clear a second-level cache collection region.
      doctrine:cache:clear-entity-region      Clear a second-level cache entity region.
      doctrine:cache:clear-metadata           Clears all metadata cache for an entity manager
      doctrine:cache:clear-query              Clears all query cache for an entity manager
      doctrine:cache:clear-query-region       Clear a second-level cache query region.
      doctrine:cache:clear-result             Clears result cache for an entity manager
      doctrine:database:create                Creates the configured database
      doctrine:database:drop                  Drops the configured database
      doctrine:database:import                Import SQL file(s) directly to Database.
      doctrine:ensure-production-settings     Verify that Doctrine is properly configured for a production environment.
      doctrine:generate:crud                  [generate:doctrine:crud] Generates a CRUD based on a Doctrine entity
      doctrine:generate:entities              [generate:doctrine:entities] Generates entity classes and method stubs from your mapping information
      doctrine:generate:entity                [generate:doctrine:entity] Generates a new Doctrine entity inside a bundle
      doctrine:generate:form                  [generate:doctrine:form] Generates a form type class based on a Doctrine entity
      doctrine:mapping:convert                [orm:convert:mapping] Convert mapping information between supported formats.
      doctrine:mapping:import                 Imports mapping information from an existing database
      doctrine:mapping:info
      doctrine:query:dql                      Executes arbitrary DQL directly from the command line.
      doctrine:query:sql                      Executes arbitrary SQL directly from the command line.
      doctrine:schema:create                  Executes (or dumps) the SQL needed to generate the database schema
      doctrine:schema:drop                    Executes (or dumps) the SQL needed to drop the current database schema
      doctrine:schema:update                  Executes (or dumps) the SQL needed to update the database schema to match the current mapping metadata.
      doctrine:schema:validate                Validate the mapping files.


Générer une entité
---

Pour générer une entité, il faut d'abord générer une base de données.

    >php bin/console doctrine:database:create
    Created database `adressbook` for connection named default
La base ici prend le nom renseigné à la création du controller.

Exemple de génération d'entity :

    C:\Users\prepavenir\PhpstormProjects\Formation_Git_2017_01\AddressBookSymfony>php bin/console doctrine:generate:entity
    
    
      Welcome to the Doctrine2 entity generator
    
    
    
    This command helps you generate Doctrine2 entities.
    
    First, you need to give the entity name you want to generate.
    You must use the shortcut notation like AcmeBlogBundle:Post.
    
    The Entity shortcut name: AppBundle:Contact
    
    Determine the format to use for the mapping information.
    
    Configuration format (yml, xml, php, or annotation) [annotation]:
    
    Instead of starting with a blank entity, you can add some fields now.
    Note that the primary key will be added automatically (named id).
    
    Available types: array, simple_array, json_array, object,
    boolean, integer, smallint, bigint, string, text, datetime, datetimetz,
    date, time, decimal, float, binary, blob, guid.
    
    New field name (press <return> to stop adding fields): prenom
    Field type [string]:
    Field length [255]: 40
    Is nullable [false]:
    Unique [false]:
    
    New field name (press <return> to stop adding fields): nom
    Field type [string]:
    Field length [255]: 40
    Is nullable [false]:
    Unique [false]:
    
    New field name (press <return> to stop adding fields):
    
    
      Entity generation
    
    
      created .\src\AppBundle/Entity/
      created .\src\AppBundle/Entity/Contact.php
    > Generating entity class C:\Users\prepavenir\PhpstormProjects\Formation_Git_2017_01\AddressBookSymfony\src\AppBundle\Entity\Contact.php: OK!
    > Generating repository class C:\Users\prepavenir\PhpstormProjects\Formation_Git_2017_01\AddressBookSymfony\src\AppBundle\Repository\ContactRepository.php: OK!
    
    
      Everything is OK! Now get to work :).



Générer la table :

    C:\Users\prepavenir\PhpstormProjects\Formation_Git_2017_01\AddressBookSymfony>php bin/console doctrine:schema:update --dump-sql
    CREATE TABLE contact (id INT AUTO_INCREMENT NOT NULL, prenom VARCHAR(40) NOT NULL, nom VARCHAR(40) NOT NULL, PRIMARY KEY(id)) DEFAULT CHARACTER SET utf8 COLLATE utf8_unicode_ci ENGINE = InnoDB;
Afficher la requête qui va être exécuter.

    C:\Users\prepavenir\PhpstormProjects\Formation_Git_2017_01\AddressBookSymfony>php bin/console doctrine:schema:update --force
    Updating database schema...
    Database schema updated successfully! "1" query was executed


Chaque document Entity contient une classe dont les attributs sont reliés par des annotation aux champs de la base de données.

    class Contact
    {
        /**
         * @var int
         *
         * @ORM\Column(name="id", type="integer")
         * @ORM\Id
         * @ORM\GeneratedValue(strategy="AUTO")
         */
        protected $id;
    
        /**
         * @var string
         *
         * @ORM\Column(name="prenom", type="string", length=40)
         */
        protected $prenom;
     }

Dans Doctrine il y a deux grandes classes; repository (lecture) entitymanager (écriture)

Pour récupérer des données, on utilise donc repository :

    $repo = $this->getDoctrine()->getRepository('AppBundle:Contact');
    $contacts = $repo->findAll();
    
On renvoit la variable $contacts depuis le controller (ici ContactController) vers la vue (views/Contact/list.html.twig)par l'intermédiaire de la fonction render

    return $this->render('AppBundle:Contact:list.html.twig', array(
                'contacts' => $contacts
            ));