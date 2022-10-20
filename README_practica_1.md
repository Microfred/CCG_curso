# CCG_curso

# Funciones básicas de navegación y manejo de archivos con bash 

Windows, Mac y las interfaces gráficas de Linux (como Ubuntu y Biolinux) tienen un sistema de archivos que estamos acostumbrados a explorar a través carpetas y subcarpetas que podemos ver en una ventana. Por ejemplo así:

![](finder.png) 

A continuación vamos a ver cómo navegar por este **mismo** sistema de archivos, pero desde la Terminal y con el teclado en vez de desde una ventana y con clicks.

### `pwd`

`pwd` nos da el directorio en donde estamos (viene de print **working directory**). 

El directorio de trabajo es **dónde estamos**, equivalente a tener una ventana abierta del explorador en una carpeta determinada. Al menos que le indiques lo contrario, todo archivo que se genere como parte de la ejecución de un programa se guardará aquí. También este será el lugar donde cualquier programa/script buscará los archivos que le pidas, y NO los encontrará si no están exactamente ahí. Claro que es posible decirle que busque en otro directorio, lo veremos adelante.  

El working directory de base es la carpeta "home" del usuario de la computadora. En mi caso:
```
Toxic-Avenger:~ ToxicAvenger$ pwd
/Users/ToxicAvenger
```

    $ pwd
    /Users/ticatla
 
La diagonal **/** es el símbolo que separa los directorios en niveles jerárquicos. Es decir `ticatla` es un subdirectorio de `Users` que a su vez es un subdirectorio de `root` (simbolizado aquí como una sola /), la raíz de todos los directorios.

### `cd`

`cd` viene de **change directory** y sirve para movernos a otro directorio. Por ejemplo:

```
Toxic-Avenger:~ ToxicAvenger$ cd Documents/
Toxic-Avenger:Documents ToxicAvenger$ cd POSTDOC_/
Toxic-Avenger:POSTDOC_ ToxicAvenger$  
```

**Pregunta:** ¿Qué pasa con el texto antes del nombre de usuario?

Como se explicó antes, el texto antes de `$` nos indica el nombre del equipo, el directorio actual y el nombre del usuario. El directorio actual cambió de "ToxicAvenger" (home) a "Desktop". 

Ahora vamos a navegar al directorio del repositorio. La navegación se puede hacer de diferentes maneras:


Para esto hay varias opciones:

#### Moverse hacia adelante/abajo (i.e. adentro de subdirectorios):

* **Absolute path** que es dar la ruta (dirección) completa **desde root** hasta el directorio que queremos.

* **Relative path** que es dar la ruta **desde donde estamos** hasta el directorio que queremos.

Ejemplo de ruta absoluta:

```
Toxic-Avenger:~ ToxicAvenger$ cd Documents/GitHub/Unidad_1/Prac_Uni1/
Toxic-Avenger:Prac_Uni1 ToxicAvenger$ cd ~
Toxic-Avenger:~ ToxicAvenger$ 

```
Háganlo en sus compus (terminales). Noten que `ToxicAvenger` es **mi** nombre de usuario, entonces el path absoluto tiene que llevar **su nombre de usuario**. Para esto es necesario clonar el repositorio con `git`

`git clone https://github.com/Microfred/CCG_curso.git`

Ahora sí manos a la obra...

Ejemplo de ruta relativa:

```
(base) Toxic-Avenger:~ ToxicAvenger$ cd CCG_curso/
Toxic-Avenger:CCG_curso ToxicAvenger$ ls 
LICENSE			Prac_Uni1		README_practica_1.md
(base) Toxic-Avenger:CCG_curso ToxicAvenger$ cd Prac_Uni1/
(base) Toxic-Avenger:Prac_Uni1 ToxicAvenger$ pwd
/Users/ToxicAvenger/CCG_curso/Prac_Uni1
Toxic-Avenger:Prac_Uni1 ToxicAvenger$ 
Toxic-Avenger:Prac_Uni1 ToxicAvenger$ ls
Maiz		Manzanas	Peras		Tomates
Toxic-Avenger:Prac_Uni1 ToxicAvenger$ cd Maiz/
Toxic-Avenger:Maiz ToxicAvenger$ 
``` 

#### Moverse a home:

`~` es una especie de ruta corta a la ruta absoluta de tu directorio home. No importa dónde estés `cd ~` o `cd $HOME` te llevará a home. 

```
Toxic-Avenger:~ ToxicAvenger$ cd CCG_curso
Toxic-Avenger:Prac_Uni1 ToxicAvenger$ cd ~
Toxic-Avenger:~ ToxicAvenger$ 

Toxic-Avenger:~ ToxicAvenger$ cd Prac_Uni1 ToxicAvenger$ pwd
Toxic-Avenger:Prac_Uni1 ToxicAvenger$ pwd
/Users/ToxicAvenger/CCG_curso/Prac_Uni1
Toxic-Avenger:Prac_Uni1 ToxicAvenger$ cd $HOME
Toxic-Avenger:~ ToxicAvenger$ 
```

#### Moverse para atrás (hacia el directorio raíz):

Igual puede ser con rutas absolutas o relativas, pero utilizando `..` que representa **parent directory**, es decir el directorio arriba (o atrás, como le entiendas mejor):

`cd ..` por lo tanto te lleva a un directorio arriba de donde estés.

Ejemplo:


```

$ pwd
Toxic-Avenger:Prac_Uni1 ToxicAvenger$ cd Maiz/
Toxic-Avenger:Maiz ToxicAvenger$ cd ..
Toxic-Avenger:Prac_Uni1 ToxicAvenger$ cd ..
Toxic-Avenger:Unidad_1 ToxicAvenger$ cd ..
Toxic-Avenger:GitHub ToxicAvenger$

```

#### Moverse para atrás y para adelante en la misma línea

Puedes usar `..` muchas veces. Ojo con incluir `/` para separar niveles. 

Ejemplo:

```
$pwd
/Users/ToxicAvenger/Desktop/GitHub/Unidad_1/Prac_Uni1/Tomates/VerdesFritos
$ cd ../../Manzanas/
$ pwd
/Users/ToxicAvenger/Desktop/GitHub/Unidad_1/Prac_Uni1/Manzanas

```

Es decir `../` se puede combinar con una ruta relativa. Ejemplo:

```
$ pwd
Toxic-Avenger:~ ToxicAvenger$ cd Documents/GitHub/Unidad_1/Prac_Uni1/Tomates/VerdesFritos/
Toxic-Avenger:VerdesFritos ToxicAvenger$ cd ../../Manzanas/
Toxic-Avenger:Manzanas ToxicAvenger$ pwd
/Users/ToxicAvenger/Documents/GitHub/Unidad_1/Prac_Uni1/Manzanas
Toxic-Avenger:Manzanas ToxicAvenger$  
```

#### No moverse
O en otras palabras ir al directorio donde ya estás. Suena inútil, y en general lo es si lo hace con `cd`, pero el concepto es importante para otros comandos que veremos más adelante. 

`cd ./` te lleva al directorio en el que estás. Lo importante a recordar es que `.` significa "el directorio actual". 


#### Errores comunes al usar `cd`


* `-bash: cd: manzanas: No such file or directory`

 ¿Escribiste bien Manzanas? Ups. No. Es Manzanas no manzanas. Ojo con las mayúsculas. También aguas con  los errores de dedo (e.g. Manzaanas arrojaría el mismo error)

* `-bash: cd: ../Manzanas: No such file or directory`


  Sí está bien escrito, el directorio Manzanas existe y no lo encuentra. Ok, existe, pero NO en el directorio inmediatamente arriba. Checa dónde estás y a dónde dirigen tus `cd ..`

* `-bash: cd..: command not found`. 
  
  Ojo, con tus espacios `cd..` no es lo mismo que `cd ..`. Otro clásico es poner `cd ...`


En resumen: checa que esté bien escrito y que puedas ir a ese directorio con la ruta que le estás pidiendo. 

#### Tips de acceso rápido en la Terminal

**Flecha arriba/abajo** para acceder a los últimos comandos utilizados
**TAB** para "completar" la escritura del path o nombre de archivos.


### `ls`

Enlista los archivos y directorios presentes en un directorio. Ejemplo:

```
$ cd Maiz
$ ls
nuevos_final.bed	nuevos_final.fam
nuevos_final.bim	nuevos_final.log
```

Nota que los enlista en orden alfabético. 

Para tener más info de los archivos:

`ls -l` brinda la misma lista, pero con datos sobre: 
si es un directorio (d) o un archivo (-), permisos (si es sólo lectura, editable, etc y por quién, detalles más adelante), número de links al archivo, qué usuario es el dueño, a qué grupo pertenece dicho usuario, tamaño en bytes, fecha-hora en que se modificó y el nombre del directorio o archivo.

Ejemplo:
```
Toxic-Avenger:Prac_Uni1 ToxicAvenger$ cd Maiz/
Toxic-Avenger:Maiz ToxicAvenger$ ls
nuevos_final.bed	nuevos_final.bim	nuevos_final.fam	nuevos_final.log
Toxic-Avenger:Maiz ToxicAvenger$ ls -l
total 5216
-rw-r--r--  1 ToxicAvenger  staff  1551105 Feb  2 22:00 nuevos_final.bed
-rw-r--r--  1 ToxicAvenger  staff  1109078 Feb  2 22:00 nuevos_final.bim
-rw-r--r--  1 ToxicAvenger  staff     3604 Feb  2 22:00 nuevos_final.fam
-rw-r--r--  1 ToxicAvenger  staff     1825 Feb  2 22:00 nuevos_final.log
```


Pero se pueden ordenar por fecha (y hora, aunque no se vea) de modificación, por ejemplo:

```
Toxic-Avenger:Maiz ToxicAvenger$ ls -lt
total 5216
-rw-r--r--  1 ToxicAvenger  staff     1825 Feb  2 22:00 nuevos_final.log
-rw-r--r--  1 ToxicAvenger  staff     3604 Feb  2 22:00 nuevos_final.fam
-rw-r--r--  1 ToxicAvenger  staff  1109078 Feb  2 22:00 nuevos_final.bim
-rw-r--r--  1 ToxicAvenger  staff  1551105 Feb  2 22:00 nuevos_final.bed
Toxic-Avenger:Maiz ToxicAvenger$ 
``` 


`man ls` abre el manual de `ls` (**o de cualquier otro comando**), donde vienen muchas más opciones para usar este comando.

**Tip**: presiona "q" para salir de la pantalla de `man`. 

**Ejercicio**:
* Enlista el contenido de `Maiz` por tamaño del archivo y has que el tamaño del archivo se lea en KB y MB (ie reducido en vez de todos los bytes).

### `mkdir`

Crea un directorio. 

```
$ mkdir Prueba
$ ls
Prueba			nuevos_final.bim	nuevos_final.log
nuevos_final.bed	nuevos_final.fam
```

Nota: Se puede combinar con paths absolutos o relativos para crearlo en un directorio diferente al WD.


**Ejercicio:** ¿Qué pasa si intentas crear un directorio que ya existe? ¿Para qué sirve el flag `-p`?


### `cp`

Copia un archivo o directorio de lugar A a lugar B.

```
$ cp -r Prueba ../
$ ls ../
Maiz		Manzanas	Peras		Prueba		Tomates
```

¿Por qué utilicé el flag `-r` en el ejemplo anterior?


### `mv`

Mueve un archivo o directorio de lugar A a lugar B. Equivalente a "cut-paste".

```
$ mv ../Prueba ../Manzanas
$ ls ../
Maiz		Manzanas	Peras		Tomates
$ ls ../Manzanas
Prueba

```

Nota que con `mv` no es necesario utilizar `-r` para borrar directorios.


### `rm`

Borra (**AGUAS al usar esto**) archivos o directorios.

```
$ rm -r Prueba
$ rm -r ../Manzanas/Prueba
```

**Pregunta:** ¿Si borras un directorio se borra su contenido? 


### `tar`

Es un método de ultra comprensión (más que zip) utilizado por sistemas Linux/Unix. Viene de "*tape archive*" y originalmente surgió para comprimir archivos para los discos "tape" de respaldo. 

La compresión tar genera archivos "tarball", gzip y bzip. Con terminaciones como `.tar.gz`. Este tipo de compresión es muy utilizada en datos genómicos.

#### Crear un tar.gz

Imaginemos que queremos comprimir la carpeta `Maiz`

```
Toxic-Avenger:Prac_Uni1 ToxicAvenger$ ls
Maiz		Manzanas	Peras		Tomates
Toxic-Avenger:Prac_Uni1 ToxicAvenger$ tar cvzf Maiz.tar.gz Maiz
a Maiz
a Maiz/nuevos_final.log
a Maiz/nuevos_final.bim
a Maiz/nuevos_final.bed
a Maiz/nuevos_final.fam
Toxic-Avenger:Prac_Uni1 ToxicAvenger$ ls
Maiz		Maiz.tar.gz	Manzanas	Peras		Tomates
Toxic-Avenger:Prac_Uni1 ToxicAvenger$ ls -lhS
total 2536
-rw-r--r--  1 ToxicAvenger  staff   1.2M Feb  3 16:26 Maiz.tar.gz
drwxr-xr-x  7 ToxicAvenger  staff   224B Feb  3 15:43 Tomates
drwxr-xr-x  6 ToxicAvenger  staff   192B Feb  2 22:00 Maiz
drwxr-xr-x  3 ToxicAvenger  staff    96B Feb  2 22:00 Manzanas
drwxr-xr-x  3 ToxicAvenger  staff    96B Feb  2 22:00 Peras
Toxic-Avenger:Prac_Uni1 ToxicAvenger$ 
```
¿Qué hacen los flags de `tar` que utilizamos?

`c`  Crea un nuevo archivo .tar.

`v`  Muestra "*Verbosely*" el progreso de la compresión.

`z`  Especifica que queremos un `.gzip`.

`f`  Nombre del archivo tar que queremos como resultado.

#### Descomprimir (Untar) archivos .tar.gz

```
$ rm -r Maiz
$ tar -xvf Maiz.tar.gz
Maiz/
Maiz/.DS_Store
Maiz/nuevos_final.bed
Maiz/nuevos_final.bim
Maiz/nuevos_final.fam
Maiz/nuevos_final.log
$ ls
Maiz		Maiz.tar.gz	Manzanas	Peras		Tomates
```

**Pregunta:** ¿Qué hacen las flags `-xvf`?

#### Ver el contenido de un archivo tar SIN descomprimirlo

```
Toxic-Avenger:Prac_Uni1 ToxicAvenger$ tar -tvf Maiz.tar.gz
drwxr-xr-x  0 ToxicAvenger staff       0 Feb  2 22:00 Maiz/
-rw-r--r--  0 ToxicAvenger staff    1825 Feb  2 22:00 Maiz/nuevos_final.log
-rw-r--r--  0 ToxicAvenger staff 1109078 Feb  2 22:00 Maiz/nuevos_final.bim
-rw-r--r--  0 ToxicAvenger staff 1551105 Feb  2 22:00 Maiz/nuevos_final.bed
-rw-r--r--  0 ToxicAvenger staff    3604 Feb  2 22:00 Maiz/nuevos_final.fam
Toxic-Avenger:Prac_Uni1 ToxicAvenger$ 

```
**Pregunta:** ¿En qué situación puede ser útil ver el contenido de un tar sin descomprimirlo?

[Aquí una guía con más opciones para usar `tar`](http://www.tecmint.com/18-tar-command-examples-in-linux/)

`tar` tiene muchas opciones, lo importante es saber que existen y cómo buscarlas en el manual. Casi siempre:

![](tar_xkcd.png)

### Crear archivos desde la terminal

Es posible crear archivos de texto directamente desde la terminal utilizando programas como `vi` y `nano` o el comando `touch`. 


Touch solo crea un archivo sin contenido. Ejemplo :

```
$ cd Maiz
$ touch prueba
$ ls 
nuevos_final.bed	nuevos_final.fam	prueba
nuevos_final.bim	nuevos_final.log
$ rm prueba
```

## curl

`curl` Sirve para bajar archivos de internet a la computadora.

Sintaxis:

    curl [opciones] [direccionURLdelarchivo]


Ejemplo, podemos bajar el archivo de texto del README que vive en el repositorio de esta clase:


```
$ curl -s "https://github.com/Microfred/IntroBioinfo/edit/main/README.md"
# Introducción a la bioinformática e investigación reproducible para análisis genéticos

Este es el repositorio de apuntes y código del curso **Introducción a la bioinformática e investigación reproducible para análisis genéticos** [...]
```

O bajar sencuencias de ADN de GeneBank! ([instrucciones de cómo construir la url aquí](http://www.ncbi.nlm.nih.gov/books/NBK25499/#chapter4.EFetch))


```
$ curl -s "https://eutils.ncbi.nlm.nih.gov/entrez/eutils/efetch.fcgi?db=nucleotide&rettype=fasta&id=AB080944.1"
>AB080944.1 Pinus patula chloroplast matK gene for maturase, complete cds
ATGGATGAGTTCCATAGATGCGGAAAGGAAGATAGCTTTTGGCAACAATGCTTTTTATATCCACTCTTTT
TTCAGGAAGATCTTTACGCAATTTCTCATGATCATTATTTGGATGTATCAAGTTCCTCCAGACCGATGGA
ACATTTAAGTTCCAATGATCAATTAAGTTTCCTAACTGTAAAACGTTTGATTGGTCAAATACGTCAACAA
AATCATTCAATTGTTTTATTCGTGAATTGCGATCCAAATCCATTAGCTGATCGCAAGAAGAGTTTCTATT
CTGAATCGGTACTAGAAGCACTTACATTGGTCCTGGAAGTTCCGTTCTCTATATGGTCAAAATATTCTGT
GGAAGGGATGAATGAATCGAAGAGTTTCCGGTCGATCCATTCAATATTTCCCTTCTTAGAGGATAAATTC
CCGCATTCAAATTCTATATTAGATGCACGAATACCCTATTCTATTCATCCGGAAATTTTGGTTCGAACCT
TTCGTCGCTGGATCCGAGATGCTCCCTCCTTGCACCCATTACGATCTGTTCTCTATGAATATAGAAATAG
TCCAGATAATTTACAAAGATCAATTATTGTCGTCCCAAGAGTAAATACGAGATTCTTCCTGTTCCTGTGG
AATTATTATGTCTGTGAATGCGAATCCATTTTATTTTCCCGTCTTAAACGATCCTCTCATTCACGATCGT
TGACTCATGGATCTTTCCCTCAGCGAACTCATTTTCATCGAAAGATAAAACATATTATCATATTTTCTCG
TCGAAATTCACTGAAAAGTATCTGGTCGTTGAAGGATCCTAAAATTCACTATGTTAGATATGGCGAAAGA
CCTATTATAGCTATAAAGGGTGCTCATCTCCTAGTTAAAAAATGTAGATATTATCTTCTAATTTTTCGGC
AATTTTATTTCCATCTTTGGTCCGAACCGTATAGGGTCTGTTCTCATCAATTATCCAAGAATTGTTCTTC
TTCTCCAGGTTATTTTTTGAGGGTTCGGATGAACCCTATTTTGGTCAGAACCAAAATGCTCGATGAGTTA
TTCATCGCCGATCTTATTACCGATGAAATTGATCCAATAGTTCCGATTGTACCAATAATTGGATTATTGG
CTACAGAAAAATTCTGTGACATATCAGGGCGGCCAATTAGTAAATTGTCTTGGACCAGTCTAACAGATGA
TGATATCCTCGATCGATTCGATCAAATTTGGAGAAATCTTTTTCATTACTACAGTGGATCCTTTGATCGA
GATGGTTTATATCGTATAAAGTATATACTTTCATTATCATGTGCTAAAACTTTAGCCTGTAAACATAAAA
GTACGATACGTGTAGTTCGGAAGGAATTAGGTCCAGAACTCTTTAAAAAATCGTTTTCAAAAGAACGAGA
ATTTTATTCTCTGCGCTTTTCATCAAAAGCGGCGGCCCGTTCGCAGAGAGAACGAATTTGGCATTCAGAT
ATTTCCCAGATAAATCCCCTAGCTAATTCCTGGCAAAAGATACAGGATCTGAAAATAGAAAACTTATTTG
ACCAATGAAATGCTCTTTGAGTAATTGCCTCGATTCAGAATCATTTTTATTTTTCTATCCGAGAACTAAA
ATGATTAGGAAATAGATACATTACATGGGGAAAGCCGTGTGCAATGAGAAT
```

En bioinformática `curl` se utiliza para transferir desde archivos FASTA de secuencias individuales de GeneBank hasta genomas completos.

Nota:
`wget` hace algo parecido a `curl`, pero lo salva a un archivo directamente. No existe de base en Mac, pero es posible instalarlo.

Más info:

* Cómo bajar archivos de GeneBank utilizando e-utils (ejemplo anterior): [http://www.ncbi.nlm.nih.gov/books/NBK25499/#chapter4.EFetch](http://www.ncbi.nlm.nih.gov/books/NBK25499/#chapter4.EFetch)

* Truco para bajar varios metagenomas (o genomas, secuencias, etc) en una sola línea de código [https://www.biostars.org/p/94875/](https://www.biostars.org/p/94875/)

* Excelente explicación más profunda de `curl` y `wget` en el Capítulo 6 de Buffalo V (2015) Bioinformatics data skills.

### Comodines o el uso de `*` `?` `[]` `{}`

Volvamos a ver el contenido de Maiz:

```
$ cd Maiz
$ ls
ejemplonano.txt		nuevos_final.bim	nuevos_final.log
nuevos_final.bed	nuevos_final.fam
```

**Ejercicio**: Necesitamos crear más archivos .bed y .fam para los ejemplos de abajo. Queremos qué se llamen `ejemplo_final.bed` y `ejemplo_final.fam`. ¿Cómo hacerlo?


El resultado del ejercicio anterior es:

```
$ ls
ejemplo_final.bed	nuevos_final.bed	nuevos_final.log
ejemplo_final.fam	nuevos_final.bim
ejemplonano.txt		nuevos_final.fam
```

Fácilmente podemos ver que hay 6 archivos, y que hay dos que terminan en .bed y dos que terminan en .fam.


¿Y si tuviéramos 1,000 archivos con las terminaciones .bed, .fam, .bim pero con diferente prefijo? ¿Cómo contarlos y ver cuántos .bed hay?

### `*`

"Comodín" o *wildcard*. Cualquier texto (uno o más caracteres) a partir (derecha o izquierda) de dónde se ponga el `*`.

Ejemplo:

```
$ ls *.bed
ejemplo_final.bed	nuevos_final.bed
$ ls nuevos*
nuevos_final.bed	nuevos_final.fam
nuevos_final.bim	nuevos_final.log

```


### `?`
Parecido a ´*´ pero para un sólo carácter.

```
$ ls *.b??
ejemplo_final.bed	nuevos_final.bed	nuevos_final.bim
```

### `[]`

Para agrupar términos de búsqueda. Por ejemplo letras [a-z]

```
$ ls [a-z]*.bed
ejemplo_final.bed	nuevos_final.bed
```

Hay más comodines, puedes explorarlos [aquí](http://tldp.org/LDP/GNU-Linux-Tools-Summary/html/x11655.htm).



## Funciones básicas de exploración de archivos con bash

### `more`

Nos permite ver el archivo una línea (flecha abajo) o página a la vez (barra espaciadora). Para salir: `q`

```
$ more nuevos_final.fam
1 maiz_3 0 0 0 -9
2 maiz_68 0 0 0 -9
3 maiz_91 0 0 0 -9
4 maiz_39 0 0 0 -9
5 maiz_12 0 0 0 -9
6 maiz_41 0 0 0 -9
7 maiz_35 0 0 0 -9
8 maiz_58 0 0 0 -9
9 maiz_51 0 0 0 -9
10 maiz_82 0 0 0 -9
11 maiz_67 0 0 0 -9
12 maiz_93 0 0 0 -9
13 maiz_21 0 0 0 -9
14 maiz_6 0 0 0 -9
15 maiz_101 0 0 0 -9
16 maiz_27 0 0 0 -9
17 maiz_43 0 0 0 -9
18 maiz_1 0 0 0 -9
19 maiz_33 0 0 0 -9
20 maiz_100 0 0 0 -9
21 maiz_24 0 0 0 -9
22 maiz_103 0 0 0 -9
23 maiz_72 0 0 0 -9
24 maiz_10 0 0 0 -9
25 maiz_28 0 0 0 -9
26 maiz_49 0 0 0 -9
27 maiz_56 0 0 0 -9
28 maiz_66 0 0 0 -9
29 maiz_52 0 0 0 -9
nuevos_final.fam
```

(puedes salir con `q` si no quieres escrolear (yes, esa palabra no existe en español) todo el archivo para abajo)
[Scroll](https://es.wikipedia.org/wiki/Scroll)

### `less`
Igual que `more` pero se desarrolló más recientemente y puede abrir archivos binarios y otras cosas raras. Juego de palabras con que *less is more*. Pum pum. Se recomienda usar `less` en la vida.

Dentro de `less` (y `more`) podemos escribir `/` y luego texto, mismo que será buscando dentro del archivo.

**Ejercicio**: En el archivo que estamos viendo hay unas muestras de teocintles cuyos nombres empiezan con "teos". ¿En qué líneas del documento están?


### `head`

Muestra las primeras líneas de un archivo (default 10).

```
$ head nuevos_final.fam
1 maiz_3 0 0 0 -9
2 maiz_68 0 0 0 -9
3 maiz_91 0 0 0 -9
4 maiz_39 0 0 0 -9
5 maiz_12 0 0 0 -9
6 maiz_41 0 0 0 -9
7 maiz_35 0 0 0 -9
8 maiz_58 0 0 0 -9
9 maiz_51 0 0 0 -9
10 maiz_82 0 0 0 -9
```

### `tail`

Muestra las últimas líneas de un archivo.

**Pregunta:** ¿Para qué podría ser útil ver las últimas líneas de un archivo?

### `wc`
Brinda el número de líneas, el número de palabras y el número de caracteres del archivo.

```
$ wc nuevos_final.fam
     165     990    3604 nuevos_final.fam
```

### `cat`

Viene de *Concatenate*. Sirve para unir uno detrás de otro varios archivos, o para imprimir todo el contendio de un archivo a la consola.

```
$ cat nuevos_final.fam *log
1 maiz_3 0 0 0 -9
2 maiz_68 0 0 0 -9
3 maiz_91 0 0 0 -9
4 maiz_39 0 0 0 -9
5 maiz_12 0 0 0 -9
6 maiz_41 0 0 0 -9
7 maiz_35 0 0 0 -9
8 maiz_58 0 0 0 -9
9 maiz_51 0 0 0 -9
10 maiz_82 0 0 0 -9
11 maiz_67 0 0 0 -9
12 maiz_93 0 0 0 -9
13 maiz_21 0 0 0 -9
14 maiz_6 0 0 0 -9
15 maiz_101 0 0 0 -9
16 maiz_27 0 0 0 -9
17 maiz_43 0 0 0 -9
18 maiz_1 0 0 0 -9
19 maiz_33 0 0 0 -9
20 maiz_100 0 0 0 -9
21 maiz_24 0 0 0 -9
22 maiz_103 0 0 0 -9
23 maiz_72 0 0 0 -9
24 maiz_10 0 0 0 -9
25 maiz_28 0 0 0 -9
26 maiz_49 0 0 0 -9
27 maiz_56 0 0 0 -9
28 maiz_66 0 0 0 -9
29 maiz_52 0 0 0 -9
30 maiz_47 0 0 0 -9
31 maiz_80 0 0 0 -9
32 maiz_65 0 0 0 -9
33 maiz_94 0 0 0 -9
34 maiz_36 0 0 0 -9
35 maiz_26 0 0 0 -9
36 maiz_105 0 0 0 -9
37 maiz_30 0 0 0 -9
38 maiz_16 0 0 0 -9
39 maiz_42 0 0 0 -9
40 maiz_4 0 0 0 -9
41 maiz_31 0 0 0 -9
42 maiz_17 0 0 0 -9
43 maiz_46 0 0 0 -9
44 maiz_5 0 0 0 -9
45 maiz_32 0 0 0 -9
46 maiz_19 0 0 0 -9
47 maiz_50 0 0 0 -9
48 maiz_8 0 0 0 -9
49 maiz_34 0 0 0 -9
50 maiz_23 0 0 0 -9
51 maiz_54 0 0 0 -9
52 maiz_14 0 0 0 -9
53 maiz_37 0 0 0 -9
54 maiz_25 0 0 0 -9
55 maiz_55 0 0 0 -9
56 maiz_40 0 0 0 -9
57 maiz_29 0 0 0 -9
58 maiz_60 0 0 0 -9
59 maiz_44 0 0 0 -9
60 maiz_74 0 0 0 -9
61 maiz_89 0 0 0 -9
62 maiz_64 0 0 0 -9
63 maiz_83 0 0 0 -9
64 maiz_75 0 0 0 -9
65 maiz_92 0 0 0 -9
66 maiz_69 0 0 0 -9
67 maiz_84 0 0 0 -9
68 maiz_76 0 0 0 -9
69 maiz_97 0 0 0 -9
70 maiz_70 0 0 0 -9
71 maiz_85 0 0 0 -9
72 maiz_77 0 0 0 -9
73 maiz_71 0 0 0 -9
74 maiz_86 0 0 0 -9
75 maiz_78 0 0 0 -9
76 maiz_102 0 0 0 -9
77 maiz_73 0 0 0 -9
78 maiz_88 0 0 0 -9
79 maiz_79 0 0 0 -9
80 maiz_106 0 0 0 -9
81 maiz_119 0 0 0 -9
82 maiz_148 0 0 0 -9
83 maiz_108 0 0 0 -9
84 maiz_120 0 0 0 -9
85 maiz_151 0 0 0 -9
86 maiz_134 0 0 0 -9
87 maiz_123 0 0 0 -9
88 maiz_153 0 0 0 -9
89 maiz_135 0 0 0 -9
90 maiz_124 0 0 0 -9
91 maiz_184 0 0 0 -9
92 maiz_140 0 0 0 -9
93 maiz_125 0 0 0 -9
94 maiz_141 0 0 0 -9
95 maiz_131 0 0 0 -9
96 maiz_189 0 0 0 -9
97 maiz_57 0 0 0 -9
98 maiz_126 0 0 0 -9
99 maiz_113 0 0 0 -9
100 maiz_138 0 0 0 -9
101 maiz_63 0 0 0 -9
102 maiz_127 0 0 0 -9
103 maiz_114 0 0 0 -9
104 maiz_139 0 0 0 -9
105 maiz_99 0 0 0 -9
106 maiz_129 0 0 0 -9
107 maiz_116 0 0 0 -9
108 maiz_142 0 0 0 -9
109 maiz_110 0 0 0 -9
110 maiz_132 0 0 0 -9
111 maiz_118 0 0 0 -9
112 maiz_144 0 0 0 -9
113 maiz_133 0 0 0 -9
114 maiz_121 0 0 0 -9
115 maiz_111 0 0 0 -9
116 maiz_137 0 0 0 -9
117 maiz_109 0 0 0 -9
118 maiz_146 0 0 0 -9
119 maiz_164 0 0 0 -9
120 maiz_157 0 0 0 -9
121 maiz_171 0 0 0 -9
122 maiz_149 0 0 0 -9
123 maiz_165 0 0 0 -9
124 maiz_159 0 0 0 -9
125 maiz_172 0 0 0 -9
126 maiz_150 0 0 0 -9
127 maiz_166 0 0 0 -9
128 maiz_160 0 0 0 -9
129 maiz_173 0 0 0 -9
130 maiz_152 0 0 0 -9
131 maiz_167 0 0 0 -9
132 maiz_161 0 0 0 -9
133 maiz_174 0 0 0 -9
134 maiz_154 0 0 0 -9
135 maiz_169 0 0 0 -9
136 maiz_162 0 0 0 -9
137 maiz_176 0 0 0 -9
138 maiz_156 0 0 0 -9
139 maiz_170 0 0 0 -9
140 maiz_163 0 0 0 -9
141 maiz_177 0 0 0 -9
142 maiz_178 0 0 0 -9
143 maiz_192 0 0 0 -9
144 maiz_185 0 0 0 -9
145 maiz_201 0 0 0 -9
146 maiz_179 0 0 0 -9
147 maiz_193 0 0 0 -9
148 maiz_186 0 0 0 -9
149 maiz_202 0 0 0 -9
150 maiz_180 0 0 0 -9
151 maiz_195 0 0 0 -9
152 maiz_187 0 0 0 -9
153 maiz_181 0 0 0 -9
155 maiz_197 0 0 0 -9
156 maiz_188 0 0 0 -9
157 maiz_182 0 0 0 -9
158 maiz_198 0 0 0 -9
159 maiz_190 0 0 0 -9
160 maiz_200 0 0 0 -9
161 maiz_183 0 0 0 -9
162 maiz_191 0 0 0 -9
163 teos_96 0 0 0 -9
164 teos_203 0 0 0 -9
163 teos_911 0 0 0 -9
164 teos_9107 0 0 0 -9

@----------------------------------------------------------@
|        PLINK!       |     v1.07      |   10/Aug/2009     |
|----------------------------------------------------------|
|  (C) 2009 Shaun Purcell, GNU General Public License, v2  |
|----------------------------------------------------------|
|  For documentation, citation & bug-report instructions:  |
|        http://pngu.mgh.harvard.edu/purcell/plink/        |
@----------------------------------------------------------@

Web-based version check ( --noweb to skip )
Recent cached web-check found... OK, v1.07 is current

+++ PLINK 1.9 is now available! See above website for details +++

Writing this text to log file [ nuevos_final.log ]
Analysis started: Wed May 06 12:19:25 2015

Options in effect:
	--file nuevos_final
	--out nuevos_final
	--recodeA

36931 (of 36931) markers to be included from [ nuevos_final.map ]
Warning, found 165 individuals with ambiguous sex codes
Writing list of these individuals to [ nuevos_final.nosex ]
165 individuals read from [ nuevos_final.ped ]
0 individuals with nonmissing phenotypes
Assuming a disease phenotype (1=unaff, 2=aff, 0=miss)
Missing phenotype value is also -9
0 cases, 0 controls and 165 missing
0 males, 0 females, and 165 of unspecified sex
Before frequency and genotyping pruning, there are 36931 SNPs
165 founders and 0 non-founders found
Total genotyping rate in remaining individuals is 0.990151
0 SNPs failed missingness test ( GENO > 1 )
0 SNPs failed frequency test ( MAF < 0 )
After frequency and genotyping pruning, there are 36931 SNPs
After filtering, 0 cases, 0 controls and 165 missing
After filtering, 0 males, 0 females, and 165 of unspecified sex
Writing recoded file to [ nuevos_final.raw ]

Analysis finished: Wed May 06 12:19:30 2015
```

Es decir, básicamente es como copiar-pegar un archivo al final de otro.

También podemos crear un archivo nuevo:

`cat > file_new.txt`
¿cómo vemos el contenido de ese archivo? ...

... añadir información a un archivo:

`cat >> file_new.txt`
Hello world!

### etc...


**Ejercicio** ¿Cómo concatenar tres o más archivos a la vez?


**Pregunta:** ¿Y si quisiéramos tener el resultado en un archivo nuevo?

Más detalles y otras formas de redireccionar (que ocupan algunos programas) las puedes encontrar aquí [https://www.tutorialspoint.com/unix/unix-io-redirections.htm](https://www.tutorialspoint.com/unix/unix-io-redirections.htm)

### Regular expressions y búsqueda de patrones (`grep`)

Las expresiones regulares son las grandes olvidadas, no se utilizan mucho, pero cuando te toca utilizarlas lamentas no conocerlas más.

#### ¿Qué son las expresiones regulares
Las *expresiones regulares* son una herramienta de búsqueda o búsqueda-remplazo de cadenas de texto acorde a un patrón dado. Existen en la línea de comando, pero también en otros lenguajes, como R y casi cualquier buscador de texto.

Una expresión regular se puede pensar como una combinación de caracteres literales y metacaracteres.

* Los **caracteres literales** son de los que están formadas las **palabras en el lenguaje utilizado**. Ejemplo: "c",""o","n","a","b","i","o","2","0","6"

* Los **metacaracteres** son aquellos que tienen una **función particular en la expresión regular**. Ejemplo:  "*","?",".","|","^","$","(",")","[","]"

Las expresiones regulares también se conocen como *regexp*, *regex* o `grep` (global regular expression print), que es el comando que utilizaremos. Pero en realidad `grep` solo es uno de los comandos que las utiliza, es decir hay otros.

#### ¿Para qué sirven?

Las principales aplicaciones de las expresiones regulares en bioinformática son:

* Reformatear archivos de datos. **Una se la vive haciendo esto**
* Decirle a un algoritmo que realice análisis en ciertas muestras y no otras
* Identificar patrones cortos de ADN en una secuencia, por ejemplo enzimas de restricción o índices.


#### ¿Cómo utilizar expresiones regulares en la línea de comando?

El comando `grep` busca dentro de uno o más archivos las líneas que contengan una expresión regular dada y copia dicha línea al stdout (o hace algo con ese output, si se lo indicamos).

`grep [options] [regularexpression] [filename]`

Las opciones de grep pueden verse en el manual (**Pregunta** ¿Cómo buscar el manual de `grep` en la Terminal?). Veremos los casos más usados adelante.

La *regularexpression* puede ser tal cual el texto a buscar, pero también podemos hacer una búsqueda mucho más compleja con **operadores**, **cuantificadores**, y **posicionadores**, que de forma similar a las *wildcards* nos permiten realizar búsquedas más flexibles.

##### Operadores

* **.**  Cualquier símbolo (una vez)

* **[....]**  Para hacer una lista de caracteres, por ejemplo [Bb]iology10[1234] acepta cualquiera de las cadenas "Biology102", "biology101". También se pueden incluir rangos, por ejemplo: [0-9] para todos los números.

* **[^...]** Para hacer una lista de caracteres negativos, o sea que busque cualquiera excepto los enlistados.

* **\w** Cualquier "caracter de palabra", ie: letras, números y _.
* **\W** Cualquier "caracter de NO palabra", ie: símbolos raros que no son letras, números ni _.

* **\\**  Sirve para usar los metacaracteres ($ * + . ? [ ] ^ { } | ( ) \) como caracteres literales. Por ejemplo \\$3 para el string \$3. A esto se le conoce como "escapar" (*escape*). Experto y además un [juego](https://www.therobinlord.com/projects/slash-escape) para aprender mucho más de escape y *RegEx*

* **|**  Operador "or" acepta un patrón u otro, por ejemplo p(err|at)o va a aceptar tanto "perro" como "pato".

* **(....)**  Grupos, sirven para recuperar partes del patrón encontrado para ser usadas después

##### Cuantificadores

* __*__ Cero o más ocurrencias del caracter anterior, por ejemplo 10\*, va a aceptar las cadenas "1", "10", "100", "1000", etc

* **+**  Una o más ocurrencias del caracter anterior, por ejemplo 10+, va a aceptar las cadenas 10", "100", "1000", etc, pero no la cadena "1"

* **?**  Hasta una ocurrencia del caracter anterior, por ejemplo patos?, va aceptar las cadenas "pato" y "patos"

* **{n}**  Exactamente n veces el caracter anterior, por ejemplo 10{5}, únicamente va a aceptar la cadena "100000"

* **{n,}**  Mínimo n veces el caracter anterior, por ejemplo 10{5,}, aceptará las cadenas "100000", "1000000", "1000000", etc

* **{n,m}**  Entre n y m veces el caracter anterior, por ejemplo 10{2,5}, aceptará las cadenas "100", "10000"

##### Posicionadores
* **<** Inicio de la cadena (palabra), por ejemplo <GAAA aceptará "GAAACCCTTT", pero no "CCCTGAAAC"

* **>** Fin de la cadena, por ejemplo TCCA> aceptará "ACTTCCA" pero no "AGTCCATC"

* **^** Igual que los anteriores, pero para el inicio de una línea

* **$** Final de una línea



### Usos comunes de `grep`

Empecemos por ver el archivo `tomatesverdes.fasta` (Vive en: `/Unidad_1/Prac_Uni1/Tomates`)

```
$ less tomatesverdes.fasta
>gi|156629013|gb|EF438954.1| Physalis philadelphica isolate P061 maturase K (matK) gene, partial cds; chloroplast
TAGGTCGATTTTGTTGGAAAATCCAGGTTATAACAATAAATTTAGTTTCCTAATTGTGAAACGTTTAATT
ACTCGAATGTATCAACAGAATCATTTTATTATTTCTACTAATGATTCTAACAAAAATCCATTTTTGGGGT
GCAACAAGAGTTTGTATTCTCAAATGATATCAGAGGGATTTGCATTTATTGTGGAAATTCCGTTTTCTCT
ACGATTAATATCTTCTTTATCTTCTTTCGAAGGCAAAAAGATTTTAAAATCTCATAATTTACGATCAATT
CATTCAACATTTCCTTTTTTAGAGGACAATTTTTCACATCTAAATTATGTATTAGATATACTAATACCCT
ACCCCGTTCATCTGGAAATCTTGGTTCAAACTCTTCGCTATTGGGTAAAAGATGCCTCTTCTTTACATTT
ATTACGATTCTTTCTCCACGAATATTGGAATTTGAATAGTCTTATTACTTCAAAGAAGCCCGGTTACTCC
TTTTCAAAAAAAAATCAAAGATTCTTCTTCTTCTTATATAATTCTTATGTATATGAATGGGAATCCACTT
TCGTCTTTCTACGGAACCAATCTTCTCATTTACGATCAACATCTTTTGGAGCCCTTCTTGAACGAATATA
TTTCTATGGAAAAATAGAACGTCTTGTAGAAGTCTTTGCTAAGGATTTTCAGGTTACCTTATGGTTATTC
AAGGATCCTTTCATGCATTATGTTAGGTATCAAGGAAAATCAATTCTGGCTTCAAAAGGGACGTTTCTTT
TGATGAATAATTGGAAATTTTACCTAGTGGATTTTTGGCACTGTCATTTTTTTCGGTGCTTTCACTCATG
TAGGATCCTTATAAACCAATTGGCCAATCATTTACGTGACTTTCTGGGCTATCTTTCAAGTGTGCGGCTA
AATCTTTCAATGGTTCGTAGAAAA
>gi|156629009|gb|EF438952.1| Physalis philadelphica isolate P059 maturase K (matK) gene, partial cds; chloroplast
TAGGTCGATTTTGTTGGAAAATCCAGGTTATAACAATAAATTTAGTTTCCTAATTGTGAAACGTTTAATT
ACTCGAATGTATCAACAGAATCATTTTATTATTTCTACTAATGATTCTAACAAAAATCCATTTTTGGGGT
GCAACAAGAGTTTGTATTCTCAAATGATATCAGAGGGATTTGCATTTATTGTGGAAATTCCGTTTTCTCT
ACGATTAATATCTTCTTTATCTTCTTTCGAAGGCAAAAAGATTTTAAAATCTCATAATTTACGATCAATT
CATTCAACATTTCCTTTTTTAGAGGACAATTTTTCACATCTAAATTATGTATTAGATATACTAATACCCT
ACCCCGTTCATCTGGAAATCTTGGTTCAAACTCTTCGCTATTGGGTAAAAGATGCCTCTTCTTTACATTT
ATTACGATTCTTTCTCCACGAATATTGGAATTTGAATAGTCTTATTACTTCAAAGAAGCCCGGTTACTCC
TTTTCAAAAAAAAATCAAAGATTCTTCTTCTTCTTATATAATTCTTATGTATATGAATGGGAATCCACTT
TCGTCTTTCTACGGAACCAATCTTCTCATTTACGATCAACATCTTTTGGAGCCCTTCTTGAACGAATATA
TTTCTATGGAAAAATAGAACGTCTTGTAGAAGTCTTTGCTAAGGATTTTCAGGTTACCTTATGGTTATTC
AAGGATCCTTTCATGCATTATGTTAGGTATCAAGGAAAATCAATTCTGGCTTCAAAAGGGACGTTTCTTT
TGATGAATAAATGGAAATTTTACCTTGTCAATTTTTGTCAATGTCATTTTTTTCTGTGCTTTCACACAGG
AAGGATCCATATAAACCAATTATCCAATCATTTACGTGACTTTATGGGCTATCTTTCAAGTGTGCGACTA
AATCATTCAATGGTACGTAGTCAAATGTTAGAAAA
:
```

**Preguntas:**

1) ¿Qué tipo de archivo es?

2) ¿Cuántas secuencias contiene?

3) ¿Cuál es el encabezado de las secuencias?

`grep` puede permitirnos extraer información de archivos como este, pero mucho más grandes y difíciles de ver.

Formas comunes de usar `grep`:

#### `grep` a secas:
Busca una expresión regular y otorga las líneas donde se encontró dicha expresión.

Ejemplo:

```
$ grep ">" tomatesverdes.fasta
>gi|156629013|gb|EF438954.1| Physalis philadelphica isolate P061 maturase K (matK) gene, partial cds; chloroplast
>gi|156629009|gb|EF438952.1| Physalis philadelphica isolate P059 maturase K (matK) gene, partial cds; chloroplast
>gi|156628921|gb|EF438908.1| Physalis philadelphica isolate P056 maturase K (matK) gene, partial cds; chloroplast
>gi|156628893|gb|EF438894.1| Physalis philadelphica isolate P050 maturase K (matK) gene, partial cds; chloroplast
>gi|156629011|gb|EF438953.1| Physalis philadelphica isolate P060 maturase K (matK) gene, partial cds; chloroplast
```
**Pregunta**: ¿Por qué está ">" entre comillas?

**Ejercicio** En el mismo directorio hay otro archivo fasta. Utiliza `grep` y algo más para ver el encabezado de `tomatesverdes.fasta` y `jitomate.fasta`. ¿Qué diferencia hay con el output anterior?


#### `grep -c`
Para contar en cuántas líneas aparece la expresión de búsqueda

```
$ grep -c ">" tomatesverdes.fasta
5
```

#### `grep -l`
Sólo enlista los archivos donde se encontró la expresión, pero no las líneas.

```
$ grep -l Physalis *.fasta
tomatesverdes.fasta

```

#### `grep -i`
Hace que la búsqueda sea **insensible** a Mayúsculas/minúsculas.

```
$ grep -l physalis *.fasta
$
$ grep -li physalis *.fasta
tomatesverdes.fasta

```

#### `grep -w`
Sirve para buscar palabras completas, por ejemplo para buscar "he" y no "the".

```
$ grep iso tomatesverdes.fasta
>gi|156629013|gb|EF438954.1| Physalis philadelphica isolate P061 maturase K (matK) gene, partial cds; chloroplast
>gi|156629009|gb|EF438952.1| Physalis philadelphica isolate P059 maturase K (matK) gene, partial cds; chloroplast
>gi|156628921|gb|EF438908.1| Physalis philadelphica isolate P056 maturase K (matK) gene, partial cds; chloroplast
>gi|156628893|gb|EF438894.1| Physalis philadelphica isolate P050 maturase K (matK) gene, partial cds; chloroplast
>gi|156629011|gb|EF438953.1| Physalis philadelphica isolate P060 maturase K (matK) gene, partial cds; chloroplast
$ grep -w iso tomatesverdes.fasta
$
```


#### `grep -E`

Lee el texto entre comillas como una expresión regular  completa, es decir con operadores, cuantificadores y posicionadores. Es útil utilizarlo junto con `-o` para mostrar solo la parte del texto encontrado que cumple con la expresión regular.

```
$ grep -oE "\| \w+ \w+" tomatesverdes.fasta
| Physalis philadelphica
| Physalis philadelphica
| Physalis philadelphica
| Physalis philadelphica
| Physalis philadelphica

```

**Ejercicio 1** Obtener el nombre de la especie *Physalis philadelphica* como en el ejemplo anterior, pero sin el "|" del principio.


**Ejercicio 2** Obtener el *nombre de las secuencias* de los archivos tomatesverdes.fasta y jitomares.fasta y escribirlos a un archivo llamado secsIDs. No importa cómo escribas la expresión regular, pero el chiste es lograr que toda la operación sea en una sola línea de código.

El texto dentro del archivo secsIDs debe verse así

```
>gi|156629013|gb|EF438954.1|
>gi|156629009|gb|EF438952.1|
>gi|156628921|gb|EF438908.1|
>gi|156628893|gb|EF438894.1|
>gi|156629011|gb|EF438953.1|
```


**Más información de expresiones regulares en:**

Cap 2. Cap 3. y Cap 5 de Haddock SHD, Dunn CW (2011) Practical computing for biologists. Sinauer Associates Sunderland, MA.

Buena referencia de expresiones regulares [aquí](http://tldp.org/LDP/abs/html/x17129.html)

Y buenos ejemplos de cómo usar `grep` [aquí](http://www.thegeekstuff.com/2009/03/15-practical-unix-grep-command-examples/)

**Nota:** `awk` y `sed` son otros comandos que también usan expresiones regulares.

`sed` es particularmente útil para sustituir una expresión regular (como una palabra) por otra.

Por ejemplo esta línea cambia "Solanum lycopersicum" del archivo "tomates.fasta" por "jitomate"

```
sed 's/Solanum lycopersicum/jitomate/' tomates.fasta
```

`awk` es parecido, pero es particularmente útil para archivos con filas y columnas, pues puedes acceder específicamente a ellas.


No los cubriremos aquí, pero vale la pena darles un ojo. Recomiendo esta [Introducción a `sed`](http://www.grymoire.com/Unix/Sed.html#uh-1)  y esta [introducción a `awk`](https://www.lifewire.com/write-awk-commands-and-scripts-2200573) así como estos [ejemplos de cómo se utilizan para manipular archivos fasta](http://bioinformatics.cvr.ac.uk/blog/short-command-lines-for-manipulation-fastq-and-fasta-sequence-files/).


## Redirección con bash

**Pregunta** ¿Qué son el Standar output y el Standar input?

###  `>` y `>>`

Redirige el Standar output (*stdout*) a un archivo en vez de imprimirlo en pantalla.

Estando en `/Unidad1/Prac_Uni1/Maiz`:

```
$ cat nuevos_final.fam *log > catejemplo.txt
$ ls
catejemplo.txt		ejemplonano.txt		nuevos_final.fam
ejemplo_final.bed	nuevos_final.bed	nuevos_final.log
ejemplo_final.fam	nuevos_final.bim
$ head catejemplo.txt
1 maiz_3 0 0 0 -9
2 maiz_68 0 0 0 -9
3 maiz_91 0 0 0 -9
4 maiz_39 0 0 0 -9
5 maiz_12 0 0 0 -9
6 maiz_41 0 0 0 -9
7 maiz_35 0 0 0 -9
8 maiz_58 0 0 0 -9
9 maiz_51 0 0 0 -9
10 maiz_82 0 0 0 -9
$ tail catejemplo.txt
Total genotyping rate in remaining individuals is 0.990151
0 SNPs failed missingness test ( GENO > 1 )
0 SNPs failed frequency test ( MAF < 0 )
After frequency and genotyping pruning, there are 36931 SNPs
After filtering, 0 cases, 0 controls and 165 missing
After filtering, 0 males, 0 females, and 165 of unspecified sex
Writing recoded file to [ nuevos_final.raw ]

Analysis finished: Wed May 06 12:19:30 2015
```

Nota que si el archivo catejemplo.txt ya existe será borrado por el comando anterior. Si no deseas que esto ocurra sino que el nuevo contenido se agregue al final de un archivo ya existente entonces usa  `>>`. Así:

```
$ cat nuevos_final.fam *log >> catejemplo.txt
```

**Ejercicio** utiliza `sed` para sustituir "Solanum lycopersicum" del archivo `Tomates/tomates.fasta` por "jitomate" y guarda el output en un nuevo archivo llamado "edited_tomates.fasta"


### `|`
Toma el stdout de un comando y lo convierte en el input de otro (*Pipes* the strout).

![Mariopipe](https://i.ytimg.com/vi/uMCCxuGIGtw/hqdefault.jpg)


Ejemplo:

```
$ ls
catejemplo.txt		ejemplonano.txt		nuevos_final.fam
ejemplo_final.bed	nuevos_final.bed	nuevos_final.log
ejemplo_final.fam	nuevos_final.bim
$ ls | wc -l
       8
```  

Otro ejemplo (no se muestra el stdout pues es demasiado largo)

```
cat *.fam | more
```


Más detalles y otras formas de redireccionar (que ocupan algunos programas) las puedes encontrar aquí [https://www.tutorialspoint.com/unix/unix-io-redirections.htm](https://www.tutorialspoint.com/unix/unix-io-redirections.htm)


**Ejercico** Primero explora qué hace el comando `history`. ¿Cómo lo combinarías con `grep` para buscar cuáles líneas hemos corrido con `less`?


## Loops con bash (¿están listos?)

Los *for loops* permiten **repetir** una serie de comandos con diferentes *variables de una lista*.


Sintaxis:

```
for i in list; do
 command1
 command2
 ..
done
```

"i" puede leerse como "el elemento i de la lista". Y  la lista no es más que el conjunto total de las variables que queremos.

Ejemplo:

```
$ for i in adenina citosina guanina timina; do
> echo "La $i es una base nitrogenada"
> done

La adenina es una base nitrogenada
La citosina es una base nitrogenada
La guanina es una base nitrogenada
La timina es una base nitrogenada
```


**Observaciones importantes:**

* Los elementos de la lista NO se separan por comas (en otros lenguajes sí).
* Para referirnos al "elemento i" dentro de los comandos debemos usar como prefijo el símbolo `$`.
* No tienes que escribir el `>` antes de `echo` y de `done`, los pongo solo para mostrar que eso aparece en la terminal hasta que terminemos de meter los comandos que formarán parte del loop. De hecho `done` sirve para decir "ok, aquí termina el loop". En los ejemplos de abajo ya no lo pondré.

Otro ejemplo:

```
for perro in labrador "pastor mesoamericano" xolo; do
echo Mi mejor amigo es un $perro; done

Mi mejor amigo es un labrador
Mi mejor amigo es un pastor mesoamericano
Mi mejor amigo es un xolo
```

**Preguntas**

1) ¿Cuándo debo usar comillas en la lista de elementos?

2) ¿Qué hace `;`?

Y un ejemplo más:

```
for i in {1..100};do
mkdir directorio$i; done
```

Lo cual hará 100 directorios, llamados directorio1, directorio2 y así.

**Pregunta** ¿De qué manera sencilla borrarías esos 100 directorios que acabas de crear?

### Definir variables

Los for loops utilizan *variables* definidas por el usuario, es decir "i" y "perro" en los ejemplos anteriores. Sin embargo, también pueden crearse variables **afuera** de un for loop, y usarlas para lo que queramos.

Ejemplo:

```
$ varx=2
$ $varx
-bash: 2: command not found

```

**Observaciones importantes**
* NO debe haber espacios entre el símbolo = y la variable o su valor.
* El nombre de la variable puede ser cualquier cosa que queramos **MENOS** el nombre de un comando que exista.

Las variables se pueden usar para acortar algo que escribamos muy seguido (como un path o un nombre de archivo largos) y conjuntar con otras variables dentro de un loop.

Ejemplo:

```
$ maullido=miau
$ for i in gato gatito gatón; do
> echo El $i hace $maullido
> done
El gato hace miau
El gatito hace miau
El gatón hace miau
```

**Ejercicio** Navega al directorio `/Unidad1/Prac_Uni1`. Desde ahí (i.e. **sin** utilizar `cd`) utiliza un for loop para crear por lo menos cuatro directorios dentro del directorio `Tomates/VerdesFritos`. Tu for loop debe incluir una variable definida externamente.


### Crear arrays y utilizarlos como una lista en un loop

Quizá quieras correr algo sobre muchas variables, como los nombres de 30 muestras o poblaciones distintas. Esto puede resolverse utilizando comodines, si los nombres lo permiten, o alimentando al loop con un un **arreglo**.

**Con comodines**

Por ejemplo si el loop lo quieres correr sobre puros archivos fasta que estén en un directorio (eg `Prac_Uni1/Tomates`):

```
$ ls
VerdesFritos		jitomate.fasta		tomatesverdes.fasta
$ for i in *.fasta; do
> echo "El archivo $i es un fasta ejemplo"
> echo "Utilizamos al archivo $i en este loop"
> done
El archivo jitomate.fasta es un fasta ejemplo
Utilizamos al archivo jitomate.fasta en este loop
El archivo tomatesverdes.fasta es un fasta ejemplo
Utilizamos al archivo tomatesverdes.fasta en este loop
```

**Con arreglos**

Los arreglos (una "lista"). Se generan parecido a las variables, pero con un par de () para indicar que se trata de un arreglo.

```
$ a=( gato gatito gatón )
```

Luego para indicar dentro de un loop que `a` es un array, debemos utilizar la notación `${a[@]}`:

```
$ for i in ${a[@]}; do echo El $i hace miau; done
El gato hace miau
El gatito hace miau
El gatón hace miau
```

Un arreglo también puede ser el resultado de un comando, por ejemplo de `grep`, siguiendo la siguiente sintaxis `
some_array=($(command))`. Ejemplo utilizando archivos en `Prac_Uni1/Maiz`:


```
$ a=($(grep -oE "\w+_[0-9]*" nuevos_final.fam))
$ for i in ${a[@]}; do echo Hacer algo con la muestra $i; done
Hacer algo con la muestra maiz_3
Hacer algo con la muestra maiz_68
Hacer algo con la muestra maiz_91
Hacer algo con la muestra maiz_39
Hacer algo con la muestra maiz_12
Hacer algo con la muestra maiz_41
Hacer algo con la muestra maiz_35
Hacer algo con la muestra maiz_58
Hacer algo con la muestra maiz_51
Hacer algo con la muestra maiz_82
Hacer algo con la muestra maiz_67
Hacer algo con la muestra maiz_93
Hacer algo con la muestra maiz_21
Hacer algo con la muestra maiz_6
Hacer algo con la muestra maiz_101
Hacer algo con la muestra maiz_27
Hacer algo con la muestra maiz_43
Hacer algo con la muestra maiz_1
Hacer algo con la muestra maiz_33
Hacer algo con la muestra maiz_100
Hacer algo con la muestra maiz_24
Hacer algo con la muestra maiz_103
Hacer algo con la muestra maiz_72
Hacer algo con la muestra maiz_10
Hacer algo con la muestra maiz_28
Hacer algo con la muestra maiz_49
Hacer algo con la muestra maiz_56
Hacer algo con la muestra maiz_66
Hacer algo con la muestra maiz_52
Hacer algo con la muestra maiz_47
Hacer algo con la muestra maiz_80
Hacer algo con la muestra maiz_65
Hacer algo con la muestra maiz_94
Hacer algo con la muestra maiz_36
Hacer algo con la muestra maiz_26
Hacer algo con la muestra maiz_105
Hacer algo con la muestra maiz_30
Hacer algo con la muestra maiz_16
Hacer algo con la muestra maiz_42
Hacer algo con la muestra maiz_4
Hacer algo con la muestra maiz_31
Hacer algo con la muestra maiz_17
Hacer algo con la muestra maiz_46
Hacer algo con la muestra maiz_5
Hacer algo con la muestra maiz_32
Hacer algo con la muestra maiz_19
Hacer algo con la muestra maiz_50
Hacer algo con la muestra maiz_8
Hacer algo con la muestra maiz_34
Hacer algo con la muestra maiz_23
Hacer algo con la muestra maiz_54
Hacer algo con la muestra maiz_14
Hacer algo con la muestra maiz_37
Hacer algo con la muestra maiz_25
Hacer algo con la muestra maiz_55
Hacer algo con la muestra maiz_40
Hacer algo con la muestra maiz_29
Hacer algo con la muestra maiz_60
Hacer algo con la muestra maiz_44
Hacer algo con la muestra maiz_74
Hacer algo con la muestra maiz_89
Hacer algo con la muestra maiz_64
Hacer algo con la muestra maiz_83
Hacer algo con la muestra maiz_75
Hacer algo con la muestra maiz_92
Hacer algo con la muestra maiz_69
Hacer algo con la muestra maiz_84
Hacer algo con la muestra maiz_76
Hacer algo con la muestra maiz_97
Hacer algo con la muestra maiz_70
Hacer algo con la muestra maiz_85
Hacer algo con la muestra maiz_77
Hacer algo con la muestra maiz_71
Hacer algo con la muestra maiz_86
Hacer algo con la muestra maiz_78
Hacer algo con la muestra maiz_102
Hacer algo con la muestra maiz_73
Hacer algo con la muestra maiz_88
Hacer algo con la muestra maiz_79
Hacer algo con la muestra maiz_106
Hacer algo con la muestra maiz_119
Hacer algo con la muestra maiz_148
Hacer algo con la muestra maiz_108
Hacer algo con la muestra maiz_120
Hacer algo con la muestra maiz_151
Hacer algo con la muestra maiz_134
Hacer algo con la muestra maiz_123
Hacer algo con la muestra maiz_153
Hacer algo con la muestra maiz_135
Hacer algo con la muestra maiz_124
Hacer algo con la muestra maiz_184
Hacer algo con la muestra maiz_140
Hacer algo con la muestra maiz_125
Hacer algo con la muestra maiz_141
Hacer algo con la muestra maiz_131
Hacer algo con la muestra maiz_189
Hacer algo con la muestra maiz_57
Hacer algo con la muestra maiz_126
Hacer algo con la muestra maiz_113
Hacer algo con la muestra maiz_138
Hacer algo con la muestra maiz_63
Hacer algo con la muestra maiz_127
Hacer algo con la muestra maiz_114
Hacer algo con la muestra maiz_139
Hacer algo con la muestra maiz_99
Hacer algo con la muestra maiz_129
Hacer algo con la muestra maiz_116
Hacer algo con la muestra maiz_142
Hacer algo con la muestra maiz_110
Hacer algo con la muestra maiz_132
Hacer algo con la muestra maiz_118
Hacer algo con la muestra maiz_144
Hacer algo con la muestra maiz_133
Hacer algo con la muestra maiz_121
Hacer algo con la muestra maiz_111
Hacer algo con la muestra maiz_137
Hacer algo con la muestra maiz_109
Hacer algo con la muestra maiz_146
Hacer algo con la muestra maiz_164
Hacer algo con la muestra maiz_157
Hacer algo con la muestra maiz_171
Hacer algo con la muestra maiz_149
Hacer algo con la muestra maiz_165
Hacer algo con la muestra maiz_159
Hacer algo con la muestra maiz_172
Hacer algo con la muestra maiz_150
Hacer algo con la muestra maiz_166
Hacer algo con la muestra maiz_160
Hacer algo con la muestra maiz_173
Hacer algo con la muestra maiz_152
Hacer algo con la muestra maiz_167
Hacer algo con la muestra maiz_161
Hacer algo con la muestra maiz_174
Hacer algo con la muestra maiz_154
Hacer algo con la muestra maiz_169
Hacer algo con la muestra maiz_162
Hacer algo con la muestra maiz_176
Hacer algo con la muestra maiz_156
Hacer algo con la muestra maiz_170
Hacer algo con la muestra maiz_163
Hacer algo con la muestra maiz_177
Hacer algo con la muestra maiz_178
Hacer algo con la muestra maiz_192
Hacer algo con la muestra maiz_185
Hacer algo con la muestra maiz_201
Hacer algo con la muestra maiz_179
Hacer algo con la muestra maiz_193
Hacer algo con la muestra maiz_186
Hacer algo con la muestra maiz_202
Hacer algo con la muestra maiz_180
Hacer algo con la muestra maiz_195
Hacer algo con la muestra maiz_187
Hacer algo con la muestra maiz_181
Hacer algo con la muestra maiz_197
Hacer algo con la muestra maiz_188
Hacer algo con la muestra maiz_182
Hacer algo con la muestra maiz_198
Hacer algo con la muestra maiz_190
Hacer algo con la muestra maiz_200
Hacer algo con la muestra maiz_183
Hacer algo con la muestra maiz_191
Hacer algo con la muestra teos_96
Hacer algo con la muestra teos_203
Hacer algo con la muestra teos_911
Hacer algo con la muestra teos_9107
```

**Pregunta**: Si `some_array=($(command))` sirve para crear un arreglo a partir del resultado de un comando ¿Cómo puedes crear una **variable** a partir de un comando?

**Leyendo desde un archivo**

Los arrays tienen sus problemas cuando son muy grandes y  es fácil cometer errores porque nunca "los vemos", por lo tanto mucha gente prefiere mejor leer los elemntos directo de un archivo. Ejemplo:

```
$ grep -oE "\w+_[0-9]*" nuevos_final.fam > muestras.txt
$ for i in $(cat muestras.txt); do echo Hacer algo con la muestra $i; done
Hacer algo con la muestra maiz_3
Hacer algo con la muestra maiz_68
Hacer algo con la muestra maiz_91
Hacer algo con la muestra maiz_39
Hacer algo con la muestra maiz_12
Hacer algo con la muestra maiz_41
Hacer algo con la muestra maiz_35
Hacer algo con la muestra maiz_58
Hacer algo con la muestra maiz_51
Hacer algo con la muestra maiz_82
Hacer algo con la muestra maiz_67
Hacer algo con la muestra maiz_93
Hacer algo con la muestra maiz_21
Hacer algo con la muestra maiz_6
Hacer algo con la muestra maiz_101
Hacer algo con la muestra maiz_27
Hacer algo con la muestra maiz_43
Hacer algo con la muestra maiz_1
... [o sea lo mismo que hace rato]

```


### Más información de for loops

Aquí presenté la sintaxis más usada, pero hay otros métodos para escribir loops que hacen lo mismo. Y también pueden hacerse más complejos agregando "ifs".
Puedes consultar esta y más info de for loops en [esta guía con ejemplos y varios formatos](http://www.thegeekstuff.com/2011/07/bash-for-loop-examples/).


##### Ejercicios

1. Escribe **una línea de código** que cree un archivo con los nombres de las muestras de maiz enlistadas en `/Unidad1/Prac_Uni1/Maiz/nuevos_final.fam`.

2. Escribe **un script** que cree 4 directorios llamados PobA, PobB, PobC, PobD y dentro de cada uno de ellos un archivo de texto que diga "Este es un individuo de la población x" donde x debe corresponder al nombre del directorio.

3. Escribe un script que baje 5 secuencias (algún loci corto, no un genoma) de una especie que te interese y señala cuántas veces existe la secuencia "TGCA" en cada una de ellas. ¿Sabes qué hace esta secuencia?





###Tomado de Alicia Mastretta.
