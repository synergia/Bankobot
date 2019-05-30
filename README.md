# Bankobot

Kod odnosi się do robota "Bańkobot". Robot ze szwedzkimi kołami, czasami występujący z pistoletem do robienia baniek na korpusie. <br/> 

Kod jest na platrofmę arduino. Obecnie w robocie znajduje się Arduino Mega. <br/> 

Program odczytuje sygnał z odbiornika RC (Flysky). Obecnie odczytuje 5 kanałów. Trzy z nich odpowiadają za ruchy a dwa 
za włączanie pistoletu i wiatraka. Następnie w funkcjach warunkowych sprawdza się stan poszczególncych kanałów i w zależności od tego 
czy na danym kanale zmienia się sygnał robot się porusza. W tej chwili ruch jest binarny. Nie korzysta się z wejścia PWM na mostakch
(oznacza to, że robot zawsze jeździ z pełną prędkością). <br/> 

Sterowanie robotem:
Krok 1. Włączyć aparaturę. Lewy drążek musi znajdować się w maksymalnie dolnej pozycji. Wszystkie przełączniki ustawione do góry. <br/>
Krok 2. Włączyć robota poprzez odbezpieczenie przycisku awaryjnego <br/>
Krok 3. Poruszając prawym drążkiem powodujemy ruch do przdu/tyłu i w prawo/lewo. Ruszając lewym obracamy robota wokół własnej osi.
Krok 4. W celu wyłączenia robota wciskamy przycisk awaryjny co całkowicie odcina dopływ prądu. Następnie wyłączamy kontroler. 
 


Rozwój projketu: 
-wykorzystać wejście PWM na mostkach <br/>
-podłączyć i okodować enkodery
 

Osoba odpowiedzialna za projekt:
Kamil Goś 
