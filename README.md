
# 🧩 1. Introduction

Le langage C dispose d’un **ensemble riche de librairies standard**.  
Ces librairies permettent de :

- Gérer les **entrées/sorties** (clavier, console, fichiers)  
- Manipuler des **chaînes et blocs mémoire**  
- Effectuer des **calculs mathématiques complexes**  
- Interagir avec le **système et la mémoire**  
- Développer des programmes **réseau et multithreading**  

Bien comprendre et utiliser ces librairies est essentiel pour écrire un code **robuste, maintenable et performant**.

---

# 🏛️ 2. Librairies essentielles

## 📥 `<stdio.h>` — Entrées / Sorties

**Description :**  
Permet la lecture et écriture sur la console et les fichiers.  
Fournit des fonctions de gestion de flux, formatage et contrôle.

**Cas d’utilisation :**  
- Lecture et écriture console  
- Gestion de fichiers texte et binaires  
- Débogage simple via affichage formaté

### Fonctions clés

| Fonction | Description | Exemple |
|----------|-------------|---------|
| `printf()` | Affiche du texte formaté sur la console | `printf("Bonjour %s\n", nom);` |
| `scanf()` | Lit une entrée formatée | `scanf("%d", &age);` |
| `fopen()` | Ouvre un fichier | `fopen("data.txt","r");` |
| `fclose()` | Ferme un fichier ouvert | `fclose(fichier);` |
| `fprintf()` | Écrit dans un fichier formaté | `fprintf(fichier,"Score=%d",score);` |
| `fscanf()` | Lit depuis un fichier formaté | `fscanf(fichier,"%d",&val);` |
| `putchar()` | Écrit un caractère | `putchar('A');` |
| `getchar()` | Lit un caractère | `char c = getchar();` |
| `fgets()` | Lit une ligne depuis un fichier | `fgets(buffer,100,fichier);` |
| `fputs()` | Écrit une ligne dans un fichier | `fputs("Hello\n",fichier);` |
| `feof()` | Vérifie fin de fichier | `while(!feof(fichier)) {...}` |
| `fflush()` | Vide le buffer | `fflush(stdout);` |

**Exemple complet :**

```c
#include <stdio.h>

int main() {
    char nom[20];
    FILE *f = fopen("test.txt","w");
    printf("Entrez votre nom : ");
    scanf("%s", nom);
    fprintf(f, "Nom entré : %s\n", nom);
    fclose(f);
    printf("Nom enregistré dans test.txt\n");
    return 0;
}
```

**Conseils :**

* Toujours vérifier si `fopen()` retourne NULL
* Toujours fermer les fichiers avec `fclose()`
* Utiliser `fflush(stdout)` pour forcer l’affichage immédiat

---

## 🧱 `<stdlib.h>` — Fonctions fondamentales

**Description :**
Librairie centrale pour la **gestion mémoire**, la génération de nombres aléatoires, la conversion de chaînes et le contrôle du programme.

**Cas d’utilisation :**

* Allocation dynamique mémoire
* Gestion du programme (exit, system)
* Conversion chaîne → nombre
* Génération aléatoire

### Fonctions clés

| Fonction    | Description                   | Exemple                                         |
| ----------- | ----------------------------- | ----------------------------------------------- |
| `malloc()`  | Alloue un bloc mémoire        | `int *tab = malloc(10*sizeof(int));`            |
| `calloc()`  | Alloue et initialise à zéro   | `int *tab = calloc(10,sizeof(int));`            |
| `realloc()` | Redimensionne un bloc mémoire | `tab = realloc(tab,20*sizeof(int));`            |
| `free()`    | Libère la mémoire             | `free(tab);`                                    |
| `atoi()`    | Convertit chaîne → int        | `int x = atoi("42");`                           |
| `atof()`    | Convertit chaîne → float      | `float y = atof("3.14");`                       |
| `atol()`    | Convertit chaîne → long       | `long l = atol("123456");`                      |
| `rand()`    | Génère un entier aléatoire    | `int r = rand()%100;`                           |
| `srand()`   | Initialise le générateur      | `srand(time(NULL));`                            |
| `exit()`    | Termine le programme          | `exit(0);`                                      |
| `system()`  | Exécute commande shell        | `system("ls");`                                 |
| `bsearch()` | Recherche binaire             | `int *p = bsearch(&val,tab,n,sizeof(int),cmp);` |

**Exemple complet :**

```c
#include <stdio.h>
#include <stdlib.h>

int main() {
    int *tab = malloc(5*sizeof(int));
    for(int i=0;i<5;i++) tab[i] = i*i;
    for(int i=0;i<5;i++) printf("%d ", tab[i]);
    free(tab);
    return 0;
}
```

**Conseils :**

* Toujours libérer la mémoire allouée (`free`)
* Initialiser le générateur aléatoire avec `srand`
* Vérifier que `malloc`/`calloc` ne retourne pas NULL

---

## 🧵 `<string.h>` — Manipulation de chaînes et mémoire

**Description :**
Permet de travailler efficacement sur **chaînes de caractères** et **blocs mémoire**.

**Cas d’utilisation :**

* Concaténer, copier, comparer des chaînes
* Manipulation mémoire (buffers)
* Recherche de caractères ou sous-chaînes

### Fonctions clés

| Fonction    | Description                  | Exemple                      |
| ----------- | ---------------------------- | ---------------------------- |
| `strlen()`  | Longueur d’une chaîne        | `size_t l = strlen("test");` |
| `strcpy()`  | Copie chaîne                 | `strcpy(dest, src);`         |
| `strncpy()` | Copie avec limite            | `strncpy(dest, src,5);`      |
| `strcat()`  | Concatène chaînes            | `strcat(a,b);`               |
| `strncat()` | Concatène avec limite        | `strncat(a,b,3);`            |
| `strcmp()`  | Compare deux chaînes         | `strcmp(a,b);`               |
| `strncmp()` | Compare jusqu’à n caractères | `strncmp(a,b,3);`            |
| `strchr()`  | Cherche un caractère         | `strchr(a,'x');`             |
| `strrchr()` | Cherche dernier caractère    | `strrchr(a,'x');`            |
| `strstr()`  | Cherche une sous-chaîne      | `strstr(a,"abc");`           |
| `memset()`  | Remplit mémoire              | `memset(tab,0,10);`          |
| `memcpy()`  | Copie mémoire                | `memcpy(dest,src,10);`       |

**Exemple complet :**

```c
#include <string.h>
#include <stdio.h>

int main() {
    char str1[20] = "Bonjour";
    char str2[] = " le monde";
    strcat(str1,str2);
    printf("%s\n", str1);
    return 0;
}
```

**Conseils :**

* Toujours réserver assez d’espace pour `strcat`
* Préférer `strncpy` pour éviter les débordements
* `memcpy` peut copier n’importe quel type de donnée, pas seulement des chaînes

---

## 🧮 `<math.h>` — Mathématiques avancées

**Description :**
Pour tous les calculs scientifiques, trigonométriques, logarithmiques et exponentiels.

**Cas d’utilisation :**

* Algorithmes scientifiques
* Simulations physiques et trigonométriques
* Statistiques et calculs numériques

### Fonctions clés

| Fonction  | Description            | Exemple             |
| --------- | ---------------------- | ------------------- |
| `pow()`   | Puissance              | `pow(2,3)` → 8      |
| `sqrt()`  | Racine carrée          | `sqrt(9)` → 3       |
| `cbrt()`  | Racine cubique         | `cbrt(8)` → 2       |
| `fabs()`  | Valeur absolue float   | `fabs(-3.2)` → 3.2  |
| `ceil()`  | Arrondi supérieur      | `ceil(3.2)` → 4     |
| `floor()` | Arrondi inférieur      | `floor(3.8)` → 3    |
| `round()` | Arrondi au plus proche | `round(3.5)` → 4    |
| `sin()`   | Sinus                  | `sin(3.14/2)` → 1   |
| `cos()`   | Cosinus                | `cos(0)` → 1        |
| `tan()`   | Tangente               | `tan(0)` → 0        |
| `log()`   | Logarithme naturel     | `log(2.718)` → 1    |
| `exp()`   | Exponentielle          | `exp(1)` → 2.718... |

**Exemple complet :**

```c
#include <stdio.h>
#include <math.h>

int main() {
    double x = 2.0;
    printf("sqrt(%f) = %f\n", x, sqrt(x));
    printf("2^3 = %f\n", pow(2,3));
    return 0;
}
```

**Conseils :**

* Compiler avec `-lm` (`gcc fichier.c -lm`)
* Vérifier la précision des floats/doubles pour éviter les erreurs d’arrondi

---

# 🔢 3. Librairies numériques et avancées

## 🔢 `<complex.h>` — Nombres complexes

**Description :**  
Permet de créer et manipuler des nombres complexes (a + bi). Très utilisé en physique, électronique et traitement du signal.

**Cas d’utilisation :**  
- Calculs avec nombres complexes  
- Électronique, circuits AC  
- Algèbre linéaire et simulations physiques

### Fonctions clés

| Fonction | Description | Exemple |
|----------|-------------|---------|
| `I` | Constante imaginaire | `double complex z = 1.0 + 2.0*I;` |
| `cabs()` | Module d’un complexe | `cabs(z)` → √(a²+b²) |
| `carg()` | Argument (angle) | `carg(z)` |
| `creal()` | Partie réelle | `creal(z)` |
| `cimag()` | Partie imaginaire | `cimag(z)` |
| `cadd()` | Addition complexe | `z1 + z2` |
| `csub()` | Soustraction complexe | `z1 - z2` |
| `cmul()` | Multiplication complexe | `z1 * z2` |
| `cdiv()` | Division complexe | `z1 / z2` |
| `cexp()` | Exponentielle complexe | `cexp(z)` |
| `clog()` | Logarithme complexe | `clog(z)` |
| `csqrt()` | Racine carrée complexe | `csqrt(z)` |

**Exemple complet :**

```c
#include <stdio.h>
#include <complex.h>

int main() {
    double complex z1 = 1.0 + 2.0*I;
    double complex z2 = 2.0 - I;
    double complex z3 = z1 + z2;
    printf("z3 = %.2f + %.2fi\n", creal(z3), cimag(z3));
    printf("Module de z1 = %.2f\n", cabs(z1));
    return 0;
}
```

---

## 📏 `<float.h>` — Limites numériques

**Description :**
Permet de connaître les limites, précision et caractéristiques des types flottants (`float`, `double`, `long double`).

**Cas d’utilisation :**

* Calculs sensibles
* Eviter les erreurs d’arrondi
* Comparaison de flottants

### Constantes clés

| Constante      | Description                        |
| -------------- | ---------------------------------- |
| `FLT_MAX`      | Plus grand float                   |
| `FLT_MIN`      | Plus petit float positif           |
| `DBL_MAX`      | Plus grand double                  |
| `DBL_MIN`      | Plus petit double positif          |
| `LDBL_MAX`     | Plus grand long double             |
| `LDBL_MIN`     | Plus petit long double positif     |
| `FLT_EPSILON`  | Plus petit incrément float         |
| `DBL_EPSILON`  | Plus petit incrément double        |
| `LDBL_EPSILON` | Plus petit incrément long double   |
| `FLT_DIG`      | Chiffres significatifs float       |
| `DBL_DIG`      | Chiffres significatifs double      |
| `LDBL_DIG`     | Chiffres significatifs long double |

**Exemple :**

```c
#include <stdio.h>
#include <float.h>

int main() {
    printf("Max float = %e\n", FLT_MAX);
    printf("Epsilon double = %e\n", DBL_EPSILON);
    return 0;
}
```

---

# ✒️ 4. Caractères et formatage

## 🔠 `<ctype.h>` — Tests sur les caractères

**Description :**
Permet d’identifier et transformer les caractères.

**Cas d’utilisation :**

* Validation d’input utilisateur
* Nettoyage de texte
* Analyse de données

### Fonctions clés

| Fonction     | Description                           |
| ------------ | ------------------------------------- |
| `isdigit()`  | Vérifie si caractère est un chiffre   |
| `isalpha()`  | Vérifie si caractère est une lettre   |
| `isalnum()`  | Lettre ou chiffre                     |
| `isspace()`  | Vérifie espace / tabulation / newline |
| `isupper()`  | Vérifie majuscule                     |
| `islower()`  | Vérifie minuscule                     |
| `toupper()`  | Convertit en majuscule                |
| `tolower()`  | Convertit en minuscule                |
| `isxdigit()` | Vérifie caractère hexadécimal         |
| `isprint()`  | Vérifie caractère imprimable          |
| `ispunct()`  | Vérifie ponctuation                   |
| `iscntrl()`  | Vérifie caractère de contrôle         |

**Exemple :**

```c
#include <stdio.h>
#include <ctype.h>

int main() {
    char c = 'a';
    if(isalpha(c)) printf("%c est une lettre\n", c);
    printf("Majuscule : %c\n", toupper(c));
    return 0;
}
```

---

## 🌍 `<locale.h>` — Formats locaux

**Description :**
Permet de gérer les conventions locales, comme le format de date, monnaie, nombres.

**Cas d’utilisation :**

* Internationalisation
* Affichage correct selon région
* Traitement de fichiers multilingues

### Fonctions clés

| Fonction       | Description                        |
| -------------- | ---------------------------------- |
| `setlocale()`  | Définit la locale                  |
| `localeconv()` | Obtient informations sur la locale |
| `LC_ALL`       | Toutes les catégories              |
| `LC_NUMERIC`   | Formats numériques                 |
| `LC_TIME`      | Formats date/heure                 |
| `LC_MONETARY`  | Format monétaire                   |
| `LC_COLLATE`   | Comparaison de chaînes             |
| `LC_CTYPE`     | Classification caractères          |
| `LC_MESSAGES`  | Langue des messages                |
| `newlocale()`  | Crée nouvelle locale               |
| `uselocale()`  | Applique locale                    |
| `freelocale()` | Libère locale                      |

**Exemple :**

```c
#include <stdio.h>
#include <locale.h>

int main() {
    setlocale(LC_ALL,"fr_FR.UTF-8");
    printf("Locale actuelle : %s\n", setlocale(LC_ALL,NULL));
    return 0;
}
```

---

# ⏳ 5. Gestion du temps

## 🕒 `<time.h>` — Gestion du temps

**Description :**
Pour mesurer le temps, obtenir la date/heure et faire des chronomètres.

**Cas d’utilisation :**

* Chronométrage
* Statistiques et logs
* Calculs temporels

### Fonctions clés

| Fonction      | Description                          |
| ------------- | ------------------------------------ |
| `time()`      | Timestamp actuel                     |
| `clock()`     | Temps CPU depuis début programme     |
| `difftime()`  | Différence entre deux temps          |
| `mktime()`    | Convertit struct tm → time_t         |
| `localtime()` | Conversion time_t → struct tm locale |
| `gmtime()`    | Conversion time_t → struct tm UTC    |
| `strftime()`  | Formate date/heure                   |
| `asctime()`   | Formate struct tm en string          |
| `ctime()`     | Formate time_t en string             |
| `difftime()`  | Différence en secondes               |
| `time_t`      | Type représentant le temps           |
| `struct tm`   | Structure détaillée date/heure       |

**Exemple :**

```c
#include <stdio.h>
#include <time.h>

int main() {
    time_t now = time(NULL);
    printf("Timestamp actuel: %ld\n", now);
    printf("Heure locale: %s\n", ctime(&now));
    return 0;
}
```
---

# 🖥️ 6. Programmation Système (Linux / POSIX)

## 🧱 `<unistd.h>` — Fonctions système

**Description :**  
Permet d’interagir avec le système POSIX : processus, entrées/sorties bas niveau, gestion de fichiers, etc.

**Cas d’utilisation :**  
- Gestion des processus et forks  
- Lecture/écriture directe sur fichiers et périphériques  
- Sleep et temporisation  
- Scripts et outils système

### Fonctions clés

| Fonction   | Description                                      |
|----------  |------------------------------------------------  |
| `fork()`   | Crée un processus fils                           |
| `execve()` | Remplace le processus courant par un programme   |
| `getpid()` | Retourne PID du processus courant                |
| `getppid()`| Retourne PID du parent                           |
| `sleep()`  | Met en pause le processus                        |
| `usleep()` | Pause en microsecondes                           |
| `read()`   | Lit depuis un fichier/périphérique               |
| `write()`  | Écrit dans un fichier/périphérique               |
| `close()`  | Ferme un descripteur de fichier                  |
| `pipe()`   | Crée un canal entre processus                    |
| `dup()`    | Duplique un descripteur de fichier               |
| `alarm()`  | Envoie un signal après n secondes                |

**Exemple :**

```c id="l06hx1"
#include <unistd.h>
#include <stdio.h>

int main() {
    pid_t pid = fork();
    if(pid == 0) {
        printf("Je suis le fils, PID=%d\n", getpid());
    } else {
        printf("Je suis le père, PID=%d\n", getpid());
    }
    return 0;
}
```

**Conseils :**

* Toujours vérifier le retour de `fork()`
* `read` et `write` sont bas niveau → plus rapides que `fread/fwrite`
* Utiliser `close` pour libérer les descripteurs

---

## 🗃️ `<fcntl.h>` — Contrôle des fichiers

**Description :**
Permet de contrôler l’accès aux fichiers et de définir des flags et droits.

**Cas d’utilisation :**

* Ouvrir fichiers en mode non-bloquant
* Gérer verrous (lock)
* Configurer les droits

### Fonctions clés

| Fonction   | Description                 |
| ---------- | --------------------------- |
| `open()`   | Ouvre un fichier avec flags |
| `creat()`  | Crée un fichier             |
| `fcntl()`  | Contrôle des descripteurs   |
| `O_RDONLY` | Flag lecture seule          |
| `O_WRONLY` | Flag écriture seule         |
| `O_RDWR`   | Lecture + écriture          |
| `O_APPEND` | Ajoute à la fin             |
| `O_CREAT`  | Crée si inexistant          |
| `O_TRUNC`  | Tronque le fichier          |
| `lockf()`  | Verrouillage fichier        |
| `close()`  | Ferme fichier               |
| `read()`   | Lit fichier                 |

**Exemple :**

```c id="h93d2s"
#include <fcntl.h>
#include <unistd.h>
#include <stdio.h>

int main() {
    int fd = open("test.txt", O_CREAT | O_RDWR, 0644);
    if(fd == -1) { perror("open"); return 1; }
    write(fd, "Hello\n",6);
    close(fd);
    return 0;
}
```

---

## 📂 `<sys/stat.h>` — Infos fichiers

**Description :**
Obtenir les informations sur fichiers et répertoires.

**Cas d’utilisation :**

* Vérifier taille, permissions, type de fichier
* Scripts et monitoring systèmes

### Fonctions / macros clés

| Fonction    | Description                       |
| ----------- | --------------------------------- |
| `stat()`    | Infos sur un fichier              |
| `fstat()`   | Infos via descripteur             |
| `lstat()`   | Infos sans suivre lien symbolique |
| `st_mode`   | Type et permissions               |
| `st_size`   | Taille fichier                    |
| `st_uid`    | UID propriétaire                  |
| `st_gid`    | GID groupe                        |
| `S_ISREG()` | Vérifie fichier régulier          |
| `S_ISDIR()` | Vérifie dossier                   |
| `S_ISLNK()` | Vérifie lien symbolique           |
| `chmod()`   | Change permissions                |
| `mkdir()`   | Crée répertoire                   |

**Exemple :**

```c id="y2mjfs"
#include <sys/stat.h>
#include <stdio.h>

int main() {
    struct stat st;
    if(stat("test.txt",&st)==0) {
        printf("Taille: %ld octets\n", st.st_size);
        printf("C'est un fichier régulier ? %d\n", S_ISREG(st.st_mode));
    }
    return 0;
}
```

---

## 🧬 `<sys/types.h>` — Types système

**Description :**
Définit les types utilisés dans les appels système.

**Fonctions / types clés**

| Type      | Description              |
| --------- | ------------------------ |
| `pid_t`   | PID processus            |
| `uid_t`   | UID utilisateur          |
| `gid_t`   | GID groupe               |
| `off_t`   | Taille/offset fichier    |
| `ssize_t` | Retour lecture/écriture  |
| `mode_t`  | Type permissions         |
| `time_t`  | Temps en secondes        |
| `size_t`  | Taille objet mémoire     |
| `key_t`   | IPC key                  |
| `ino_t`   | Numéro inode             |
| `dev_t`   | Identifiant périphérique |
| `nlink_t` | Nombre de liens          |

---

# ⚠️ 7. Gestion des erreurs

## 🚨 `<errno.h>` — Codes erreurs système

**Description :**
Fournit le code d’erreur global et fonctions associées.

**Cas d’utilisation :**

* Comprendre pourquoi une fonction système a échoué
* Débogage fiable

### Fonctions clés

| Fonction / variable | Description                                 |
| ------------------- | ------------------------------------------- |
| `errno`             | Variable globale contenant le code d’erreur |
| `perror()`          | Affiche message d’erreur associé à errno    |
| `strerror()`        | Retourne chaîne texte de l’erreur           |
| `EDOM`              | Erreur domaine mathématique                 |
| `ERANGE`            | Erreur dépassement                          |
| `EACCES`            | Permission refusée                          |
| `ENOENT`            | Fichier non trouvé                          |
| `EEXIST`            | Fichier existe déjà                         |
| `EINVAL`            | Paramètre invalide                          |
| `ENOMEM`            | Mémoire insuffisante                        |
| `EIO`               | Erreur d’entrée/sortie                      |
| `EPERM`             | Opération non permise                       |

**Exemple :**

```c id="j39lxq"
#include <stdio.h>
#include <errno.h>
#include <string.h>

int main() {
    FILE *f = fopen("nonexistent.txt","r");
    if(!f) perror("Erreur fopen");
    return 0;
}
```

---

# 🛰️ 8. Réseaux & Sockets

## 🌐 `<sys/socket.h>` — Création sockets

**Description :**
Pour programmer réseau TCP/UDP.

**Cas d’utilisation :**

* Clients/serveurs réseau
* Transmission données
* Communication interprocessus

### Fonctions clés

| Fonction       | Description                |
| -------------- | -------------------------- |
| `socket()`     | Crée une socket            |
| `bind()`       | Associe socket à IP/port   |
| `listen()`     | Met serveur en écoute      |
| `accept()`     | Accepte connexion entrante |
| `connect()`    | Connecte client à serveur  |
| `send()`       | Envoie données             |
| `recv()`       | Reçoit données             |
| `sendto()`     | Envoie UDP                 |
| `recvfrom()`   | Reçoit UDP                 |
| `close()`      | Ferme socket               |
| `setsockopt()` | Configure options socket   |
| `getsockopt()` | Lit options socket         |

---

## 📡 `<netinet/in.h>` — Structures réseau

**Description :**
Définit adresses IP, ports et structures pour sockets.

**Structures clés**

| Structure / Macro    | Description                |
| -------------------- | -------------------------- |
| `struct sockaddr_in` | Adresse IPv4               |
| `sin_family`         | Type protocole             |
| `sin_port`           | Port réseau                |
| `sin_addr`           | Adresse IPv4               |
| `INADDR_ANY`         | Toute interface locale     |
| `htons()`            | Conversion port → réseau   |
| `htonl()`            | Conversion long → réseau   |
| `ntohs()`            | Conversion port → hôte     |
| `ntohl()`            | Conversion long → hôte     |
| `struct in_addr`     | Représente IP              |
| `inet_addr()`        | Convertit string → in_addr |
| `inet_ntoa()`        | Convertit in_addr → string |

---

## 🔌 `<arpa/inet.h>` — Conversion IP

**Fonctions clés**

| Fonction          | Description                            |
| ----------------- | -------------------------------------- |
| `inet_pton()`     | String → binaire                       |
| `inet_ntop()`     | Binaire → string                       |
| `htons()`         | Port hôte → réseau                     |
| `htonl()`         | Long hôte → réseau                     |
| `ntohs()`         | Port réseau → hôte                     |
| `ntohl()`         | Long réseau → hôte                     |
| `inet_addr()`     | Convertit IPv4 string → in_addr_t      |
| `inet_aton()`     | Convertit IPv4 string → struct in_addr |
| `inet_ntoa()`     | Convertit struct in_addr → string      |
| `inet_makeaddr()` | Combine réseau + hôte                  |
| `inet_lnaof()`    | Adresse hôte seule                     |
| `inet_netof()`    | Adresse réseau seule                   |

---

# 🧵 9. Multithreading

## ⚙️ `<pthread.h>` — Threads POSIX

**Description :**
Permet la programmation parallèle via threads.

**Cas d’utilisation :**

* Serveurs multi-clients
* Calcul parallèle
* Synchronisation via mutex

### Fonctions clés

| Fonction                  | Description                   |
| ------------------------- | ----------------------------- |
| `pthread_create()`        | Crée un thread                |
| `pthread_join()`          | Attend fin d’un thread        |
| `pthread_exit()`          | Termine thread courant        |
| `pthread_self()`          | Retourne ID thread courant    |
| `pthread_detach()`        | Détache un thread             |
| `pthread_mutex_init()`    | Initialise mutex              |
| `pthread_mutex_lock()`    | Verrouille mutex              |
| `pthread_mutex_unlock()`  | Déverrouille mutex            |
| `pthread_mutex_destroy()` | Supprime mutex                |
| `pthread_cond_init()`     | Initialise condition variable |
| `pthread_cond_wait()`     | Attend condition variable     |
| `pthread_cond_signal()`   | Signale condition variable    |

**Exemple :**

```c id="w0x3p9"
#include <stdio.h>
#include <pthread.h>

void* threadFunc(void *arg) {
    printf("Hello depuis le thread!\n");
    return NULL;
}

int main() {
    pthread_t t;
    pthread_create(&t, NULL, threadFunc, NULL);
    pthread_join(t, NULL);
    return 0;
}
```

---

# 🏁 Conclusion

Les librairies C étudiées couvrent :

* Entrées/Sorties, chaînes, mathématiques, nombres complexes
* Gestion mémoire et erreurs
* Système, fichiers, processus
* Réseau et multithreading

**Bien choisir et comprendre chaque librairie permet :**

* Code plus propre et rapide
* Meilleure sécurité et robustesse
* Développement d’applications complexes (scientifique, serveur, multithread)

---
