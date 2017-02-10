https://github.com/nelmio/alice -> necessite PHP 7
https://github.com/hautelook/AliceBundle/tree/1.x -> ancienne version, marche avec PHP 5.6

Syntaxe : https://github.com/fzaninotto/Faker#fakerproviderlorem

Dans AppBundle, créer un repertoire DataFixtures et un sous-répertoire ORM.
Dans ce sous-repertoire, créer un fichier .yml pour chaque table à remplir.

    @ORM/offre.yml
    
    AppBundle\Entity\Offre:
        offre{1..10}:
            titre: <text(60)>
            lieu: <city()>
            date: <dateTimeBetween('-3 days')>
            societe: <company()>
            contrat: <randomElement($array = array ('CDD','CDI','Stage','Freelance'))>
            description: <paragraph()>
            categories: <numberBetween(1, 5)>x @categorie*
<br>
    
    @ORM/categorie.yml
    
    AppBundle\Entity\Categorie:
        categorie1:
            nom: PHP
        categorie2:
            nom: Java
        categorie3:
            nom: Jquery
        categorie4:
            nom: Angular
        categorie5:
            nom: Javascript
        categorie6:
            nom: Android
        categorie7:
            nom: HTML
        categorie8:
            nom: CSS

