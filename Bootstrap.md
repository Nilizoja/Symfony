Installer Bootstrap
---

Bootstrap se présente sous la forme d'un fichier compresser contenant 3 dossier : css, js et fonts.<br>
Ces trois dossiers sont à placer dans le dossier web de notre projet Symfony.
Pour les appeler sur une page (ex : la page base.html.twig dans app/ressources/views/default) mettre des balises script dans le body

    <script src="{{ asset('js/jquery-3.1.1.js') }}"></script>
            <script src="{{ asset('js/bootstrap.js') }}"></script>
Pour limiter la taille du body, l'intégrer entre deux balises div de classe contrainer :

    <div class="container">
    {% block body %}{% endblock %}
    </div>
            
Bootstrap propose des classes correspondant à des css.
On peut ajouter plusieurs classes pour ajouter différents effets.

        <table class="table table-striped table-hover">
            <tr>
                <td>Jean Dupont</td>
                <td>
                    <a href="#">Afficher</a>
                </td>
            </tr>
            <tr>
                <td>Eric Martin</td>
                <td>
                    <a href="#">Afficher</a>
                </td>
            </tr>
        </table>
        
Ici la table aura alternativement des lignes blanches et grises (table-striped), et chaque ligne devient plus foncée lorsque le curseur le survol (table-hover)

    <div class="row">
        <div class="col-md-2">
            <b>Prenom : </b>
        </div>
        <div class="col-md-10">
            Jean
        </div>
    </div>
    <div class="row">
            <div class="col-md-2">
                <b>Nom : </b>
            </div>
            <div class="col-md-10">
                Truc
            </div>
        </div>
col-md taille totale : 10, donc la premiere cellule fait 2/10eme de la largeur de la page, la seconde occupe les 8/10ème restant

