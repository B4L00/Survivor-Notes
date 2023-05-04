# Survivor-Notes
Des notes persos pour la programmation.<br />
Raccourcis de vscode, de vim, de terminal et autres tips utiles.

---------------------------

# Sommaire

- [Terminator](#Terminator)
- [VSCode](#VSCode)
- [VIM](#VIM)
- [Makefile](#Makefile)
  - [Règles](#Règles)
  - [Noms et definitions](https://github.com/B4L00/Survivor-Notes#noms-et-definitions)
  - [prefix / suffix](https://github.com/B4L00/Survivor-Notes#prefix--suffix)
  - [Exemple](#Exemple)
- [Compilation](#Compilation)
  - [Fonctionnement](#Fonctionnement)
  - [Options](#Options)
- [Valgrind](#Valgrind)

---------------------------

## Terminator
**ctrl-shift-E**  sépare la fenêtre actuelle en une nouvelle fenêtre verticale<br />
**ctrl-shift-O**  sépare la fenêtre actuelle en une nouvelle fenêtre horizontale<br />
**ctrl-shift-W**  ferme la fenêtre actuelle<br />
**ctrl-shift-N**  (Next) prochaine fenêtre<br />
**ctrl-shift-P**  (Previous) fenêtre précédente<br />
**ctrl-shift-X**  Passe en plein écran la fenêtre actuelle (faire pareil pour revenir comme avant)

---------------------------

## VSCode
**alt-fleche**   déplace une ligne (en haut ou en bas)<br />
**ctrl-maj-k**   supprime une ligne<br />
**ctrl-/**       ajoute / supprime un commentaire à la ligne <br />
**ctrl-maj-a**   ajoute un ensemble de commentaire<br />
**ctrl-p**       aller au fichier<br />
**ctrl-tab**     aller au fichier suivant <br />
**ctrl-w**       fermer le fichier en cours <br />
**ctrl-\\**      fractionner l'éditeur <br />
**ctrl-1**       aller sur le groupe 1 <br />
**ctrl-2**       aller sur e groupe 2 <br />
**ctrl-`**       aller sur le terminal <br />
<br />
Pour mettre les tabs par défaut : ctrl+, => affiche les options<br />
Décocher dans espace de travail **Editor: Insert Spaces** <br />

---------------------------

## VIM
**I**		insert mode<br />
**:x** 	enregistre et quitte<br />
**:w**  enregistre<br />
**:wq** enregistre et quitte (equivalent à **:x**)<br />
**:q**  quitte<br />
<br />
**yy**  copier une ligne<br />
**p**   coller la ligne précédemment copiée<br />
**^**		début de ligne<br />
**$**		fin de ligne<br />
**gg**	début du fichier<br />
**G**		fin de fichier<br />
**shift + V** sélectionne une ligne (retaper pour retirer)<br />

---------------------------

## Makefile

### Règles
**all**     make par defaut<br />
**clean**   supprime les .o <br />
**fclean**  supprime les .o et l'éxécutable / biblio<br />
**re**      comme fclean et re make derrière<br />
**.PHONY**  évite d'appeler un fichier qui se nomme pareil qu'une règle<br />
<br />
### Noms et definitions
**"VAR :="**  définit la constante VAR<br />
**$(VAR)**  utilise la variable VAR<br />
**CC**			:=	pour le compilateur (cc, clang, gcc, g++ ...)<br />
**CFLAGS** 	:=	pour les flags (-Wall -Werror -Wextra ...)<br />
**CPPFLAGS** := pour les flags en C++<br />
**NAME**		:=  nom de l'éxecutable créé<br />
**SRCS**		:=  tous les fichiers sources utiles pour créer l'éxec<br />
**OBJ**			:=  tous les objets créent à partir de **SRCS**<br />
**%.c** fait référence à tous les fichiers .c (idem pour %.o)<br />
**$<** fait réference à la source de la règle<br />
**$@** fait réference au(x) résultat(s) de la règle<br />
<br />
### prefix / suffix
```Makefile
SRCS	:= $(addprefix $(SRCS_D), $(addsuffix .c, $(SRCS_F)))
             ^                      ^__ ajoute le suffixe .c à la constante SRCS_F. Donc ajoute .c à tous les fichiers étant définit dans SRCS_F
             |__ ajoute le prefix contenu dans SRCS_D, dans l'exemple : "srcs/"
          Ce qui fabrique les chemins suivants : srcs/file1.c, srcs/file2.c, srcs/file3.c et srcs/main.c

Idem avec OBJ en remplacant .c par .o dans l'addsuffix
```

### Exemple
``` Makefile
CC        := cc
CFLAGS    := -g -Wall -Wextra -Werror

NAME      := name

SRCS_D    := srcs/

LIBFT_D   := $(SRCS_D)/libft

SRCS_F    := file1 file2 file3 ... main

SRCS      := $(addprefix $(SRCS_D), $(addsuffix .c, $(SRCS_F)))
OBJ       := $(addprefix $(SRCS_D), $(addsuffix .o, $(SRCS_F)))

all:            $(NAME)

$(NAME):        $(OBJ)
        make -C $(LIBFT_D)
        mv $(LIBFT_D)/libft.a .
        ar rcs $(NAME) $(OBJ) <-- facultatif, seulement pour créer une biblio
        $(CC) $(CFLAGS) $(OBJ) -L. -lft -o $(NAME) <-- pour créer un exec 

clean:
        rm -f $(OBJ)

fclean:         clean
        rm -f $(NAME)
        make fclean -C $(LIBFT_D)

re:             fclean all

.PHONY:         all clean fclean re bonus
```

---------------------------

## Compilation
### Fonctionnement
**Preprocessing :**     crée des fichiers temporaires<br />
**Compilation :**       crée les .o à partir de ces fichiers temporaires<br />
**Edition des liens**:  crée l'executable à partir des .o<br />

**Preprocessing + Compilation**   ```gcc -c file.c``` --> sort un file.o <br />
**Edition des liens**             ```gcc -o exec file.o``` --> sort exec <br />

### Options
**-c** compile mais ne lie pas<br />
**-o** permet l'édition des liens et de nommer le fichier executable<br />
**-g** permet le debuging<br />
**-l** cherche une librairie<br />
**-L** cherche le dossier d'une librairie<br />
**-I** cherche le dossier des headers (.h)<br />
**-Werror** tous les warnings deviennent errors<br />
**-Wall** affiche tous les warnings<br />
**-Wextra** affiche d'autres warnings non géré par -Wall<br />

---------------------------

## Valgrind

```bash
valgrind --leak-check=full --show-leak-kinds=all
```
**--leak-check=full** : Voir toutes les fuites <br>
**--track-origins=yes** : Trouver l'origine des variables non initialisées. <br>
```bash
valgrind --track-fds=yes --leak-check=full --show-leak-kinds=all --trace-children=yes
```
```bash
valgrind --track-fds=yes --leak-check=full --show-leak-kinds=all --child-silent-after-fork=yes
```
**--child-silent-after-fork=yes** : ne montre pas les erreurs de leaks dans les processus fils.
