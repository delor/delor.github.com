---
layout: post
title: Argumenty wiersza poleceń i zmienne środowiskowe
category: pas
---
*   argumenty wiersza poleceń: lista [sys.argv]("http://docs.python.org/library/sys.html#sys.argv" "sys.argv — System-specific parameters and functions — Python documentation")
*   zmienne środowiskowe: słownik os.environ
*   Wbudowane operacje we/wy
    *   print
* moduł [sys]("http://docs.python.org/library/sys.html" "sys — System-specific parameters and functions — Python documentation")

## Zadania ##

<div class="question">
<p>Napisać program wyświetlający w czytelnej postaci swoją nazwę i wszystkie argumenty wiersza poleceń, np.:</p>
<pre>
<code>
$ python program.py -a 'Cos tam'
nazwa programu: './program.py'
argument nr 1: '-a'
argument nr 2: 'Cos tam'
</code>
</pre>
<ul>
<li><a href="http://diveintopython.org/scripts_and_streams/command_line_arguments.html">Dive Into Python - Handling command-line arguments</a></li>
</ul>
</div>

<div class="answer">
{% highlight python%}
import sys

print 'nazwa programu:', sys.argv[0]
ilosc_argumentow = len(sys.argv)
for numer in range(1, ilosc_argumentow):
    print 'argument nr %i: %s' % (numer, sys.argv[numer])
{% endhighlight %}
</div>

<div class="question">
<p>Napisać program, który dla każdej z zadanych w parametrach wiersza poleceń zmiennych środowiskowych wyświetli w osobnym wierszu napis postaci NAZWA=WARTOŚĆ, np.:</p>
<pre>
<code>
$ env ABC=abc
$ ./program.py HOME ABC
HOME=/home/mklisow
ABC=abc
</code>
</pre>
<p>Jeżeli któraś z wymienionych zmiennych nie jest zdefiniowana, to program ma tylko wyświetlić informację o tym na standardowym wyjściu błędów i zakończyć działanie z kodem błędu będącym niewielką liczbą całkowitą większą od zera.</p>
<ul>
<li><a href="http://docs.python.org/library/os.html#process-parameters">Process Parameters</a></li>
<li><a href="http://diveintopython.org/scripts_and_streams/stdin_stdout_stderr.html">Dive Into Python - Standard input, output, and error</a></li>
</ul>
</div>

<div class="answer">
{% highlight python %}
import sys
import os

for zmienna in sys.argv[1:]:
    try:
        print '%s=%s' % (zmienna, os.environ[zmienna])
    except KeyError, err:
        print >> sys.stderr, 'zmienna %s nie jest ustawiona' % err
        sys.exit(1)
{% endhighlight %}
</div>
