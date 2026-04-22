# Commandes Linux — Référence

## Table des matières

1. [[#Affichage & Informations]]
2. [[#Navigation & Répertoires]]
3. [[#Fichiers — Création, Copie, Déplacement, Suppression]]
4. [[#Lecture & Comparaison de fichiers]] 
5. [[#Permissions & Propriété]]
6. [[#Gestion des utilisateurs]]
7. [[#Récapitulatif général]]

---

## Affichage & Informations

| Commande | Description                                                                |
| -------- | -------------------------------------------------------------------------- |
| `echo`   | **Affiche un message** ou la valeur d'une variable (équivalent de `print`) |
| `whoami` | **Affiche le nom de l'utilisateur courant**                                |
| `id`     | **Affiche les infos** sur les groupes de **l'utilisateur courant**         |
| `pwd`    | **Affiche le chemin du répertoire courant**                                |
| `echo ~` | Équivalent de `pwd`                                                        |
### `echo`

```bash
echo "Hello World !"
Hello World !
```

### `id`

```bash
id
uid=1000(imane_ben) gid=1000(imane_ben) groups=1000(imane_ben),4(adm),20(dialout),24(cdrom),25(floppy),27(sudo),29(audio),30(dip),44(video),46(plugdev),116(netdev)
```
- `uid` : identifiant de l'**utilisateur**
- `gid` : identifiant du **groupe**
- `groups` : **tous les groupes de l'utilisateur**

```bash
id root
uid=0(root) gid=0(root) groups=0(root)
```
> **root** est le superutilisateur / administrateur système

`id -un` : identique à `whoami` 
- `-u` : affiche uniquement l'utilisateur
- `-n` : affiche le nom plutôt que l'identifiant numérique

```bash
id -un
imane_ben
```

---

## Navigation & Répertoires

| Commande       | Description                                              |
| -------------- | -------------------------------------------------------- |
| `ls`           | **Liste le contenu du répertoire courant**               |
| `ll`           | Comme `ls` mais avec permissions, propriétaire...        |
| `ls -a`        | Affiche aussi les fichiers cachés                        |
| `cd <chemin>`  | **Se déplacer** dans un répertoire                       |
| `cd ..`        | **Reculer d'un niveau**                                  |
| `cd ~`         | **Revenir au répertoire d'accueil**                      |
| `mkdir <nom>`  | **Créer un répertoire**                                  |
| `mkdir -p`     | Créer un répertoire avec **répertoire(s)** **parent(s)** |
| `mkdir -m XXX` | Créer un réêrtoire avec **permission**                   |
> Un fichier commençant par `.` est **caché** par défaut (ex : `.hiddenfile`)

---
[[#Table des matières]]
## Fichiers — Création, Copie, Déplacement, Suppression

### Création

| Commande                     | Description                                                                               |
| ---------------------------- | ----------------------------------------------------------------------------------------- |
| `touch <fichier>`            | **Crée un fichier vide** (si déjà existant, met à jour la date sans modifier le contenu)  |
| `echo "texte" > fichier.txt` | **Écrit directement dans un fichier** (le crée s'il n'existe pas, **écrase** s'il existe) |
```bash
touch file1.txt 
echo "hello" > file2.txt
echo "hidden" > .hiddenfile
mkdir toto
ls
file1.txt  file2.txt  toto
```
>Pour la commande `touch` il est possible de créer plusieurs fichiers d'affiler 

### Copie — `cp`

```bash
cp toto.txt toto_copy.txt      # copie un fichier
cp tata.txt dir/               # copie un fichier dans un répertoire
cp -r dir dir_copy             # copie un répertoire entier (-r = récursif)
```

### Déplacement & Renommage — `mv`

```bash
mv toto_copy.txt toto2.txt     # renomme un fichier
mv toto2.txt dir/              # déplace un fichier dans un répertoire
mv dir_copy dir2               # renomme un dossier
mv dir/toto2.txt ./titi.txt    # renomme et déplace en même temps
```
> `./` désigne le répertoire courant

### Suppression

| Commande          | Description                                                       |
| ----------------- | ----------------------------------------------------------------- |
| `rm <fichier>`    | **Supprime un fichier** (sans retour en arrière)                  |
| `rm -i <fichier>` | **Demande confirmation avant suppression** (`Y` = oui, `N` = non) |
| `rm -r <dossier>` | **Supprime un répertoire et son contenu**                         |
| `rmdir <dossier>` | **Supprime un répertoire** **vide** uniquement                    |

---

## Lecture & Comparaison de fichiers

### Affichage — `cat`

| Commande           | Description                                  |
| ------------------ | -------------------------------------------- |
| `cat <fichier>`    | **Affiche le contenu d'un fichier**          |
| `cat -n <fichier>` | Affiche le contenu avec les numéros de ligne |
| `cat > <fichier>`  | **Édite le contenu** du fichier directement  |
```bash
cat /tmp/hello
Hi,
I am Labby!

cat -n /tmp/hello
1  Hi,
2  I am Labby!

 # Astuce création de fichier multi-ligne
cat > file3 << EOF 
> Hello
> Learning Linux
> LabEx is fun
> EOF
```
> `<<EOF` indique que la saisie se termine quand on tape `EOF` (end of file)

### Premières / Dernières lignes — `head` & `tail`

|Commande|Description|
|---|---|
|`head <fichier>`|Affiche les 10 premières lignes|
|`head -n5 <fichier>`|Affiche les 5 premières lignes|
|`head -c20 <fichier>`|Affiche les 20 premiers caractères|
|`tail <fichier>`|Inverse de `head` (dernières lignes)|
### Différences — `diff`

Affiche les changements à faire pour que **fichier1 corresponde au fichier2**.

**Symboles dans la sortie :**
`N` = Numéro de la ligne ou intervalle de ligne
- `NcN` : **change** — lignes modifiées
- `NaN` : **add** — lignes ajoutées
- `NdN` : **delete** — lignes supprimées
- `<` : contenu du fichier 1
- `---` : séparateur
- `>` : contenu du fichier 2

```bash
diff file3 file4
2,3c2,3                    # Intervalle entre lignes 2 et 3 
< Learning Linux
< LabEx is fun
---
> Learning Linux FAST
> Goodbye
```
`diff -r` : compare deux **répertoires** (fait la `diff` des fichiers en commun, indique `Only in` pour les fichiers présents dans un seul dossier)

### Recherche dans un fichier — `grep`

`grep` affiche les **lignes où le mot recherché apparait** 
```bash
grep mot_recherché fichier.txt        # sensible au Maj/Min
grep -i mot_recherché fichier.txt     # ignorer les Maj/Min
grep -i 'mot ou phrase' fichier.txt   # chercher plusieurs mots, on met les ''
grep -c mot_recherché fichier.txt     # nb de ligne ou le mot apparait 
grep -n mot_recherché fichier.txt     # afficher le num de ligne 
grep -l mot_recherché f1.txt f2.txt   # cherche le file qui contient le mot
grep -w mot_recherché fichier.txt     # cherche le mot entier
grep 'exp_regul' fichier.txt          # rechercher des exp r dans un file 
sudo grep -w 'nom_user' /etc/passwd   # -w = mot entier
```

### Compter le nombre de lignes, mots, caractères — `wc`

```bash
wc -l fichier.txt   # compte le nombre de ligne
wc -w fichier.txt   # compte le nombre de mot
wc -c fichier.txt   # compte le nombre de caractère
```

---
[[#Table des matières]] 
## Permissions & Propriété

### Comprendre les permissions

```bash
ls -l example.txt
-rw-rw-r-- 1 root root 0 Jul 29 15:11 example.txt
```

|Caractère|Signification|
|---|---|
|`-` (1er)|Fichier (`d` = répertoire, `l` = lien)|
|`r`|**Read** — lecture|
|`w`|**Write** — écriture|
|`x`|**Execute** — exécution|
Les 9 caractères suivants se découpent en 3 groupes : **owner**, **group**, **other**
`root root 0` : nom du **owner et du group** ainsi que la **taille** du fichier 
Ensuite il y a la **date, l'heure et le nom du fichier** 

### Élévation de privilèges — `sudo`

```bash
sudo <commande>    # exécute avec les privilèges de root
```

### Changer le propriétaire — `chown`

```bash
sudo chown owner:group fichier.txt
sudo chown root:root example.txt   # exemple sur un fichier
sudo chown -R root:root new-dir    # -R = récursif sur tout un répertoire
```
> `sudo` est obligatoire (sinon "Permission denied")

### Changer les permissions — `chmod`

```bash
sudo chmod XXX fichier.txt    # X = chiffre entre 0 et 7
sudo chmod -R 750 mon-dossier # -R = récursif
```

**Calcul des droits :**

| Valeur | Permission |
| ------ | ---------- |
| 4      | Lecture    |
| 2      | Écriture   |
| 1      | Exécution  |
| 0      | Aucune     |
Exemple : `chmod 750` : 
- **owner** = **7** = lecture(4) + écriture(2) + exécution(1)
- **group** = **5** = lecture(4) + exécution(1)
- **other** = **0** = aucune permission

---
[[#Table des matières]] 
## Gestion des utilisateurs

### Créer un utilisateur — `useradd`

```bash
sudo useradd nom_user          # créer un utilisateur
sudo useradd -m nom_user       # créer avec un répertoire home/nom_user
```

**Vérifier la création** dans `/etc/passwd` :
```bash
sudo grep -w 'nom_user' /etc/passwd
nom_user:x:5001:5001::/home/nom_user:/bin/sh
```
- `x` : mot de passe (masqué)
- `5001` : uid / gid
- `/home/nom_user` : répertoire home
- `/bin/sh` : shell par défaut

### Gérer le mot de passe — `passwd`

```bash
sudo passwd nom_user    # initialiser/modifier le mot de passe (à taper 2 fois)
sudo passwd -S nom_user # voir le statut du mot de passe
```
> Les mots de passe chiffrés sont stockés dans `/etc/shadow`

### Modifier un utilisateur — `usermod`

```bash
sudo usermod -d /home/new nom_user     # changer le répertoire home
sudo usermod -s /bin/bash nom_user     # changer le shell par défaut
sudo usermod -aG sudo nom_user         # ajouter au groupe sudo
```

|Option|Description|
|---|---|
|`-d`|Changer le répertoire d'accueil|
|`-s`|Changer le shell (`/bin/bash` recommandé pour plus d'options)|
|`-aG`|Ajouter à un groupe (append to Group)|
> Ajouter un user au groupe `sudo` lui donne plus de privilèges sans avoir à connaître le mot de passe root.

### Changer de session — `su`

```bash
su - nom_user    # se connecter en tant qu'un autre utilisateur
su - root        # se connecter en root
exit             # quitter et retourner à la session précédente
```

### Supprimer un utilisateur — `userdel`

```bash
sudo userdel nom_user       # supprimer l'utilisateur
sudo userdel -r nom_user    # supprimer + home directory + mail
```

---
[[#Table des matières]]

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

