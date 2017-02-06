Rappels PHP.
===

Si l'on fait en sorte que les setter renvoie l'objet entier :

    setNom()
    {
        $this->nom = xxx;
        return $this;
    }

On peut enchaîner les setters.

    $objet->setNom(xxx)->setPrenom(yyy)->setAdresse(zzz)...

Chaque setter "devient" l'objet et permet d'appeler le setter suivant.