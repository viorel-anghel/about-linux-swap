
# WIP work in progress

# About Linux swap

This is an introductory article on the topic of swap with some applications on Linux operating system.

Copyright (2024) Viorel Anghel 

Original link: https://github.com/viorel-anghel/about-linux-swap

## What is Unix/Linux swap

## Why do we talk about swap?

Noi folosim un system de monitorizare care, intre altele, urmareste si cat de folosit este swap-ul pe masini fizice sau virtuale. 

Recent am decis sa nu mai monitorizam swap-ul pe masinile virtuale, din cateva motive:
- pe majoritatea VM-urilor chiar nu avem swap setat. In primul rand pentru ca daca o masina ajunge sa faca swap, performanta este compromisa grav. In acelasi sens si proiectul Kubernetes recomanda sa disablati swap-ul pe VMurile folosite intr-un cluster de Kubernetes
- problema pe astea pe care nu avem swap setat este ca sistemul de monitorizare trimite o alarma de genul "swap unknown" dar despre asta mai mult la final
- monitorizarea de LOAD average este o indicatie suficient de buna ca ceva nu e in regula pe un VM si trebuie investigat. Ar putea fi folosirea intensa a swap-ului sau altceva care va creste LOAD average-ul.

## Swap commands

TBD

## Setting up swap

TBD

## Using top

In imaginea de mai jos este un screenshot (partial) al comnenzii `top` pe un VM cu Linux.

![Screenshot top](Screenshot-top-swap.png)

Am marcat cu rosu doua zone de interes:
- in partea unde scrie *MiB Swap:* - este self-explanatory, cati MB se Swap avem in total, liberi si folositi. In acest caz particular, masina nu are swap.
- mai interesant, zona unde scrie *0.0 wa* - inseamna cat procent CPU este in starea "wait for I/O", adica procesorul asteapta dupa operatii de I/O, in mod usual disk. Asta nu este neaparat swap, poate fi activitate intensa de scriere/citire pe disk. Dar poate fi si swap

As a side note, ar trebui sa stiti foarte clar tot ce scrie pe linia *%CPU* din comanda top. Pe scurt, sunt proceente din timpul folosit de procesor pentru:
- us = user processes (i.e. non-kernel)
- sy = system processes (i.e kernel)
- ni = nice - procese (user space) cu prioritate non-default
- id = idle - provcesorul sta degeaba
- wa = tocmai am explicat, wait for i/o
- hi = hardware interrupts
- si = software interrupts
- st = stolen from this vm by the hypervisor

Cum putem sti toate astea? Simplu, `man top`. Cele la care ma uit primele sunt `id` si `wa`.

# Using vmstat

Pana acum nu avem o comanda care sa indice clar daca se face activitate de scriere / citire pe swap. Cea pe care o folosesc eu frecvenrt este `vmstat` cu argumentele `-n 1` care inseamna ca arata periodic, la fiecare 1 secunda informatiile:

![Screenshot vmstat](Screenshot-vmstat.png)

Evident, pentru ce discutam, coloana *swap* este de interes. *si* inseamna swap in, adica blocuri transferate din memorie pe disk. *so* inseamna swap out, adica blocuri aduse de pe disk (swap) in memorie pentru a fi folosite. 
PE un sistem care face swap, rata de modificare in timp la *so* este parametrul important de urmarit, in ideea ca swap in nu este grav cata vreme nu se produce mult swap out.

Pentru celelalte numere si informatii din screenshotul de mai sus, sper ca deja stiti, `man vmstat`. Unii parametri sunt aceeasi ca si la top (cpu / us sy id wa st).

## Swappiness

TBC

## Monitorizare Nagios check-swap

