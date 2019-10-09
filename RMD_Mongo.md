# # # # #    MONGODB    # # # # #

• LISTE LES DB

show dbs

• LISTE LES COLLECTIONS

show collections

• LANCER DB

"C:\Program Files\MongoDB\Server\4.0\bin\mongod.exe" --dbpath="C:\Users\Mathieu\Desktop\Mushin\chat_poc\MongoDb"
	-> Pour lancer le serveur
- mongo.exe	-> Pour lancer l'invite de commande

• CREATE/USE

use dbsupsup		-> Permet de sélectionner une db et la crée si n'existe pas

• INSERT

db.nomCollection.insert({nom:"Pouet", prenom:"Chouette"})
			-> Insert dans la collection et crée si n'existe pas

• FIND

db.nomCollection.find()
			-> Retourne ce que contient la collection
db.nomCollection.find({clé:valeur})
db.nomCollection.find({clé:valeur, clé2:valeur})
			-> Retourne avec filtre / Equivalent de WHERE
db.nomCollection.find({clé:valeur}).count()
			-> Compte le nombre de résultat du find

$gt 	-> plus grand que
$lt 	-> plus petit que
$gte	-> plus grand ou égal à
$lte	-> plus petit ou égal à

$or	-> opérateur OU
$and 	-> opérateur ET
$in
$all
$exist
$type
$regex

ex : db.produits.find({price: {$gte:9997, $lt:9999}})

db.nomCollection.find({clé: valeur}, {compteur:1})
			-> Ne récupère la valeur que de _id & compteur
db.nomCollection.find({clé: valeur}, {_id:0, compteur:1})
			-> Ne récupère que le compteur sans id
db.nomCollection.find({clé: {$in: [500, 600, 700]}})
			-> la clé vaudra ALTERNATIVEMENT 500, 600 ou 700
db.nomCollection.find({clé: {$in: [500, 600, 700]}}).sort({mill:1})
			-> la clé vaudra SUCCESSIVEMENT 500, 600 et 700
db.nomCollection.find({clé: {$in: [500, 600, 700]}}).sort({mill:1})

• UPDATE

db.nomCollection.update({clé: valeur}, {$set : {clé3: valeur}})
			-> Ne met à jour que le 1er document sorti
db.nomCollection.update({clé: valeur}, {$set : {clé3: valeur}}, {multi:true})
			-> Met à jour tous les documents trouvés

• DELETE PROPERTIES

db.nomCollection.update({dixmill: 666} , {$unset : {suspect:1}}, {multi:true})
			-> Supprime la propriété "suspect"

• MAJ of Array

db.nomCollection.insert({compteur:100001, tab:['a', 'b', 'c']})
db.nomCollection.update({compteur:100001}, {$push: {tab: 'd'}})
			-> Ajoute la valeur "d" dans l'Array tab
			?> $pushAll pour ajouter plusieurs valeurs en 1 fois
db.nomCollection.update({compteur:100001}, {$pop : {tab:1}})
			-> L'Array à perdu son dernier élément ajouté
db.nomCollection.update({compteur:100001}, {$pop : {tab:-1}})
			-> L'Array à perdu son prmier élément
db.nomCollection.update({compteur:100001}, {$addToSet : {tab : 'b'}})
			-> $addToSet permet d'ajouter sans doublons

• DELETE DOCUMENT

db.nomCollection.remove({pouet: "cacahuete"})
			-> Supprime tous les documents qui ont pour valeur "cacahuete" à la propriété "pouet"
