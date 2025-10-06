---
sidebar_position: 2
id: quick-start-vth-keten
title: Quick-Start Indienen
slug: /plan-keten/quick-start-vth-keten
---

# Quick-Start Indienen

Een groot deel van de werking van het DSO is gebaseerd op basis van juridische activiteiten uit omgevingsdocumenten. Op het moment dat deze activiteiten zijn geannoteerd en daarna toepasbaar zijn gemaakt, kunnen er voor die activiteiten via het DSO-LV aanvragen of meldingen ingediend worden. 

Dat indienen werkt via een reeks van API's, die in een bepaalde volgorde gebruikt moeten worden. Het is daarbij praktisch om kennis van [DMN](https://en.wikipedia.org/wiki/Decision_Model_and_Notation) te hebben omdat dit helpt om de informatie, die uit de bevragingen van de API's komt, te kunnen verwerken en op de juiste manier te kunnen afhandelen.

Omdat activiteiten aan locaties zijn gekoppeld is noodzakelijk om gebruik te maken van een dienst die iets als lengte/breedte coördinaten om te zetten naar [Rijksdriehoekscoördinaten](https://nl.wikipedia.org/wiki/Rijksdriehoeksco%C3%B6rdinaten). Daarnaast zijn er een [API-key voor het DSO](https://developer.omgevingswet.overheid.nl/formulieren/api-key-aanvragen-0/) nodig, een [PKIoverheidcertificaat](https://www.logius.nl/onze-dienstverlening/toegang/pkioverheid/wat-een-pkioverheidcertificaat) en moet uw organisatie geprovisioned worden binnen de DSO systemen van Rijkswaterstaat.  

## Hoe werkt het proces van Indienen?

1. Op basis van de RD-coördinaten roept u de [Omgevingsdocument Toepasbaar opvragen](https://developer.omgevingswet.overheid.nl/api-register/api/omgevingsdocument-toepasbaar-opvragen/) API aan. Deze API geeft u een lijst een zogeheten werkingsgebieden terug.
2. Met deze lijst van werkingsgebieden roept u vervolgens de [Toepasbare regels zoeken](https://developer.omgevingswet.overheid.nl/api-register/api/toepasbare-regels-zoeken/) API aan. Deze API geeft u een lijst terug met alle beschikbare activiteiten op die locatie waarvoor u een aanvraag kunt indienen.
3. Door de [Uitvoeren services](https://developer.omgevingswet.overheid.nl/api-register/api/uitvoeren-services/) te bevragen met de ID's van de gekozen activiteiten uit stap 2, krijgt u de vragen terug die horen bij de gekozen, zogeheten indieningsvereisten van de activiteiten. Voor de teksten van de toelichtingen, kunt u deze Uitvoeren services API nog een keer bevragen, maar dan met de input van de toelichting ID's.
4. Naast de vragen, behorende bij de indieningsvereisten, moet een initiatiefnemer vanzelfsprekend ook contactgegevens e.d. opgeven. Dat onderdeel noemen we, binnen het DSO-LV, de zogeheten "Algemene Set". De vragen van deze Algemene Set zijn op te vragen door de [Samengestelde services Registratie Toepasbare Regels}(https://developer.omgevingswet.overheid.nl/api-register/api/samengestelde-registratie-toepasbare-regels/) aan te roepen.
5. Door de vragen tussentijds te beantwoorden, ontstaat er als het ware een soort van vraag-antwoord spel met de Uivtvoeren services en de Samengestelde services Registratie Toepasbare Regels. Hierdoor kunnen er nieuwe vragen bij komen of juist vragen wegvallen op basis van gegeven antwoorden. De vragen zelf bevatten elementen uit de [STTR standaard](https://iplo.nl/digitaal-stelsel/aansluiten/standaarden/sttr-imtr/) waardoor u zaken meekrijgt over de prioriteit van bepaalde vragen, en daarmee in welke volgorde u de vragen zou kunnen beantwoorden. 
6. Op het moment dat alle vragen beantwoord zijn, kan de [Verzoek indienen](https://developer.omgevingswet.overheid.nl/api-register/api/verzoek-indienen/) API aangeroepen worden waarmee het indienen van het verzoek voorbeid kan worden.
7. Door dezelde API nog een keer aan te roepen met de parameters verkregen uit stap 6 kunt u definitief gaan indienen. 

