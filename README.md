# Maps Vejledning 🗺️

I dag skal vi arbejde med at få et `react-native-maps` til at virke på en simple app. Start med at læse dokumentationen her: 

https://docs.expo.dev/versions/latest/sdk/map-view/ <br>
https://github.com/react-native-maps/react-native-maps

Dette modul har virkelig mange fede features så gør jer selv en tjeneste og læs dokumentationen! 

<Br>

# App.js 📲

Til start med skal vi lave en TapNavigator til de 2 screens vi skal bruge. 

## Navigation
I en ny folder kaldt `screens` lav 2 screens:
- `Home.js`
- `Map.js`

I hver screen indsæt følgende kode (husk at ændre navn osv.):
```javascript
import React from 'react';
import { View, Text, StyleSheet } from 'react-native';

export default function Home({navigation}) {
  return (
    <View style={styles.container}>
      <Text style={styles.text}>This is ???</Text>
    </View>
  );
};

const styles = StyleSheet.create({
  container: {
    flex: 1,
    justifyContent: 'center',
    alignItems: 'center',
    backgroundColor: '#fff', 
  },
  text: {
    fontSize: 24,
    fontWeight: 'bold',
  },
});


```

## App.js

Tilbage i App.js skal vi nu lave vores navigation til disse skræme. Indsæt følgende i din App.js og udfyld de forskellige `???`

```javascript
export default function App() {

  const Tab = ???();

  return (
    <???>
      <Tab.Navigator
        screenOptions={({route}) => ({
          tabBarActiveTintColor: '#FF0000',
          tabBarInactiveTintColor: "gray",
          tabBarIcon: ({color, size}) => {
            let iconName;

            if(route.name === 'Home'){
              iconName = 'home'
            }else if(route.name === 'Map'){
              iconName = 'map'
            }

            return <Ionicons name={iconName} size={size} color={color}/>
          }
        })}
        >
        <Tab.Screen name="Home" component={???} />
        <Tab.Screen name="Map" component={???} />
      </Tab.Navigator>
    </???>
  );
}

const styles = StyleSheet.create({
  container: {
    flex: 1,
    backgroundColor: '#fff',
    alignItems: 'center',
    justifyContent: 'center',
  },
});
```

Hints:
- Husk at vi skal deklare vores Bottom Tap Navigator som det første.
- Husk at vi skal indkapsle vores navigation i en Container
- Husk at vi skal impotere vores sider og moduler 

Check at din navigation virker og forsæt til Home.js

<Br> </Br>

# Home.js 🏡(❍ᴥ❍ʋ)

Start med at import dine moduler: 

```javascript
import { StatusBar } from 'expo-status-bar';
import { StyleSheet, Text, View, Image, TextInput, TouchableOpacity } from 'react-native';

import { LinearGradient } from 'expo-linear-gradient';

import AsyncStorage from '@react-native-async-storage/async-storage';
import { useState } from 'react';
```

<br>

## const

Vi skal nu lave 3 `const` med `useState` som det første i vores export function:
- `latitude` med et tomt string 
- `longitude` med et tomt string
- `markers`med et tomt array

Hint:
- `const [latitude, setLatitude] = useState('');`

<br>

## addAndSaveMarker 📍

Vi skal nu lave en addAndSaveMarker funktion.
Denne funktion tilføjer en ny markør til en liste over eksisterende markører og gemmer den opdaterede liste ved hjælp af `AsyncStorage`.

### Trin 1: Opret en ny markør

Start med at oprette en ny markør ved at bruge de aktuelle `latitude` og `longitude` værdier. Disse værdier omdannes til tal ved hjælp af `parseFloat()`.

```javascript
const newMarker = { latitude: parseFloat(???), longitude: parseFloat(???) };
```

### Trin 2: Opdater markørlisten

Opdater listen af markører ved at tilføje den nye markør til den eksisterende liste med markører. Brug `setMarkers()` til at opdatere din state.

```javascript
const updatedMarkers = [...markers, newMarker];
setMarkers(updatedMarkers);
```

Når markøren er blevet tilføjet, rydder du inputfelterne for bredde- og længdegrad ved at sætte deres værdier til tomme strenge.

```javascript
setLatitude('');
setLongitude('');
```

### Trin 3: Gem markørerne ved hjælp af AsyncStorage

Nu gemmer du de opdaterede markører (`updatedMarker`) som strings ved hjælp af `AsyncStorage`. Dette gemmer listen af markører permanent på enheden. Brug en `try` - `catch` med `await` function her. Du vil også navigerer brugeren tilbage til kortskærmen ved hjælp af `navigation.navigate()`.

```javascript
try{
    await ???.setItem('markers', JSON.stringify(???));
    navigation.navigate('???');
} catch (error) {
    console.error('Error saving markers', error);
}
```
<Br>

## return

Indsæt først din styling under din return

```javascript
const styles = StyleSheet.create({
  container: {
    flex: 1,
    backgroundColor: '#fff',
    alignItems: 'center',
    justifyContent: 'center',
  },
  background: {
    position: 'absolute',
    left: 0,
    right: 0,
    top: 0,
    height: '100%',
  },
    bcg: {
        padding: 80,
        alignItems: 'center',
        position: 'absolute',
        width: '100%',
        height: '100%',

    },
    title: {
        fontSize: 32,
        fontWeight: 'bold',
        color: '#333',
        marginBottom: 80,
    },
    input: {
        height: 40,
        borderColor: 'lightgray',
        borderWidth: 1,
        marginBottom: 20,
        paddingHorizontal: 10,
        width: '90%',
        borderRadius: 20, // Makes the input round
        backgroundColor: '#f9f9f9', // Light background color for minimalistic look
    },
    button: {
        backgroundColor: '#FF0000', // Red color matching the logo
        padding: 10,
        borderRadius: 20,
        alignItems: 'center',
        width: '90%',
        marginTop: 40,
      },
    buttonText: {
        color: '#FFFFFF', // White text color
        fontSize: 16,
        fontWeight: 'bold',
      },
});
```

Indsæt følgende i din `return` function: 

```javascript
return (
    <View style={styles.container}>
        <Image source={require('??? - vi vil gerne have background her')} style={{width: '100%', height: '100%'}}/>
        <LinearGradient
        // Background Linear Gradient
        colors={['rgba(255,255,255,0.10)', 'rgba(255,255,255,0.75)','rgba(255,255,255,1)', 'rgba(255,255,255,1)']}
        style={styles.background}
      />
        <View style = {styles.bcg}>
            <Image source={require('??? - vi vil gerne have logo her')} style={{width: 100, height: 100, marginBottom: 50}}/>
            <Text style={styles.title}> INNT Map App </Text>
            <TextInput style={styles.input} value={???} onChangeText={??? - vi vil gerne set vores værdi her} placeholder="lattitude"/>
            <TextInput style={styles.input} value={???} onChangeText={??? - vi vil gerne set vores værdi her} placeholder="longitude"/>
            <TouchableOpacity style={styles.button} onPress={???}>
                <Text style={styles.buttonText}>Search</Text>
            </TouchableOpacity>
        </View>
    </View>
  );
```

Download `background.jpeg` og `logo.png` her fra repo og indsæt disse i dine `assests` før du importere dem som dit `Image source`

I vores `TextInput`s vil vi gerne have vores værdi være lattitude og longitude samt set denne værdi når teksten ændres. 

I vores `TouchableOpacity` vil vi gerne kalde på vores `addAndSaveMarker` function.

Din `Home.js` skulle nu gerne være done. 

<br></br>

# Map.js (╯'□')╯︵🌍

På vores `Map.js` vil vi nu gerne skabe vores map. 

Start med imports:

```javascript
import React, { useEffect, useState } from 'react';
import { StyleSheet, View, ActivityIndicator } from 'react-native';
import MapView, { Marker } from 'react-native-maps';
import AsyncStorage from '@react-native-async-storage/async-storage';
import { useFocusEffect } from '@react-navigation/native';
```

## const

Lav nu 3 `const` med `useState`
- `markers` med tomt array
- `loading` med `useState(true)`
- `initialRegion` med 4 værdier `latitude:???`, `longitude:???`, `latitudeDelta: 0.0922`, `longitudeDelta: 0.0421`

Sæt dine longitude og latitude værdier til det som dit inital map skal vise - f.eks. KBH

<br>

## getMarkers 📌

Vi skal nu lave en async function der henter vores map markers.

Den skal bruge en `try - catch - finally` functionalitet som afventer vores `markers` fra vores `AsyncStorage`.

Derefter, if vores `storedMarkers` ikke er `null` skal vi bruge `JSON.parse` disse markers. Dette skyldes at vores data er gemt som strings og vi skal convert dem tilbage til JavaScript objects. 

Vi skal derefter opdatere vores `setMarkers` useState med disse parsed markers. 

```javascript
const getMarkers = async () => {
    try {
      const storedMarkers = await AsyncStorage.getItem('???');
      if (storedMarkers ??? null) {
        const parsedMarkers = JSON.parse(???);
        setMarkers(???);
        const latestMarker = parsedMarkers[parsedMarkers.length - 1];
        setInitialRegion({
          latitude: latestMarker.latitude,
          longitude: latestMarker.longitude,
          latitudeDelta: 0.0922,
          longitudeDelta: 0.0421,
        });
      }
    } catch (error) {
      console.error('Error retrieving markers', error);
    } finally {
      setLoading(false);
    }
  };
```

<br>

## useFocusEffect & if(loading)

vi skal nu lave en en function der aktivere vores `getMarkers`function hver gang brugeren kommer ind på vores Map.js screen. 

Til dette vil vi bruge en `useFocusEffect`. Indsæt og ret denne kodeblok efter din `getMarkers`funktion. Vi vil gerne sætte vores loading til true da dette er den inital værdi hvorefter vi vil kører vores `getMarkers` function.

```javascript
useFocusEffect(
  React.useCallback(() => {
    setLoading(???);
    ???();
  }, [])
);
```

Herefter vil gerne fortælle app'en hvad der skal ske mens der loades. ´
```javascript
if (loading) {
  return (
    <View style={styles.loadingContainer}>
      <ActivityIndicator size="large" color="#0000ff" />
    </View>
  );
}
```

## return

Indsæt følgende som det sidste på din Map.js og ret den til

```javascript
  return (
    <View style={styles.container}>
      <MapView
        style={styles.???}
        initialRegion={initialRegion}
      >
        {markers.map((marker, index) => (
          <Marker
            key={index}
            coordinate={{ latitude: marker.???, longitude: marker.??? }}
            pinColor="#FF0000" // Custom pin color
          />
        ))}
      </MapView>
    </View>
  );
}

const styles = StyleSheet.create({
  container: {
    flex: 1,
  },
  map: {
    ...StyleSheet.absoluteFillObject,
  },
  loadingContainer: {
    flex: 1,
    justifyContent: 'center',
    alignItems: 'center',
  },
});
```

<B>Du er nu done med din map app! (ノ^_^)ノ┻━┻ ┬─┬ ノ( ^_^ノ)</B> 