# File-Handling

- [Einführung](#einfuehrung)
- [rex_file](#rexfile)
  - [get](#rexfile_get)
  - [getConfig](#rexfile_getConfig)
  - [getCache](#rexfile_getCache)
  - [put](#rexfile_put)
  - [putConfig](#rexfile_putConfig) 
  - [putCache](#rexfile_putCache)
  - [copy](#rexfile_copy) 
  - [rename](#rexfile_rename) 
  - [delete](#rexfile_delete) 
  - [extension](#rexfile_extension) 
  - [mimeType](#rexfile_mimeType) 
  - [formattedSize](#rexfile_formattedSize)
  - [getOutput](#rexfile_getOutput) 
- [rex_dir](#dir)
  - [create](#create)
  - [isWritable](#isWritable)
  - [copy](#copy)
  - [delete](#delete)
  - [deleteFiles](#deleteFiles)
  - [deleteIterator](#deleteIterator)


<a name="rexfile"></a>
## rex_file

Die Class rex_file kümmert sich um das Handling einzelner Dateien. Hier stehen Methoden zum Einlesen, Schreiben und zur Ausgabe von Dateien im Dateisystem zur Verfügung. 

[Quellcode auf GitHub](https://github.com/redaxo/redaxo/blob/master/redaxo/src/core/lib/util/file.php)  



<a name="rexfile_get"></a>
### rex_file::get
Mit der Methode `get` wird eine Datei aus dem Dateisystem eingelesen. Ein weiterer Parameter erlaubt die Ausgabe eines Default-Wertes bzw. Fehlermedlung (wenn nicht festgelegt NULL), wenn die Datei nicht gelesen werden kann.  

```php
rex_file::get($file, $default = null)
```

Beispiel: 

```php
$data = rex_file::get(rex_path::frontend('/assets/styles.css'),'not available');
```


<a name="rexfile_getConfig"></a>
### rex_file::getConfig

Mit der Methode `getConfig` kann eine Config-Datei eingelesen werden. Kann die Datei nicht gelesen werden, kann ein Default-Wert zurückgegeben werden.  

> Die Methode wird hauptsächlich vom Core verwendet. AddOns sollten auf die Möglichkeiten der package.yml und rex_config zurückgreifen. 

```php 
getConfig($file, $default = [])
```

Beispiel: Einlesen der REDAXO Config

```php
$config = rex_path::coreData('config.yml');
```

### rex_file::getCache
<a name="rexfile_getCache"></a>

Mit der Methode `getCache` wird eine Datei aus dem Cache eingelesen. Ein weiterer Parameter erlaubt die Ausgabe eines Default-Wertes bzw. Fehlermedlung (wenn nicht festgelegt NULL), wenn die Datei nicht gelesen werden kann.  

```php
getCache($file, $default = [])
```


### rex_file::put
<a name="rexfile_put"></a>

Mit der Methode `put` schreibt Content in eine Datei. Existiert die Datei noch nicht, wird sie erstellt. Rie Rückgabe bei Erfolg ist TRUE, sonst FALSE. Vorhandene Inhalte der Datei werden überschriben.  

```php
put($file, $content)
```

Beispiel: 

```php
$css = 'body { background: #eee;}
p { line-height: 1.2em;}
';
$success = rex_file::put(rex_path::frontend('/assets/new_styles.css'),$css)
```




### rex_file::putConfig
<a name="rexfile_putConfig"></a>

Die Methode `putConfig` schreibt Konfigurationsdaten in eine Config-Datei. Die Rückgabe bei Erfolg ist TRUE, sonst FALSE. 

> Die Methode wird hauptsächlich vom Core verwendet. AddOns sollten auf die Möglichkeiten der package.yml und rex_config zurückgreifen. 

```php
putConfig($file, $content)
```



### rex_file::putCache
<a name="rexfile_putCache"></a>

Die Methode `putCache` schreibt Daten in den Cache. Bei Erfolg TRUE, sonst FALSE.

```php
putCache($file, $content)
```

Beispiel: 

```php 
$content = '
Dies ist ein Typoblindtext. An ihm kann man sehen, ob alle Buchstaben da sind und wie sie aussehen. 
';
rex_file::putCache(rex_path::addonCache('meinaddon').'blindtext.txt',$content);
```

Der gecachte Inhalt kann dann mit `getCache` abgerufen werden: 

```php
echo (rex_file::getCache(rex_path::addonCache('meinaddon').'blindtext.txt'));
```

<a name="rexfile_copy"></a>
### rex_file::copy

Die Methode copy ermöglicht das Kopieren einer einer Datei zu einem Verzeichnis oder Datei. Es müssen eine Quell- und ein Zielpfad eingegeben werden. Die Rückgabe bei Erfolg ist TRUE, sonst FALSE. 

```php
rex_file::copy($srcfile, $dstfile)
```


<a name="rexfile_move"></a>
### rex_file::move

Die Methode move ermöglicht das Verschieben einer einer Datei. Es müssen ein Quell- und ein Zielpfad eingegeben werden. Die Rückgabe bei Erfolg ist TRUE, sonst FALSE. 

```php
rex_file::move($srcfile, $dstfile)
```

<a name="rexfile_delete"></a>
### rex_file::delete

Die Methode `delete` ermöglicht das Löschen einer einer Datei. Es müssen ein Quell- und ein Zielpfad eingegeben werden. Die Rückgabe bei Erfolg ist TRUE, sonst FALSE. 

```php
rex_file::delete($file)
```

<a name="rexfile_extension"></a>
### rex_file::extension

Die Methode `extension` liefert als Rückgabe die Dateiendung einer Datei. 

```php
rex_file::extension($file)
```


<a name="rexfile_mimeType"></a>
### rex_file::mimeType

Die Methode `mimeType` liefert den MimeTyp einer Datei. 

```php
$extension = rex_file::mimeType($file);
```

z.B.:
- application/javascript
- image/svg+xml
- video/mpeg

<a name="rexfile_formattedSize"></a>
### rex_file::formattedSize

Die Methode formattedSize liefert eine benutzerfreundliche Ausgabe der Dateigröße einer Datei

```php
$filesize = rex_file::formattedSize($file);
```



<a name="rexfile_getOutput"></a>
### rex_file::getOutput

getOutput führt die angegebene Datei aus und gibt das Ergebnis aus. 

```php
getOutput($file)
```