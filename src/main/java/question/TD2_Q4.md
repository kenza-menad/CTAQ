Q: La chaîne de caractères "org.acme" apparaît littéralement dans les deux endroits :

Dans le test, comme valeur attendue dans l'assertion : assertEquals("org.acme", gav.group())
Dans le code, comme valeur codée en dur dans la méthode parse : return new Gav("org.acme")


Q: Parce que le code ne fait aucun vrai traitement sur la chaîne reçue en paramètre — il se contente de renvoyer une valeur fixe qui correspond, par coïncidence, à ce que le test attend. Le test passe donc sans que le comportement réel de la méthode soit validé : si on appelait Gav.parse avec une autre coordonnée (par exemple "org.other:lib-c:3.0.0"), le code renverrait quand même "org.acme", ce qui serait faux. Cela montre qu'il manque encore une vraie logique de découpage de la chaîne d'entrée le code actuel ne fait que satisfaire ce cas particulier, sans généraliser le comportement attendu.