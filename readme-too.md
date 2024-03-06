Please, read this tool

This is reall important

Cómo guarda Git toda la información
The workspace is the directory tree of (source) files that you see and edit.

The index is a single, large, binary file in /.git/index, which lists all files in the current branch, their sha1 checksums, time stamps and the file name -- it is not another directory with a copy of files in it.

The local repository is a hidden directory (.git) including an objects directory containing all versions of every file in the repo (local branches and copies of remote branches) as a compressed "blob" file.

Don't think of the four 'disks' represented in the image above as separate copies of the repo files.

(Fuente: https://stackoverflow.com/a/3690796)

Estados de los archivos
Cada archivo del Working Directory puede estar en dos estados:

TRACKED = son los archivos de los que Git tiene conocimiento, bien porque (1) están en el Staging Index o (2) porque estaban en el último snapshot (commit) y, por lo tanto, no es necesario que estén en el STAGE para saber si hay diferencias; porque comparándolos con el último COMMIT ya lo sabe. Pero sí que es necesario volvera a añadir al STAGE los archivos que queramos preparar para el siguiente COMMIT. El caso 2 es el de cuando recién clonas un repositorio.

Los TRACKED FILES Pueden estar como: - unmodified - modified - staged

UNTRACKED = todo lo demás, es decir, cualquier archivo de tu Working Directory que...

no estuviera en el último snapshot
que no esté en el Staging Index (status code: ?? en color rojo).
Cuando CLONAS un repositorio (git clone) TODOS LOS ARCHIVOS están en estado TRACKED-UNMODIFIED, porque Git solo ha hecho un CHECKOUT de ellos y tú todavía no has editado ningún archivo. Es decir, están tracked porque el repositorio ya contiene un commit donde se añadieron, y Git puede comparar tu Working Directory con ese último commit para saber si hay diferencias. Pero si haces git status puedes comprobar que no están en el Staging Index, porque por seguridad Git te obliga a añadir manualmente los archivos que quieres incluir en el siguiente commit, así se evita incluir más archivos de la cuenta.

Cuando haces COMMIT todos los archivos del STAGE se quitan de ahí y en el Working Directory se les asigna el estado de UNMODIFIED de nuevo, porque esos últimos cambios pasan a ser la nueva referencia para saber si se han producido nuevas modificaciones. Por eso al hacer un git status -sb muestra el mensaje "nothing to commit, working tree clean", porque ahora no hay nada en el stage ya que se empieza de nuevo.
