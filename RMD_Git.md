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

## Delete a folder from the tree that has already been added
=> After add folder to .gitignore file
git rm -r --cached <folder>

## Ecraser

## Define user

> Global
```
git config --global user.name "username"
git config --global user.email "email"
```

> Locally to one repo
```
git config user.email <mail>
git config user.name <name>
```


## Rebase

  Sur la branche local

git stash
git rebase BRANCH
git stash apply

## Multiple account configuration with SSH


### Create ssh key 
```
cd ~/.ssh

ssh-keygen -t rsa -b 4096 -C "your_personal_email@domain.com"
	# save as id_rsa_personal
ssh-keygen -t rsa -b 4096 -C "your_work_mail@domain.com"
	# save as id_rsa_work
```

4 files are created : id_rsa_personal / id_rsa_personal.pub / id_rsa_work / id_rsa_work.pub
	=> Files with .pub are public files to add to GitHub account

### Add public key on GitHub

Github account > Settings > SSH and GPG keys > New SSH key > ...

### Create configuration files to  manage keys

```
cd ~/.ssh
touch config

# Edit config file to add theses lines 

# Personal account - default config
Host github.com-personal
   HostName github.com
   User git
   IdentityFile ~/.ssh/id_rsa_personal

# Work account
Host github.com-work
   HostName github.com
   User git
   IdentityFile ~/.ssh/id_rsa_work

cd ~
nano ~/.gitconfig

# Add this content to ~/.gitconfig

[user]
    name = John Doe
    email = johndoe@domain.com
[includeIf "gitdir:~/path/to/work/dir/"]
    path = ~/path/to/work/dir/.gitconfig


nano ~/path/to/work/dir/.gitconfig

# Add this content to ~/path/to/work/dir/.gitconfig

[user]
    email = john.doe@company.com

# In order for the work configuration to work correctly, we are assuming that you have a directory called work which contains all your work-related # projects.
```

### Save key identities in local machine

```
cd ~
ssh-add -D

ssh-add .ssh/id_rsa_personal
ssh-add .ssh/id_rsa_work

ssh-add -l 		# Check if keys were saved correctly
```

### Modify Remote link

```
git remote set-url https://github.com/<user>/<project>.git
```