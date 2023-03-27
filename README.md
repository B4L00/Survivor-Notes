# Survivor-Notes
Des notes persos pour la programmation.<br />
Raccourcis de vscode, de vim, de terminal et autres tips utiles.


# Terminator
**ctrl-shift-E**  sépare la fenetre actuelle en une nouvelle fenêtre verticale<br />
**ctrl-shift-O**  sépare la fenetre actuelle en une nouvelle fenêtre horizontale<br />
**ctrl-shift-W**  ferme la fenêtre actuelle<br />
**ctrl-shift-N**  (Next) prochaine fenêtre<br />
**ctrl-shift-P**  (Previous) fenêtre précèdente<br />
**ctrl-shift-X**  Passe en plein écran la fenêtre actuelle (faire pareil pour revenir comme avant)


# VSCode
**alt-fleche**   deplace une ligne (en haut ou en bas)<br />
**ctrl-maj-k**   supprime une ligne<br />
**ctrl-/**       ajoute / supprime un commentaire a la ligne <br />
**ctrl-maj-a**   ajoute un ensemble de commentaire<br />
**ctrl-p**       aller au fichier<br />
**ctrl-tab**     aller au fichier suivant <br />
**ctrl-w**       fermer le fichier en cours <br />
**ctrl-\\**      fractionner l'editeur <br />
**ctrl-1**       aller sur le groupe 1 <br />
**ctrl-2**       aller sur e groupe 2 <br />
**ctrl-`**       aller sur le terminal <br />

# VIM
**I**		insert mode<br />
**:x** 	enregistre et quitte<br />
**:w**  enregistre<br />
**:wq** enregistre et quitte (equivalent a **:x**)<br />
**:q**  quitte<br />
<br />
**yy**  copier une ligne<br />
**p**   coller la ligne précédemment copiée<br />
**^**		début de ligne<br />
**$**		fin de ligne<br />
**gg**	début du fichier<br />
**G**		fin de fichier<br />
**shift + V** sélectionne une ligne (retaper pour retirer)<br />


# Makefile

### Regles
**all**     make par defaut<br />
**clean**   supprime les .o <br />
**fclean**  supprime les .o et l'executable / biblio<br />
**re**      comme fclean et re make derriere<br />
<br />
### Noms et definitions
**"VAR :="**  definit la constante VAR<br />
**$(VAR)**  utilise la variable VAR<br />
**CC**			:=	pour le compilateur (cc, clang, gcc, g++ ...)<br />
**CFLAGS** 	:=	pour les flags (-Wall -Werror -Wextra ...)<br />
**CPPFLAGS** := pour les flags en C++
**NAME**		:=  nom de l'éxecutable créé<br />
**SRCS**		:=  tous les fichiers sources utiles pour créer l'éxec<br />
**OBJ**			:=   toud les objets crées à partir de **SRCS**<br />
<br />
### prefix / suffix
```Makefile
SRCS		:= $(addprefix $(SRCS_D), $(addsuffix .c, $(SRCS_F)))
             ^                      ^__ ajoute le suffixe .c a la constante SRCS_F. Donc ajoute .c a tout les fichiers etant definit dans SRCS_F
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
        @make -C $(LIBFT_D)
        @mv $(LIBFT_D)/libft.a .
        @ar rcs $(NAME) $(OBJ) <-- facultatif, seulement pour creer une biblio

%$(SRCS_D).o:   %$(SRCS_D).c
        $(CC) $(CFLAGS) -I include -c $< -o $@

clean:
        @rm -f $(OBJ)
        @cd srcs/libft; make clean

fclean:         clean
        @rm -f $(NAME)
        @cd srcs/libft; make fclean

re:             fclean all

.PHONY:         all clean fclean re bonus
```
# Compilation
### Fonctionnement
### Options
# Valgrind

```bash
valgrind --leak-check=full --track-origins=yes
```
**--leak-check=full** : Voir toutes les fuites <br>
**--track-origins=yes** : Trouver l'origine des variables non initialisées.

