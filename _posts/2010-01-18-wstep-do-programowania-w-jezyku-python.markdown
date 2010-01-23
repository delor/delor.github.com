---
layout: post
title: Wstęp do programowania w języku Python
---
## Python — uruchamianie interpretera ##

*   interaktywne: python
*   wsadowe (nieinteraktywne): python nazwa_pliku
*   automatyczne (przez powłokę):
*   pierwszy wiersz pliku: `#!/usr/bin/python` (w zależności od realnego umiejscowienia interpretera w systemie plików, co można sprawdzić przez which python) oraz
*   `chmod a+x plik` (aby plik był uruchamialny)

## Python — specyfika języka ##

*   komentarze # jak w powłoce
*   obowiązkowe wcięcia (zamiast begin...end)
*   specyficzne operatory:
    *   `**` (potęga)
    *   `*` (mnożenie, powielanie)
    *   `//` (dzielenie całkowite)
    *   `%` (modulo, formatowanie napisów)
    *   `+` (dodawanie, łączenie)
    *   `==`, `!=` (równe, różne)
    *   `x > y >= z` (łańcuchy porównań)
    *   `in`, `not in` (należy, nie należy)
    *   `and`, `or` (uwaga na zwracane wartości!)
*   podstawienia z operacją: `+=`, `-=`, `*=`, `/=`, `%=`, `**=`, ...
*   wszystko jest obiektem
*   mocna kontrola zgodności typów danych (mimo dynamicznie ustalonego typu danej), konwersja do napisu (funkcja str)
*   obowiązek inicjowania zmiennej
*   specyficzne typy danych: słowniki, listy, krotki
*   mapowanie i filtrowanie list
*   moduły (import moduł, from moduł import obiekty, funkcja dir)
*   wyjątki (try...except...[else...][finally...], try...finally..., raise, IOError, ImportError, KeyError)
