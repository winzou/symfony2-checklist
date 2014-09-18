Własne strony błędów
podstawowe
Standardowe strony błędów wyświetlane w środowisku developerskim nie są, na szczęście, wyświetlane w środowisku produkcyjnym. Dlatego też należy stworzyć swoje własne strony  błędów - dostosowane  do wyglądu aplikacji .

Stworzenie własnych stron błędów  jest bardzo proste. Widoki stron błędów znajdują się w paczce `TwigBundle`,  co daje bezpośrednia  możliwość zastąpienia  ich swoimi. 
Widoki powinny się  znajdować : `Exception/errorXXX.html.twig`, gdzie `XXX` to numer błędu. Zaleca się  przede wszystkim  zmodyfikować/zastąpić  widoki dla  błędów 404 (nie znaleziono)  i 500 (błąd serwera).

Użyć  własnych  widoków  błędu można na  dwa sposoby:

1. Stworzyć  nową  paczkę  która  rozszerza `TwigBundle`, i umieścić widoki w `Resources/views/Exception/errorXXX.html.twig`. Takie rozwiązanie  umożliwia wielokrotne  użycie tych samych widoków w wielu projektach ( poprzez  użycie tej paczki w projektach) .;
2. Możesz po prostu umieścić widoki w  `app/Resources/TwigBundle/views/Exception/errorXXX.html.twig`. To rozwiązanie pozwala  używać widoki błędu dostosowane do konkretnego projektu, bez tworzenia  nowej paczki(bundla) .

* _Zobacz [Customize error pages on Symfony documentation](http://symfony.com/doc/master/cookbook/controller/error_pages.html)_