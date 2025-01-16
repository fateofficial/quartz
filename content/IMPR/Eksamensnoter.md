# Introduktion til C og Programmeringsstil

C er et effektivt programmeringssprog, der bruges til alt fra systemprogrammering til applikationer. God programmeringsstil er essentiel for at skrive læsbar, vedligeholdelsesvenlig og fejlfri kode. Følgende emner dækker grundlæggende koncepter, der er værd at kende.

---

### Hello World og Programmeringsstil

Det første program i C er ofte "Hello World", som introducerer grundstrukturen for et program i C.

```c
#include <stdio.h>

int main() {
    printf("Hello, World!\n");
    return 0;
}
```

**Vigtige observationer**:
- `#include <stdio.h>` er nødvendig for input/output-funktioner.
- `main()` er indgangspunktet for alle C-programmer.
- `printf()` bruges til at udskrive tekst.
- `return 0;` angiver, at programmet afsluttedes korrekt.

**Programmeringsstil**:
- Indrykning og brug af mellemrum forbedrer læsbarheden.
- Kommenter koden for at forklare formål og funktioner.

---

### Variable og Tildeling (Assignment)

#### Variable
Variable bruges til at gemme data i hukommelsen. De skal erklæres med en datatype.

```c
int age = 25;  // En integer-variabel
float pi = 3.14;  // En flydende-komma-variabel
```

#### Tildeling
Tildeling bruger `=` til at give en variabel en værdi.

```c
int x = 5;
x = x + 1;  // x bliver 6
```

**Initialisering**: Det anbefales altid at initialisere variable, når de erklæres.

**Typiske fejl**:
- Manglende initialisering før brug kan føre til udefineret adfærd.

---

### Symbolske Konstanter

Symbolske konstanter bruges til at repræsentere faste værdier, hvilket gør koden mere læsbar og lettere at vedligeholde.

```c
#define PI 3.14
```

Brug altid store bogstaver til konstanter for at skelne dem fra variable.

---

### Udtryk og Operatorer

Udtryk består af variable, konstanter og operatorer, der evalueres til en værdi.

#### Operatorer
- **Aritmetiske operatorer**: `+`, `-`, `*`, `/`, `%`
- **Relationale operatorer**: `==`, `!=`, `<`, `>`, `<=`, `>=`
- **Logiske operatorer**: `&&`, `||`, `!`

```c
int a = 10, b = 20;
if (a < b && b > 15) {
    printf("Betingelsen er sand.\n");
}
```

#### Prioritering og Associering
Operatorer har prioritet, der bestemmer rækkefølgen af evaluering.
- Aritmetiske operatorer har højere prioritet end relationelle.
- Brug parenteser for at styre rækkefølgen eksplicit.

---

### Input og Output

#### Udskrivning med `printf`
`printf` bruges til at udskrive tekst og værdier.

```c
int age = 25;
printf("Jeg er %d \u00e5r gammel.\n", age);
```

Format-specifikatorer som `%d` (heltal) og `%f` (flydende-komma) bruges til at udskrive forskellige datatyper.

#### Indlæsning med `scanf`
`scanf` bruges til at læse input fra brugeren.

```c
int number;
printf("Indtast et tal: ");
scanf("%d", &number);
printf("Du indtastede: %d\n", number);
```

**Bemærk**: Brug `&` foran variabler i `scanf` for at angive hukommelsesadressen.

---

### Eksempler på Programmer

#### Udtryk og Beregninger
Et simpelt eksempel, der beregner summen af to tal:

```c
int a = 5, b = 10;
int sum = a + b;
printf("Summen er: %d\n", sum);
```

#### Input-Output Eksempel
Et program, der tager et tal som input og fordobler det:

```c
int num;
printf("Indtast et tal: ");
scanf("%d", &num);
num = num * 2;
printf("Det dobbelte er: %d\n", num);
```

---

### Fejlfinding og Typiske Problemer
- **Forkert brug af `=` i stedet for `==`**: Dette er en af de mest almindelige fejl i C.
  ```c
  if (x = 5) {  // Tildeling i stedet for sammenligning
      printf("Dette er forkert.\n");
  }
  ```
- **Manglende semikolon**: Alle C-sætninger skal slutte med `;`.
- **Glemt initialisering af variable**: Kan føre til uforudsigelige resultater.
# Kontrolstrukturer i C

Kontrolstrukturer er essentielle i programmering, da de giver mulighed for at styre programmets flow baseret på betingelser eller gentagelser. Disse strukturer hjælper med at organisere koden og gøre den mere overskuelig, hvilket reducerer risikoen for fejl og gør det lettere at vedligeholde.

#### Typer af Kontrolstrukturer
1. **Sekventiel udførelse**: Koden udføres linje for linje i rækkefølge.
2. **Selektiv udførelse**: Koden udføres kun, hvis bestemte betingelser er opfyldt (f.eks. `if`-sætninger).
3. **Iterativ udførelse**: Gentagelse af kodeblokke, indtil en betingelse ikke længere er sand (f.eks. løkker som `while` og `for`).

---

### Logiske Udtryk og Operatorer
Logiske udtryk evaluerer betingelser og returnerer sand (true) eller falsk (false). De bruges til at kontrollere flowet i selektive og itererende strukturer.

- **Logiske operatorer**:
  - `&&` (AND): Begge betingelser skal være sande.
  - `||` (OR): Mindst én betingelse skal være sand.
  - `!` (NOT): Negerer en betingelse.
- **Prioritet og evaluering**: 
  - Operatoren `!` evalueres før `&&`, som igen evalueres før `||`.
  - Brug parenteser for at gøre komplekse udtryk mere læsbare og sikre korrekt rækkefølge.
- **Short Circuit Evaluering**:
  - I `&&` stoppes evalueringen, hvis første betingelse er falsk.
  - I `||` stoppes evalueringen, hvis første betingelse er sand.

```c
if (a > 0 && b > 0) {
    printf("Begge tal er positive.\n");
}
```

**Typisk fejl**: Brug af `=` (tildeling) i stedet for `==` (lighedstest). Eksempel: `if (x = 5)` ændrer værdien af `x` i stedet for at sammenligne.

---

### Udvælgelse med If-Else og Switch

#### If-Else
`If`-sætninger bruges til at udføre kode baseret på en betingelse. 
- Enkelt if: 
  Hvis betingelsen er sand, udføres en specifik blok kode.
- If-Else:
  Giver mulighed for en alternativ handling, hvis betingelsen er falsk.

```c
if (temperature < 0) {
    printf("Det er frostvejr.\n");
} else {
    printf("Ingen frost.\n");
}
```

#### If-Else Kæder
Disse bruges, når der er flere betingelser at teste:
- Kun én blok udføres, når en betingelse er sand.
- Effektiv rækkefølge af betingelser er vigtig for optimal performance.

```c
if (score >= 90) {
    printf("Karakter: A\n");
} else if (score >= 80) {
    printf("Karakter: B\n");
} else {
    printf("Karakter: F\n");
}
```

#### Dangling Else Problemet
Dette opstår, når det ikke er klart, hvilken `if` en `else` hører til. Brug altid `{ }` for at undgå tvetydighed.

#### Switch-Case
Switch-sætninger bruges, når en variabel kan antage mange værdier, og hver værdi kræver forskellig behandling.
- Mere overskueligt end flere if-else kæder.
- Skal afsluttes med `break` for at undgå "fall-through".

```c
switch (menu_choice) {
    case 1:
        printf("Valg: Start spillet\n");
        break;
    case 2:
        printf("Valg: Vis highscore\n");
        break;
    default:
        printf("Ugyldigt valg.\n");
}
```

---

### Iteration og Loops

#### While Løkker
En `while`-løkke gentager en kodeblok, så længe en betingelse er sand. Bruges, når antallet af iterationer ikke er kendt på forhånd.

```c
int i = 0;
while (i < 5) {
    printf("i er: %d\n", i);
    i++;
}
```

#### For Løkker
En `for`-løkke er velegnet til iterationer, hvor antallet af gentagelser er kendt. Den består af tre dele:
- Initialisering: En startværdi sættes.
- Betingelse: Bestemmer, om løkken fortsætter.
- Opdatering: Ændrer værdien efter hver iteration.

```c
for (int i = 0; i < 5; i++) {
    printf("i er: %d\n", i);
}
```

#### Do-While Løkker
Denne løkke udfører altid koden mindst én gang, da betingelsen evalueres efter udførelsen.

```c
int i = 0;
do {
    printf("i er: %d\n", i);
    i++;
} while (i < 5);
```

---

### Sammensætning af Kommandoer

Sammensætning gør det muligt at gruppere flere kommandoer i en blok ved hjælp af `{ }`. Dette bruges ofte i if-else og loops, når flere handlinger skal udføres.

```c
if (x > 0) {
    printf("x er positiv.\n");
    printf("Fortsæt behandlingen.\n");
}
```

---

### Betingede Udtryk
Betingede udtryk giver en kortere måde at skrive simple if-else udtryk på:
- Format: `betingelse ? expression_if_true : expression_if_false`

```c
int max = (a > b) ? a : b;
printf("Største værdi: %d\n", max);
```

---

 `Break`, `Continue` og `Return`

- **`break`**: Afbryder en løkke eller switch.
- **`continue`**: Hopper til næste iteration i en løkke.
- **`return`**: Afslutter en funktion og returnerer en værdi.