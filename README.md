# Bankobot

Kod odnosi się do robota "Bańkobot". Robot ze szwedzkimi kołami, czasami występujący z pistoletem do robienia baniek na korpusie. <br/> 

Kod jest na platrofmę arduino. Obecnie w robocie znajduje się Arduino Mega. <br/> 

Program odczytuje sygnał z odbiornika RC (Flysky). Obecnie odczytuje 5 kanałów. Trzy z nich odpowiadają za ruchy a dwa  <br/>
za włączanie pistoletu i wiatraka. Następnie w funkcjach warunkowych sprawdza się stan poszczególncych kanałów i w zależności od tego <br/>
czy na danym kanale zmienia się sygnał robot się porusza. W tej chwili ruch jest binarny. Nie korzysta się z wejścia PWM na mostakch <br/>
(oznacza to, że robot zawsze jeździ z pełną prędkością). <br/> 

Rozwój projketu: 
-wykorzystać wejście PWM na mostkach <br/>
-podłączyć i okodować enkodery
 

Osoba odpowiedzialna za projekt:
Kamil Goś 
