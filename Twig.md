http://twig.sensiolabs.org/doc/2.x/

Syntaxe foreach

    {% for contact in contacts  %}
    {% endfor %}

Syntaxe echo

    {{ var }}

Syntaxe if(isset($var))

    {% if var is defined %}
    {% endif %}

Liens avec méthode GET
(ici on transmet le mot "Marseille" à une fonction de recherche par mots-clés utilisée dans le searchAction de offreContrller)

    http://siteemploi.sf3/app_dev.php/offres/recherche?motscles=Marseille
    
    <a href="{{ path('app_offre_search', { 'motscles' : offre.lieu}) }}">{{ offre.lieu }}</a>

