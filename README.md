# Survivor-Notes
Des notes persos pour la programmation.<br />
Raccourcis de vim, de terminal et autres tips utiles.


# Terminator
**ctrl-shift-E**  separe la fenetre actuelle en une nouvelle fenetre vertical<br />
**ctrl-shift-O**  separe la fenetre actuelle en une nouvelle fenetre horizontal<br />
**ctrl-shift-W**  ferme la fenetre actuelle<br />
**ctrl-shift-N**  (Next) prochaine fenetre<br />
**ctrl-shift-P**  (Previous) fenetre precedente<br />
**ctrl-shift-X**  Passe en plein ecran la fenetre actuelle (faire pareil pour revenir comme avant)


# VIM
**I**		insert mode<br />
**:x** 	enregistre et quitte<br />
<br />
**^**		debut de ligne<br />
**$**		fin de ligne<br />
**gg**	debut du fichier<br />
**G**		fin de fichier<br />


# Makefile
' **:=** '	definit une constante<br />
' **=** '		definit une variable<br />
<br />
**CC**			:=	pour le compilateur (cc, clang, gcc, g++ ...)<br />
**CFLAGS** 	:=	pour les flags (-Wall -Werror -Wextra ...)<br />
**CPPFLAGS** := pour les flags en C++
**NAME**		:=  nom de l'executable cree<br />
**SRCS**		:=  tous les fichiers sources utiles pour creer l'exec<br />
file1\ <br />
file2\ <br />
file3 <br />
**OBJ**			:=  **$(SRCS:.c=.o)** liste des objets crees a partir de **SRCS**<br />

### Regles
**all**  make par defaut<br />
<br />
Les regles fonctionnent comme suit : <br />
**resultat : sources**<br />
**$<** fait reference a la source de la regle<br />
**$@** fait reference au(x) resultat(s) de la regle<br />
<br />
**%.o:	%.c**  cree les .o a partir des .c, doit etre suivi par la ligne suivante :<br />
>**$(CC) $(CFLAGS) -c $< -o $@**<br />



