# Cheatsheet - C++ development environment

A few tips to start C++ development.

## Documentation

The best documentation available to date is
[cppreference](https://en.cppreference.com/w/). It is regularly updated by
people who participate to the evolution of the language itself. Alternatively,
[DevDocs](https://devdocs.io/) is available as a more practical frontend to
cppreference. All it takes is 2 minutes to configure it properly.

**Avoid cplusplus.com at all cost.** This website is out of date, it's just a
mix of C with deprecated C++.

## IDE / Autocomplete

**Avoid Code::Blocks at all costs.**

Dans le cadre des TPs, je vous recommande d'eviter tout IDE qui ne supporte
pas directement CMake comme Visual Studio, sauf si vous savez deja generer
une solution Visual Studio via CMake.

For most projects, I would suggest to avoid IDEs that do not support CMake
properly such as Visual Studio, unless you feel comfortable enough with CMake
to generate a Visual Studio solution.

Default recommandation: [CLion](https://www.jetbrains.com/clion/):

- Excellent CMake support,
- Autocomplete available out of the box,
- Integrated debugger

[Kate](https://kate-editor.org/) and [Kdevelop](https://www.kdevelop.org/) are
very viable alternatives (much better than GTK solutions like Geany or Gedit).
Both software can provide robust autocompletion via
[Clangd](https://clangd.llvm.org/).

Otherwise, if you already have an editor of choice, get familiar with
[LSP](https://microsoft.github.io/language-server-protocol/) and find a plugin
that implements it to get autocompletion via [Clangd](https://clangd.llvm.org/).
You may refer to the [getting started](https://clangd.llvm.org/installation)
page to find a list of plugins that should work very well.

### About [Clangd](https://clangd.llvm.org/)

[Clangd](https://clangd.llvm.org/) is a language server that relies on the Clang
frontend to provide error messages and completions, thus having a bulletproof
C++ syntaxic and semantic engine for analyzing and indexing your code.

La seule condition necessaire a son fonctionnement est que vous ayez un fichier
`compile_commands.json` dans l'arborescence de votre projet pour que le serveur
`clangd` puisse indexer les fichiers de votre projet. Les projets CMake que je
donne generent ce fichier par defaut, mais vous pouvez forcer sa generation en
ajoutant `-DCMAKE_EXPORT_COMPILE_COMMANDS=ON` lorsque vous appelez CMake a
l'etape suivante.

The only necessary condition for its use is the availability of a
`compile_commands.json` file in your project tree to ensure `clangd` can
properly index the files of your project. Some CMake projects will generate it
for you, otherwise you can add `-DCMAKE_EXPORT_COMPILE_COMMANDS=ON` to the CMake
command to override it in the next step.

## The CMake build system

To read and/or understand CMake, only practice and the
[official documentation](https://cmake.org/cmake/help/latest/) may help you.

To compile a CMake project using the console, ensure you're in the same
directory as the top `CMakeLists.txt` file, then run:

```sh
mkdir build # Creation of the build directory
cd build    # Change to that directory
cmake ../   # Generating the Makefile
make        # Building the default Make target
```

## [Compiler Explorer](https://godbolt.org/)

[Compiler Explorer](https://godbolt.org/) is an open-source website by
Matt Godbolt that allows you to quickly edit, compile, and run C++ code.
Public service at its best, you can even select which compiler/toolchain to use
and take a look at the generated assembly.
