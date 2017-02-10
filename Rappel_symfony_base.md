

Dans Symfony, les fonctions générant une page sont les méthodes d'une Classe Contrôleur et on appelle ces méthodes des actions.
La classe est un regroupement de page par catégorie.

Un contrôleur est crée dans un Bundle (ex : AppBundle) dans un dossier Controller et suffixée par Controller.<br>
En général il hérite de Symfony\Bundle\FrameworkBundle\Controller\Controller.
 
` Voir Generate_controller.md`
 
 
 Changer langue
 ---
 Dans App/config/config.yml, changer locale:en et dé-commenter la seconde ligne
 
    parameters:
        locale: fr
        
        translator:      { fallbacks: ["%locale%"] }
 
 
 Vider le cache
 ---
 
    cache:clear (de base affecte le mode dev)
    cache:clear --env=prod
    
Bundle
---

Un bundle est un ensemble de code ré-utilisable dans un autre projet Symfony.
On crée rarement des bundles

    C:\Users\prepavenir\PhpstormProjects\Formation_Git_2017_01\AddressBookSymfony>php bin/console generate:bundle
    
    
      Welcome to the Symfony bundle generator!
    
    
    Are you planning on sharing this bundle across multiple applications? [no]: yes
    
    Your application code must be written in bundles. This command helps
    you generate them easily.
    
    Each bundle is hosted under a namespace (like Acme/BlogBundle).
    The namespace should begin with a "vendor" name like your company name, your
    project name, or your client name, followed by one or more optional category
    sub-namespaces, and it should end with the bundle name itself
    (which must have Bundle as a suffix).
    
    See http://symfony.com/doc/current/cookbook/bundles/best_practices.html#bundle-name for more
    details on bundle naming conventions.
    
    Use / instead of \  for the namespace delimiter to avoid any problem.
    
    Bundle namespace: Prepavenir/BootstrapBundle
    
    In your code, a bundle is often referenced by its name. It can be the
    concatenation of all namespace parts but it's really up to you to come
    up with a unique name (a good practice is to start with the vendor name).
    Based on the namespace, we suggest PrepavenirBootstrapBundle.
    
    Bundle name [PrepavenirBootstrapBundle]:
    
    Bundles are usually generated into the src/ directory. Unless you're
    doing something custom, hit enter to keep this default!
    
    Target Directory [src/]:
    
    What format do you want to use for your generated configuration?
    
    Configuration format (annotation, yml, xml, php) [xml]: annotation
    
    
      Bundle generation
    
    
    > Generating a sample bundle skeleton into C:\Users\prepavenir\PhpstormProjects\Formation_Git_2017_01\AddressBookSymfony\app/../src/Prepavenir/BootstrapBundle
      created .\app/../src/Prepavenir/BootstrapBundle/
      created .\app/../src/Prepavenir/BootstrapBundle/PrepavenirBootstrapBundle.php
      created .\app/../src/Prepavenir/BootstrapBundle/DependencyInjection/
      created .\app/../src/Prepavenir/BootstrapBundle/DependencyInjection/PrepavenirBootstrapExtension.php
      created .\app/../src/Prepavenir/BootstrapBundle/DependencyInjection/Configuration.php
      created .\app/../src/Prepavenir/BootstrapBundle/Controller/
      created .\app/../src/Prepavenir/BootstrapBundle/Controller/DefaultController.php
      created .\app/../src/Prepavenir/BootstrapBundle/Tests/Controller/
      created .\app/../src/Prepavenir/BootstrapBundle/Tests/Controller/DefaultControllerTest.php
      created .\app/../src/Prepavenir/BootstrapBundle/Resources/views/Default/
      created .\app/../src/Prepavenir/BootstrapBundle/Resources/views/Default/index.html.twig
      created .\app/../src/Prepavenir/BootstrapBundle/Resources/config/
      created .\app/../src/Prepavenir/BootstrapBundle/Resources/config/services.yml
    > Checking that the bundle is autoloaded
    > Enabling the bundle inside C:\Users\prepavenir\PhpstormProjects\Formation_Git_2017_01\AddressBookSymfony\app\AppKernel.php
      updated .\app\AppKernel.php
    > Importing the bundle's routes from the C:\Users\prepavenir\PhpstormProjects\Formation_Git_2017_01\AddressBookSymfony\app\config\routing.yml file
      updated .\app/config/routing.yml
    
    
      Everything is OK! Now get to work :).


