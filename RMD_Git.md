## Pour cloner un projet (t�l�charger)

git clone https://github.com/ShadokDeimos/supbank-web-app.git

## Pour sauvegarder votre taff (Commit)

git status
git add .		Ajouter tous les fichiers dans votre commit
git status 		Pour v�rifier que tous les fichiers sont pris
git commit -m "	"	Le commit = Le commit
git status		Pour v�rifier qu'il est bien pass�

git push 		Met � jour la branche sur GitHub

## Pour commencer � taffer

git status
git checkout -b Androhius/HomePage

## Retourner sur la branche master

git checkout master

## Ca fait longtemps que j'ai pas bosser sur ma branche

git status  			=> branche Androhius/homePage
git fetch			Met � jour les branches locales
git merge master		Applique les modifs de la master, de la branche sur laquelle tu te trouve
OU
git merge origin/master		Si y'a pas de conflit �a fait comme un commit

Si y'a conflit

git add .
git commit -m ""
git push

## Ca fait longtemps...

git status			Vous �tes sur la branche master
git pull			Met � jour ta branche local (en l'occurence master)

git checkout -b VaictusS/ValidationTacoin

## Supprimer une branche locale

$ git branch -d branch_name
$ git branch -D branch_name
  /!\ -D -> --delete-force
  /!\ -d -> --delete

## Pour supprimer une branche remote

$ git push <remote_name> --delete <branch_name>

## Ecraser

## Définit user

git config --global user.name "username"
git config --global user.email "email"

## Rebase

  Sur la branche local

git stash
git rebase BRANCH
git stash apply
