# Reponse niveau 0


##  1 - Écrivez le schéma relationnel des 4 tables

- categorie ( __id__, libelle)
- plat (__id__, nom, prix, #id_categorie)
- commande (__id__, date_commande, numero_table)
- commande_ligne (__id__, #id_commande, #id_plat, quantite, prix_unitaire)

## 2 - Pourquoi `commande_ligne` contient-elle une colonne `prix_unitaire`, alors que le prix est déjà dans `plat` ? Donnez un exemple concret où les deux valeurs seraient différentes.

- Si Tonton commande un plat de 7000ar alors que son argent est 5000ar : La on utilise le prix_unitaire de commande_ligne
- Si un jour le prix de plat change , le prix des plats sur des commandes deja fait ne change pas

## 3 - Que se passe-t-il pour les lignes d’une commande quand on supprime la commande ? Quelle instruction en est responsable ?

- Les lignes de commande sont aussi si on supprime la commande
- L'instruction responsable de cette suppression c'est le FK lie dans la table ligne_commande avec **ON DELETE CASCADE**

## 4 - Repérez **trois données absurdes** que le schéma actuel accepte sans broncher (indice : essayez d’insérer à la main un prix négatif). Notez-les : vous les corrigerez au niveau 1 et 2.

- prix negative
- nom du plat peut etre un nombre
- pas de verification de numero de table avant de valider un commande

## 5 - Pour la requete b ,on n'obtient pas 200 car on fait une creation et il y a un retour : "location du nouveau" donc 201 

## 6 - Pour la requete ,

- POSTGRES qui bloque la suppression
- return $this->erreur('Ce plat figure déjà dans des commandes, il ne peut pas être supprimé.', 409);

## 7 - Creation d'une commande

- curl -X POST http://localhost:8080/api/commandes -H "Content-Type: application/json" -d '{"numero_table": 6, "lignes": [{"id_plat": 4,"quantite": 2},{"id_plat": 10,"quantite": 1}] }'

## 0.4 Suivre une requête de bout en bout

Quand on clique sur **Ajouter le plat**, voici le chemin parcouru. Complétez le tableau en indiquant, pour chaque étape, **le fichier et le nom de la fonction** :

| # | Étape | Fichier | Fonction / ligne |
|---|---|---|---|
| 1 | Le formulaire est soumis | `components/PlatForm.vue` | `enregistrer() , ligne 33` |
| 2 | La requête HTTP est construite | `api.js` | `requete()` |
| 3 | Vite transmet `/api/...` au port 8080 | `vite.config.js` | `defineConfig , ligne 11` |
| 4 | CodeIgniter choisit le contrôleur | `app/config/Route.php` , `App/Controller/Api` | group() |
| 5 | Le contrôleur lit le JSON | | |
| 6 | Les règles de validation sont vérifiées | | |
| 7 | La ligne est insérée | | |
| 8 | Le formulaire prévient l’écran parent | | `emit(…)` |
| 9 | L’écran recharge la liste | `views/CarteView.vue` | |
