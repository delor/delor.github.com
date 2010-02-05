---
layout: post
title: Obsługa wejścia/wyjścia i systemu plików
category: pas
---
*   [Wbudowane operacje we/wy](http://docs.python.org/library/functions.html) cd.
    *   raw_input
    *   open
    *   [metody plikowe](http://docs.python.org/library/stdtypes.html#file-objects)
        *   close, flush, read, readline, readlines, seek, tell, write, writelines
*   [Moduł os](http://docs.python.org/library/os.html#module-os)
    *   chdir, mkdir, makedirs, remove, unlink, removedirs, rename, rmdir, stat
*   [Moduł os.path](http://docs.python.org/library/os.path.html#module-os.path)
    *   abspath, basename, dirname, exists, expanduser, splitext
*   [Obsługa argumentów linii poleceń](http://diveintopython.org/scripts_and_streams/command_line_arguments.html)
    *   moduł [getopt](http://docs.python.org/library/getopt.html#module-getopt)
    *   moduł [optparse](http://docs.python.org/library/optparse.html#module-optparse)

<div class="question">
  <p>Napisać program wyświetlający na standardowym wyjściu plik zadany w
  wierszu poleceń.</p>
  <ul>
    <li><a href="http://docs.python.org/library/stdtypes.html#file-objects">
        File Objects</a></li>
    <li><a href="http://diveintopython.org/file_handling/file_objects.html">
        Dive Into Python - Working with File Object</a></li>
  </ul>
</div>

<div class="answer">
<pre class="brush: python; collapse: true">
import sys

file = sys.argv[1]
file = open(file)
sys.stdout.write(file.read())
file.close()
</pre>
</div>

<div class="question">
  <p>Napisać program kopiujący plik zadany pierwszym parametrem wiersza poleceń
  na plik zadany drugim parametrem wiersza poleceń.</p>
</div>

<div class="answer">
<pre class="brush: python; collapse: true">
#!/usr/bin/env python
# -*- coding: utf-8 -*-

import sys


try:
    source_file = sys.argv[1]
    destintion_file = sys.argv[2]

    source_file = open(source_file, 'r')
    destintion_file = open(destintion_file, 'w')

    destintion_file.write(source_file.read())
except IndexError, err:
    print >> sys.stderr, err
except IOError, err:
    print >> sys.stderr, err
</pre>
</div>

<div class="question">
  <p>Pliki mp3 oprócz muzyki mogą zawierać dodatkowe informacje o utworze w
     postaci etykiet (tagów) typu ID3v1 lub ID3v2. Etykieta ID3v1 zajmuje
     ostatnie 128 bajtów w pliku i zawiera następujące informacje
     (w tej kolejności):</p>
  <ul>
    <li>3 bajty - napis „TAG”</li>
    <li>30 bajtów - tytuł utworu</li>
    <li>30 bajtów - artysta</li>
    <li>30 bajtów - tytuł albumu</li>
    <li>4 bajty - rok (jako czteroliterowy napis)</li>
    <li>30 bajtów - komentarz</li>
    <li>1 bajt - gatunek</li>
  </ul>
  <p>Pola są uzupełniane znakami pustymi (ASCII 0) do wymaganej długości.</p>
  <p>Napisać program, który dostaje w parametrze nazwę pliku. Jeżeli plik
     zawiera etykietę ID3v1 to program wyświetla informacje o utworze.</p>
  <ul>
    <li>ID3.org, ID3v1</li>
    <li>Kody gatunków ID3</li>
  </ul>
</div>

<div class="answer">
<pre class="brush: python; collapse: true">
#!/usr/bin/env python
# -*- coding: utf-8 -*-

import sys


genres = { 0: 'Blues', 1:'Classic Rock', 2: 'Country', 3: 'Dance', 4: 'Disco',
          5: 'Funk', 6: 'Grunge', 7: 'Hip-Hop', 8: 'Jazz', 9: 'Metal',
          10: 'New Age', 11: 'Oldies', 12: 'Other', 13: 'Pop', 14: 'R&B',
          15: 'Rap', 16: 'Reggae', 17: 'Rock', 18: 'Techno', 19: 'Industrial',
          20: 'Alternative', 21: 'Ska', 22: 'Death Metal', 23: 'Pranks',
          24: 'Soundtrack', 25: 'Euro-Techno', 26: 'Ambient', 27: 'Trip-Hop',
          28: 'Vocal', 29: 'Jazz+Funk', 30: 'Fusion', 31: 'Trance',
          32: 'Classical', 33: 'Instrumental', 34: 'Acid', 35: 'House',
          36: 'Game', 37: 'Sound Clip', 38: 'Gospel', 39: 'Noise',
          40: 'AlternRock', 41: 'Bass', 42: 'Soul', 43: 'Punk', 44: 'Space',
          45: 'Meditative', 46: 'Instrumental Pop', 47: 'Instrumental Rock',
          48: 'Ethnic', 49: 'Gothic', 50: 'Darkwave', 51: 'Techno-Industrial',
          52: 'Electronic', 53: 'Pop-Folk', 54: 'Eurodance', 55: 'Dream',
          56: 'Southern Rock', 57: 'Comedy', 58: 'Cult', 59: 'Gangsta',
          60: 'Top 40', 61: 'Christian Rap', 62: 'Pop/Funk', 63: 'Jungle',
          64: 'Native American', 65: 'Cabaret', 66: 'New Wave',
          67: 'Psychadelic', 68: 'Rave', 69: 'Showtunes', 70: 'Trailer',
          71: 'Lo-Fi', 72: 'Tribal', 73: 'Acid Punk', 74: 'Acid Jazz',
          75: 'Polka', 76: 'Retro', 77: 'Musical', 78: 'Rock & Roll',
          79: 'Hard Rock' }

try:
    mp3_file = sys.argv[1]
    mp3_file = open(mp3_file)
    mp3_file.seek(-128, 2)
    #print mp3_file.read(128)
    #sys.exit(1)
    tag = mp3_file.read(3)
    print tag
    if tag in ('TAG', 'ID3'):
        tag = {}
        tag['title'] = mp3_file.read(30).strip()
        tag['artist'] = mp3_file.read(30).strip()
        tag['album'] = mp3_file.read(30).strip()
        tag['year'] = mp3_file.read(4).strip()
        tag['comment'] = mp3_file.read(30).strip()
        genre = ord(mp3_file.read(1))
        try:
            tag['genre'] = genres[genre]
        except KeyError:
            tag['genre'] = 'undefined/unknown'
        print tag
        print """
        title = %(title)s
        artist = %(artist)s
        album = %(album)s
        year = %(year)s
        comment = %(comment)s
        genre = %(genre)s
        """ % tag

except IndexError, err:
    print err
except IOError, err:
    print err
</pre>
</div>

<div class="question">
  <p>Napisać program dostający w parametrze wiersza poleceń nazwę katalogu
     i wyświetlający na standardowym wyjściu wszystkie podkatalogi znajdujące
     się bezpośrednio w nim - każdy w osobnym wierszu. W przypadku jakiegoś
     błędu odpowiedni komunikat powinien zostać wyświetlony na standardowym
     wyjściu błędów i program powinien zakończyć się z kodem błędu różnym od
     zera.</p>
  <ul>
    <li>Files and Directories</li>
    <li>Moduł os.path</li>
    <li>Dive Into Python (Working with Directories) (po polsku)</li>
    <li>Errors and Exceptions</li>
    <li>Funkcja sys.exit()</li>
  </ul>
</div>

<div class="question">
  <p>Zmodyfikować program z zadania nr 4 tak, aby w przypadku otrzymania opcji
     -r program wyświetlał także (najlepiej z odpowiednim wcięciem) podkatalogi
     wszystkich wyświetlanych katalogów.</p>
  <pre><code>$ ./my_ls.py kat
kat1
kat2
  podkat21
  podkat22
kat3
  podkat31
    podpodkat311
  podkat32
    podpodkat321
    podpodkat322
kat4</code></pre>
</div>

<div class="question">
  <p>Napisać program wyświetlający na standardowym wyjściu informację o
     rozmiarze pliku zadanego w parametrze wiersza poleceń, np.:</p>
  <pre><code>$ ./rozm.py plik.txt
plik.txt 2345678</code></pre>
  <p>Program obsługuje następujące opcje:</p>
  <ul>
    <li>-h, --help - wyświetla krótką informację o tym co program robi i jak go
        używać (m. in. wymienia opcje), a następnie kończy działanie</li>
    <li>-o plik - zapisuje informacje do pliku plik zamiast wyświetlać je na
        standardowym wyjściu</li>
    <li>-s - informacja o rozmiarze wyświetlona jest w przybliżeniu i z
        odpowiednią jednostką (np. 234B, 23K, 345M, 4G)</li>
    <li>-r - jeżeli w parametrze zostanie podany katalog, to wyświetlany jest
        łączny rozmiar plików w tym katalogu i jego podkatalogach</li>
  </ul>
  <ul>
    <li>Moduł getopt</li>
    <li>Moduł optparse</li>
  </ul>
</div>

<script type="text/javascript">
    SyntaxHighlighter.all()
</script>
