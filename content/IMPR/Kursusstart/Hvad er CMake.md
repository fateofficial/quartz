CMake er et build system til blandt andet C og C++ 

**Building** 
- Holder styr på hvilke filer der er i vores projekt 
- Hjælper med at kalde compileren, vi behøver ikke længere huske at skrive gcc -o outputFil inputFil.c gcc -ansi -pendatic -Wall -lm -g inputFil.c 
- arbejder pænt sammen med CLion - specielt anvendeligt til større projekter - anvendt i industrien 
**Testing**
- Vi kan tilføje automatiske test 
**Cross compilation/ Dependency management** 
- gør det nemmere at få programmer til at compile på både windows, mac og linux
- gør det nemmere at genbruge programstumper