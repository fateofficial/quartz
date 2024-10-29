En compiler analyserer et kildeprogram, og transformerer det til en form som kan fortolkes (køres) 

**Analyse** 
- Finder fejl inden programmet transformeres og køres - Syntaxfejl eller typefejl, men ikke logiske fejl 
**Transformation** 
- Oversætter programmet, typisk til maskinnær kode 
**Options** 
- Styrer forskellige compiler variationer 
- Parametre til compileren 
- Eksempler på anvendelse af *gcc options* 
*gcc -o outputFil inputFil.c gcc -ansi -pedantic -Wall -lm -g inputFil.c*