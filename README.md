# Parser du langage M

Ce dépôt contient un "[parser](https://fr.wiktionary.org/wiki/parser)" du langage dédié nommé "M" utilisé par
le code source de la [calculette des impôts sur les revenus](https://git.framasoft.org/openfisca/calculette-impots-m-source-code).

- [`m_language.cleanpeg`](m_language.cleanpeg) contient la description de la grammaire du langage M
au format [cleanpeg](http://igordejanovic.net/Arpeggio/grammars/#grammars-written-in-peg-notations)
- [`scripts/m_source_file_to_json_ast.py`](scripts/m_source_file_to_json_ast.py) est le script de transformation du code source
vers un AST en JSON
- [`json/chap-1.json`](json/chap-1.json.json) est un exemple de la transformation en JSON du fichier
[`chap-1.m`](https://git.framasoft.org/openfisca/calculette-impots-m-source-code/tree/master/src/chap-1.m)

## Installation

Le langage Python 3 est utilisé.

Ce paquet n'est pas publié sur le dépôt [PyPI](https://pypi.python.org/pypi) donc pour l'installer il faut passer par `git clone`.

```
git clone https://git.framasoft.org/openfisca/calculette-impots-m-language-parser.git
cd calculette-impots-m-language-parser
pip3 install --editable . --user
```

> L'option `--user` sert sur les systèmes GNU/Linux.

Un utilisateur plus expérimenté en Python peut utiliser
un [`virtualenv`](https://virtualenv.readthedocs.org/en/latest/) s'il le souhaite.

## Utilisation

Ce projet est à considérer comme un dépôt de données JSON nécessaires au projet
[calculette-impots-python](https://git.framasoft.org/openfisca/calculette-impots-python).

## Grammaire

Le fichier de grammaire [`m_language.cleanpeg`](m_language.cleanpeg) est au format [Clean PEG](http://igordejanovic.net/Arpeggio/grammars/).

La bibliothèque utilisée pour le "parsing" est [Arpeggio](http://igordejanovic.net/Arpeggio/).

La partie de la grammaire touchant aux expressions est basée
sur [ce tutoriel](http://igordejanovic.net/Arpeggio/tutorials/calc/).

## Regénérer les fichiers JSON

Les commandes suivantes sont a priori inutiles, à moins que les fichiers source M, la grammaire
ou bien le code du parser ait changé. Les fichiers JSON sont de toute façon commités dans le répertoire [json](json).

```
# Convertir un répertoire de sources M entier en AST
$ ./calculette_impots_m_language_parser/scripts/convert_dir.sh /path/to/calculette-impots-m-source-code/src

# Extraire les données JSON sémantiques
$ python3 calculette_impots_m_language_parser/scripts/json_ast_to_data.py -v
```

Pour convertir un fichier M particulier :

```
$ python3 calculette_impots_m_language_parser/scripts/m_source_file_to_json_ast.py file.m
```
