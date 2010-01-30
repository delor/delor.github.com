---
layout: post
title: Wstęp do programowania w języku Python
category: pas
---
## Python — uruchamianie interpretera ##

*   interaktywne: `python`
*   wsadowe (nieinteraktywne): `python nazwa_pliku`
*   automatyczne przez powłokę
    pierwszy wiersz pliku: `#!/usr/bin/env python` oraz `chmod a+x plik` aby plik był uruchamialny

## Python — specyfika języka ##

*   komentarze `#` jak w powłoce
*   obowiązkowe wcięcia (zamiast begin...end) standard pep8 definiuje 4 spacje na wcięcie
*   specyficzne operatory:
    *   `**` - potęga
    *   `*` - mnożenie, powielanie
    *   `//` - dzielenie całkowite
    *   `%` - modulo, formatowanie napisów
    *   `+` - dodawanie, łączenie
    *   `==`, `!=` - równe, różne
    *   `x > y >= z` - łańcuchy porównań
    *   `in`, `not in` - należy, nie należy
    *   `and`, `or` (uwaga na zwracane wartości!)
*   podstawienia z operacją: `+=`, `-=`, `*=`, `/=`, `%=`, `**=`, ...
*   wszystko jest obiektem
*   mocna kontrola zgodności typów danych (mimo dynamicznie ustalonego typu danej), konwersja do napisu (funkcja str)
*   obowiązek inicjowania zmiennej
*   specyficzne typy danych: słowniki, listy, krotki
*   mapowanie i filtrowanie list
*   moduły (`import moduł`, `from moduł import obiekty`, funkcja `dir`)
*   wyjątki
        try:
            # kod, który może spowodować wystąpienie wyjątku
        except:
            # kod obsługujący wyjątek
        else:
            # kod, który zostanie wykonany gdy nie wystąpił wyjątek
        finally:
            # kod, który zawsze zostanie wykonany
    `raise` wyrzuca wyjątek

## Zadania ##

<div class="question">
<p>Napisać na trzy sposoby standardowy program wypisujący "Hello world!" (interaktywnie, wsadowo i jako skrypt).</p>
</div>

<div class="question">
<p>Napisać funkcję, która dla dwóch argumentów całkowitoliczbowych znajdzie ich największy wspólny dzielnik.</p>
</div>
