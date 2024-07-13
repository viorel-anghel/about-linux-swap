
# WIP work in progress

# About Linux swap

This is an introductory article on the topic of swap with some applications on Linux operating system.

Copyright (2024) Viorel Anghel 

Original link: https://github.com/viorel-anghel/about-linux-swap

## Why we talk about swap?

Noi folosim un system de monitorizare care, intre altele, urmareste si cat de folosit este swap-ul pe masini fizice sau virtuale. 

Recent am decis sa nu mai monitorizam swap-ul pe masinile virtuale, din cateva motive:
- pe majoritatea VM-urilor chiar nu avem swap setat. In primul rand pentru ca daca o masina ajunge sa faca swap, performanta este compromisa grav. In acelasi sens si proiectul Kubernetes recomanda sa disablati swap-ul pe VMurile folosite intr-un cluster de Kubernetes
- problema pe astea pe care nu avem swap setat este ca sistemul de monitorizare trimite o alarma de genul "swap unknown" dar despre asta mai mult la final
- monitorizarea de LOAD average este o indicatie suficient de buna ca ceva nu e in regula pe un VM si trebuie investigat. Ar putea fi folosirea intensa a swap-ului sau altceva care va creste LOAD average-ul.

## Using top

In imaginea de mai jos este un screenshot (partial) al comnenzii `top` pe un VM cu Linux.

![Screenshot top](Screenshot-top-swap.png)

Am marcat cu rosu doua zone de interes:


## What is swap



## Monitorizare Nagios check-swap

