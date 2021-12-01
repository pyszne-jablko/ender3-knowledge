
# PID drukarki 3D na Ender3 z SKR Mini E3 V2

Aplikacja ```pronterface```. 

```M303 C5 S215``` z filmiku pod linkiem [1]. HotEnd był wypełniony filamentem.

Ja wpisałem ```M303 C5 S230``` ze względu, że planuję drukować głównie z PET-G,
gdzie temperatura dyszy jest wyższa niż w przypadku PLA.

Opis:
- ```M303``` Komenda autokalibracji PID;
- ```C5``` ilość powtórzeń. Ile cykli będzie przeprowadzonych;
- ```S230``` zadana temperatura docelowa, w tym przypadku 230 stopni Celsjusza.

Jak wpisałem na rozgrzanej dyszy to uzyskałem wartości:
```
#define DEFAULT_Kp 20.31
#define DEFAULT_Ki 1.77
#define DEFAULT_Kd 58.22
```

Następnie wpisałem tą samą komendę z tą różnicą, że dysza była w temperaturze
pokojowe. Wtedy uzyskłem wartości:
```
#define DEFAULT_Kp 19.62
#define DEFAULT_Ki 1.68
#define DEFAULT_Kd 57.42
```

I właśnie te wartości wprowadzę do drukatki następującą komendą
```M301 p19.62 i1.68 d57.42```. Komenda jako argumenty przyjmuje kolejne
wartości współczynników P, I oraz D po odpowiednich literkach z przodu.

Na koniec należy zapisać ustawienia w pamięci EEPROM komendą ```M500```. To
spowoduje użycie ich po ponownym włączeniu drukarki.

Można to przetestować wyłączając, a następnie po krótkiej chwili włączając
drukarkę z sieci oraz z portu USB, a następnie po wpisaniu komendy ```M503```
sprawdzić czy zostały zapamiętane poprawne wartości.

# TODO

Można także dostroić PID dla grzanego stołu, w tym przypadku należy w komendzie
```M303``` wpisać ```E-1 S60```, a do wprowadzenia wartości użyć komendę ```M304```.

# Inne przydatne komendy

```M503``` wypisanie aktualnych ustawień

# Linki

[1] Filmik instruktarzowy https://www.youtube.com/watch?v=jVcIt7nFaks

[2] Komendy GCODE dla Marlin-a https://marlinfw.org/docs/gcode/M303.html
