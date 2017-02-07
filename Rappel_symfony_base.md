

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