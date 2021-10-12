# 8_maps_vejledning

# Øvelsesvejledning til øvelse 8 - Maps

#### Slut resultat

1. Lav et nyt expo projekt i din projekt mappe med `expo init 8_maps`og åben projektet i webstorm
2. Installér følgende dependencies:<br/>
   `expo install react-native-maps expo-constants expo-location
   `
3.	Undervejs i løsningen af denne øvelse, skal der bruges fem state variabler. Start med at initialisere følgende variabler ved brug af useState:
- hasLocationPermission - Startværdi = `false`
- currentLocation - Startværdi = `null`
- userMarkerCoordinates - Startværdi = `[]` (Et tomt array)
- selectedCoordinate - Startværdi = `null`
- selectedAddress - Startværdi = `null`

3.	Opret nu et et `<Mapview/>` i return() i app.js.<br/>HUSK: `<Mapview />` skal wrappes ind i et `<SafeAreaView/>`<br/>
HINT: Ved udfordringer se den officielle dokumentation, https://docs.expo.dev/versions/latest/sdk/map-view/

4. Vælg nu tre vilkårlige steder, du ønsker skal markeres på kortet. Find dernæst latitude & longitude for hver af stederne.
5. Placer dernæst stederne på kortet, ved brug af `<Marker />`. Forsøg at give hver markering en lille beskrivelse og en titel.<br/>
   HINT: Se dokumentationen her; https://github.com/react-native-maps/react-native-maps/blob/master/docs/marker.md
6. Forsøg nu at køre app'en. Efter opstart skal du nu blive præsenteret for et kort med tre markeringer. Ved at trykke på markeringen skal der fremvises en titel på stedet og en kort beskrivelse. 

7. Du skal nu sørge for at appen viser din aktuelle position på kortet. Af denne grund skal appen efterspørge en tilladelse til at benytte din lokation. Opret derfor metoden, getLocationPermission()
8. Metoden foretager et asynkront kald, der aktiverer en forespørgsel om tilladelse til at bruge din nuværende lokation.
   - Importer en `Location` instans fra expo-location og kald metoden,`requestForegroundPermissionsAsync` på `Location`.<br/>
    HINT: Find inspiration på den officielle vejledning: https://docs.expo.dev/versions/latest/sdk/location/
9. Sæt state-variablen `hasLocationPermission` til at være resultatet af den returnerede værdi fra det asynkrone kald - Find hjælp i bilag A.
10. Når metoden er lavet, skal denne kaldes i useEffect
11. Angiv nu en property i Mapview, som tillader brugeren at se sin nuværende position på kortet. 
12. Kør appen og se at det virker 
13. Opret nu metoden, `handleLongPress`. Metoden skal sørge for at afsætte en markør på det valgte punkt.<br/>HINT: Metoden tager en `event` med som argument. Instantiér en variabel ved navn 'coordinate' og angiv dennes værdi som resultatet af `event.nativeEvent.coordinate`
    - Tilføj koordinaten til arrayet, der skal opbevare en samling af koordinater; `userMarkerCoordinates`.<br/>HINT: Se eksempel på opdatering af state-arrays på følgende link: https://stackoverflow.com/questions/54676966/push-method-in-react-hooks-usestate
    - Aktivér nu egenskaben `longPress` i `<Mapview/>` og lav en reference til den nyoprettede metode, `handleLongPress`.
    - Afslutningsvis, skal du sørge for at alle punkter, der findes i `userMarkerCoordinates` bliver placerret på kortet.
    - Nu skal du kunne sætte markører på kortet ved at foretage længere tryk(longPress) vilkårlige steder på kortet i appen. 
14. Opret nu metoden, `handleSelectMarker` som ved tryk på en markør registrerer, hvilken markør der er trykket på og sætter værdierne for `selectedCoordinate` og `selectedAddress`. 
    - `handleSelectMarker` tager koordinatet fra markøren med som argument. 
    - Selve koordinatsættet kan direkte sættes på baggrund af den medsendte koordinat
    - Dernæst kan oplysningerne forbundet med koordinatsættet findes ved brug af det asynkrone kald, `Location.reverseGeocodeAsync`.<br/>HINT: Se dokumentation på dette ved brug af følgende link, https://docs.expo.dev/versions/latest/sdk/location/  
    - Ud fra resultatet af det asynkrone kald, skal værdien af `selectedAddress` sættes. 
    - Sørg for at handleSelectMarker påkaldes i onPress på en Markør
15. Opret nu en Tekstboks, der kun vises ved tryk på en markør og udskriver koordinatsættet(`userMarkerCoordinates`) og dertilhørende adresseoplysninger(`selectedAddress`)
16. Opret nu metoden, `RenderCurrentLocation`, der i `return()` indeholder en `<button/>` samt en en tekstboks, der udskriver koordinatsættet for din nuværende position, men kun hvis `currentLocation` har fået fastsat en værdi. <br/>Husk på at `currentLocation` i udgangspunktet er værdisat til `null`, hvorfor der i udgangspunktet kun returneres et `<button/>` fra `RenderCurrentLocation`.
    - Dernæst oprettes metoden, `updateLocation`, som opfanger enhedens position ved brug af det asynkrone kald `Location.getCurrentPositionAsync`.
    - Resultatet af det asynkrone kald, benyttes til at sætte værdien for `currentLocation`.<br/>HINT: Se dokumentationen fra punkt 8.
    


    
#### Bilag 

Bilag A - getLocationPermission
```
   const getLocationPermission = async () => {
   await Location.requestForegroundPermissionsAsync().then((item)=>{
   //Sæt din state variabel her. 
   } );
   
Bilag B - handleLongPRes
![image](https://user-images.githubusercontent.com/55731954/137005491-deebf184-2ed9-4bf8-bbb5-68a73eee98d5.png)


`


