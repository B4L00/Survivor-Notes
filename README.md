# Survivor-Notes
Des notes persos pour la programmation.<br />
Raccourcis de vim, de terminal et autres tips utiles.


# Terminator
**ctrl-shift-E**  sépare la fenetre actuelle en une nouvelle fenêtre verticale<br />
**ctrl-shift-O**  sépare la fenetre actuelle en une nouvelle fenêtre horizontale<br />
**ctrl-shift-W**  ferme la fenêtre actuelle<br />
**ctrl-shift-N**  (Next) prochaine fenêtre<br />
**ctrl-shift-P**  (Previous) fenêtre précèdente<br />
**ctrl-shift-X**  Passe en plein écran la fenêtre actuelle (faire pareil pour revenir comme avant)


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


# Makefile
' **:=** '	définit une constante<br />
' **=** '		définit une variable<br />
<br />
**CC**			:=	pour le compilateur (cc, clang, gcc, g++ ...)<br />
**CFLAGS** 	:=	pour les flags (-Wall -Werror -Wextra ...)<br />
**CPPFLAGS** := pour les flags en C++
**NAME**		:=  nom de l'éxecutable créé<br />
**SRCS**		:=  tous les fichiers sources utiles pour créer l'éxec<br />
file1\ <br />
file2\ <br />
file3 <br />
**OBJ**			:=  **$(SRCS:.c=.o)** liste des objets crées à partir de **SRCS**<br />

### Regles
**all**  make par defaut<br />
<br />
Les règles fonctionnent comme suit : <br />
**resultat : sources**<br />
**$<** fait réference à la source de la règle<br />
**$@** fait réference au(x) resultat(s) de la règle<br />
<br />
**%.o:	%.c**  crée les .o à partir des .c, doit être suivi par la ligne suivante :<br />
>**$(CC) $(CFLAGS) -c $< -o $@**<br />

# Valgrind

**--leak-check=full** : Voir toutes les fuites <br>
**--track-origins=yes** : Trouver l'origine des variables non initialisées.


