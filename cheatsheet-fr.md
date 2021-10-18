# Cheatsheet - Environnement de dev C++

Quelques tips pour commencer a developper en C++.

## Documentation

Pour la documentation, [cppreference](https://en.cppreference.com/w/) est votre
amie. La version Anglaise est plus complete, et alternativement vous pouvez la
consulter via [DevDocs](https://devdocs.io/). Cette documentation est mise a
jour regulierement par des gens qui participent a l'evolution du langage, c'est
la meilleure a ce jour.

Evitez a tout prix cplusplus.com. Elle n'est pas a jour et melange beaucoup de
C avec du vieux C++. De plus, elle ne fournit aucune info sur la disponibilite
des elements de langages ou de librairie selon les versions.

## IDE / Autocompletion

**Tout sauf CodeBlocks.**

Dans le cadre des TPs, je vous recommande d'eviter tout IDE qui ne supporte
pas directement CMake comme Visual Studio, sauf si vous savez deja generer
une solution Visual Studio via CMake.

Recommendation par defaut: [CLion](https://www.jetbrains.com/clion/):

- Excellent support de CMake,
- Autocomplete qui fonctionne sans configuration,
- Fonctions de debug...

[Kate](https://kate-editor.org/) et [Kdevelop](https://www.kdevelop.org/) sont
egalement des solutions tres viables (bien plus que les solutions GTK comme
Geany ou GEdit). Les deux softs permettent d'avoir une autocompletion robuste
via Clangd.

Autrement, si vous avez deja un editeur de choix, renseignez-vous sur
[LSP](https://microsoft.github.io/language-server-protocol/) et trouvez un
plugin qui supporte le protocole LSP pour avoir l'autocompletion via
[clangd](https://clangd.llvm.org/). Vous pouvez vous referer a la page
[getting started](https://clangd.llvm.org/installation) pour trouver une liste
de plugins qui marchent bien.

Clangd est un language server qui repose directement sur le compilateur Clang
pour vous fournir des messages d'erreur et des completions, et beneficie donc
du meme (excellent) moteur semantique qui analyse votre code a la compilation.

La seule condition necessaire a son fonctionnement est que vous ayez un fichier
`compile_commands.json` dans l'arborescence de votre projet pour que le serveur
`clangd` puisse indexer les fichiers de votre projet. Les projets CMake que je
donne generent ce fichier par defaut, mais vous pouvez forcer sa generation en
ajoutant `-DCMAKE_EXPORT_COMPILE_COMMANDS=ON` lorsque vous appelez CMake a
l'etape suivante.

# CMake

Pour ecrire et/ou comprendre du CMake, seule
[la doc officielle](https://cmake.org/cmake/help/latest/) saura vous aider.

Pour compiler en console, mettez-vous dans le dossier qui contient le fichier
`CMakeLists.txt` puis:

```sh
mkdir build # Creation du dossier de compil
cd build    # On se met dedans pour generer les fichiers
cmake ../   # On genere un Makefile
make        # On build
```