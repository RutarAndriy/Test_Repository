# Test_Repository

```2-Dimensional-Array
Українська	2
      Active Layer	      Активний шар
      AutoSnap	      Автозахоплення
      Layer	      Шар
     Distance	     Відстань
    Parameters	    Параметри
 (portrait)	 (портрет)
```
```NSIS
ShowHeader=1
Left=1086
Top=55
Width=96
Height=32
FontSize=6
ButtonSize=32
Background=-16777201
Margin=0
Gap=0
Alpha=255
Layout=0
Visible=0
Anchor=1
Names=A,T,Z

;Перевірка відкритих карт
$mapCount=@MapCount
@if ($mapCount=0) then @break Немає відкритих карт
;Встановлення робочої папки
$workFolder=@WorkFolder
;Вибір файлу
$fileName=@Dialog.OpenFile *.tdf $workFolder
@if $fileName= then @break
;Ім'я оброблювального файлу
$shortName=@ExtractFileName $fileName
;Завантаження даних у текстовий масив
@Text.Load $fileName
;Кількість точок у масиві
$count=@Text.Count
;Порядковий індекс обробки
$index=1
;Кількість точок у файлі
$pointCount=0
;
;Цикл
%process
;
;Отримання строки
$coord=@Text.Line[$index]
$index=$index+1
$ne=@Text.Line[$index]
$index=$index+1
$sw=@Text.Line[$index]
$index=$index+1
;
$x=@StringPart 3 $coord
$x=@Calc Replace("$x",",","")
$x=@DequoteText $x
;
$y=@StringPart 5 $coord
$y=@Calc Replace("$y",",","")
$y=@DequoteText $y
;
$z=@StringPart 7 $coord
$z=@Calc Replace("$z","]","")
$z=@DequoteText $z
;
$NEx=@StringPart 2 $ne
$NEx=@Calc Replace("$NEx",",","")
$NEx=@DequoteText $NEx
$NEx=@Calc Replace("$NEx","[","")
$NEx=@DequoteText $NEx
;
$NEy=@StringPart 3 $ne
$NEy=@Calc Replace("$NEy","]","")
$NEy=@DequoteText $NEy
;
$SWx=@StringPart 2 $sw
$SWx=@Calc Replace("$SWx",",","")
$SWx=@DequoteText $SWx
$SWx=@Calc Replace("$SWx","[","")
$SWx=@DequoteText $SWx
;
$SWy=@StringPart 3 $sw
$SWy=@Calc Replace("$SWy","]","")
$SWy=@DequoteText $SWy
;
;@Dialog.Message $NEx|$NEy|$SWx|$SWy
;
$obj1=@Map.AddObject 0|1|ID11900000|4|0 $NEx $SWy 0|0 $SWx $SWy 0|0 $SWx $NEy 0|0 $NEx $NEy 0|;
;
;
;Отримання координат
;$name=@StringPart 1 $line
;$x=@StringPart 2 $line
;
$pointCount=$pointCount+1
;
;Створення об'єкту
;$obj=@Map.AddObject 0|1|ID11330000|1|0 $x $y $z|1|ID11330000|2|37 $name|9 $label|
;
;Підписування об'єкту
;@Map.Object[$obj].CreateCaption 37 0 0 1 1 1 0.5
;
;Первірка умови циклу
;
@if $index<=$count then @goto %process
;
;Переведення системи коорднат
;@SendChars <CR>
;@ExecuteMenu MapReferenceSystem
;
;Виділення об'єктів
;@Map.SelectLayer ID11330000
;
;Інформаційне повідомлення
;@Dialog.Message Файл $shortName завантажено.|Кількість пікетів $pointCount.

@Dialog.Message Test

@Dialog.Message Hello
```
