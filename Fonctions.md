Fonction de recherche pa mots-clés
---

    public function search($motscles)
        {
            $dql = "SELECT o FROM AppBundle:Offre o 
                    WHERE o.titre LIKE :search 
                    OR o.lieu LIKE :search 
                    OR o.description LIKE :search
                    OR o.contrat LIKE :search";
    
            return $this->_em->createQuery($dql)
                ->setParameter('search', "%$motscles%")
                ->getResult();
        }
le 'o' peut être remplacé par n'importe quel mot, on a ici choisi 'o' pour signifier 'offre'

Cette fonction est appellée dans une action que l'on appelle searchAction

    public function searchAction(Request $request)
        {
            $motscles = $request->get('motscles');
    
            $repo = $this->getDoctrine()->getRepository('AppBundle:Offre');
    
            $offres = $repo->search($motscles);
    
            return $this->render('AppBundle:Offre:search.html.twig', array(
                'offres' => $offres
            ));
        }

L'affichage dans la vue offre:search se fait comme avec n'importe quelle autre requête

    <table class="table table-striped table-hover">
            {% for offre in offres %}
                <tr>
                    <td>{{ offre.titre }}</td>
                    <td>{{ offre.societe }}</td>
                    <td><a href="{{ path('app_offre_search', { 'motscles' : offre.lieu}) }}">{{ offre.lieu }}</a></td>
                    <td>{{ offre.date.format('d/m/Y')}}</td>
                    <td><a href="{{ path('app_offre_search', { 'motscles' : offre.contrat}) }}">{{ offre.contrat}}</a></td>
                    <td>
                        <a href="{{ path('app_offre_show', {'id': offre.id}) }}" class="btn btn-primary btn-xs">Détail</a>
                    </td>
                </tr>
            {% endfor %}
        </table>
        
