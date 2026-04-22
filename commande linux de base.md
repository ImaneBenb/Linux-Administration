### Récapitulatif général
#### Tableau récap

| Commande  | Syntaxe                                                   | Description                                   |
| --------- | --------------------------------------------------------- | --------------------------------------------- |
| `echo`    | `echo "texte"`                                            | Affiche un message ou une variable            |
| `whoami`  | `whoami`                                                  | Nom de l'utilisateur courant                  |
| `id`      | `id` / `id nom_user` / `id -un`                           | Infos utilisateur et groupes                  |
| `pwd`     | `pwd`                                                     | Chemin du répertoire courant                  |
| `ls`      | `ls` / `ls -a` / `ll`                                     | Lister le contenu (avec cachés, avec détails) |
| `cd`      | `cd <chemin>` / `cd ..` / `cd ~`                          | Naviguer entre répertoires                    |
| `mkdir`   | `mkdir <nom>` / `mkdir -p <parent/enfant>`                | Créer un répertoire                           |
| `touch`   | `touch <fichier>`                                         | Créer un fichier vide                         |
| `echo >`  | `echo "texte" > fichier.txt`                              | Écrire directement dans un fichier            |
| `cp`      | `cp <src> <dest>` / `cp -r <dir> <dir_copy>`              | Copier fichier ou répertoire                  |
| `mv`      | `mv <src> <dest>`                                         | Déplacer ou renommer                          |
| `rm`      | `rm <fichier>` / `rm -i` / `rm -r <dossier>`              | Supprimer fichier ou répertoire               |
| `rmdir`   | `rmdir <dossier>`                                         | Supprimer un répertoire vide                  |
| `cat`     | `cat <fichier>` / `cat -n`                                | Afficher le contenu d'un fichier              |
| `head`    | `head <fichier>` / `head -n5` / `head -c20`               | Premières lignes / caractères                 |
| `tail`    | `tail <fichier>`                                          | Dernières lignes d'un fichier                 |
| `diff`    | `diff <f1> <f2>` / `diff -r <d1> <d2>`                    | Différences entre fichiers ou répertoires     |
| `grep`    | `grep 'mot' <fichier>` / `grep -w` / `grep -i` / `-c` ... | Rechercher dans un fichier                    |
| `wc`      | `wc -l <fichier>` / `-w` / `-c`                           | Compter le nombre de lignes, mots, caractères |
| `sudo`    | `sudo <commande>`                                         | Exécuter avec les privilèges root             |
| `chown`   | `sudo chown owner:group <fichier>` / `chown -R`           | Changer le propriétaire                       |
| `chmod`   | `sudo chmod XXX <fichier>` / `chmod -R`                   | Changer les permissions                       |
| `useradd` | `sudo useradd <user>` / `useradd -m`                      | Créer un utilisateur                          |
| `passwd`  | `sudo passwd <user>` / `passwd -S`                        | Gérer le mot de passe                         |
| `usermod` | `sudo usermod -d/-s/-aG <user>`                           | Modifier un utilisateur                       |
| `su`      | `su - <user>` / `exit`                                    | Changer de session                            |
| `userdel` | `sudo userdel <user>` / `userdel -r`                      | Supprimer un utilisateur                      |
#### Bloc de syntaxe 

```bash
# ── Affichage & Informations ──────────────────────────────────────
echo "texte"
whoami
id
id nom_user
id -un
pwd

# ── Navigation & Répertoires ──────────────────────────────────────
ls
ls -a
ll
cd <chemin>
cd ..
cd ~
mkdir <nom>
mkdir -p <parent/enfant>
mkdir -m XXX

# ── Fichiers : Création ──────────-────────────────────────────────
touch <fichier>
echo "texte" > fichier.txt

# ── Fichiers : Copie ──────────────────────────────────────────────
cp <fichier_src> <fichier_dest>
cp <fichier> <répertoire>/
cp -r <dossier_src> <dossier_dest>

# ── Fichiers : Déplacement & Renommage ────────────────────────────
mv <ancien_nom> <nouveau_nom>
mv <fichier> <répertoire>/
mv <dossier_src> <dossier_dest>

# ── Fichiers : Suppression ────────────────────────────────────────
rm <fichier>
rm -i <fichier>
rm -r <dossier>
rmdir <dossier_vide>

# ── Lecture & Comparaison ─────────────────────────────────────────
cat <fichier>
cat -n <fichier>
head <fichier>
head -n5 <fichier>
head -c20 <fichier>
tail <fichier>
diff <fichier1> <fichier2>
diff -r <dossier1> <dossier2>
grep mot <fichier>       
grep -i mot <fichier>     
grep -i 'mot ou phrase' <fichier>   
grep -c mot <fichier>     
grep -n mot <fichier>     
grep -l mot <f1> <f2>   
grep -w mot_exact <fichier>   
grep 'exp_regul' <fichier>            
wc -l <fichier>
wc -w <fichier>
wc -c <fichier>

# ── Permissions & Propriété ───────────────────────────────────────
sudo chown owner:group <fichier>
sudo chown -R owner:group <dossier>
sudo chmod XXX <fichier>
sudo chmod -R XXX <dossier>
sudo <commande>

# ── Gestion des utilisateurs ──────────────────────────────────────
sudo useradd <user>
sudo useradd -m <user>
sudo passwd <user>
sudo passwd -S <user>
sudo usermod -d /home/nouveau <user>
sudo usermod -s /bin/bash <user>
sudo usermod -aG sudo <user>
su - <user>
exit
sudo userdel <user>
sudo userdel -r <user>

# ── CPU ────────────────────────────────────────────────────────────
nproc --all
```