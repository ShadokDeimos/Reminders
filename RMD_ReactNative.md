# REACT-NATIVE #

## Configurer un Projet

## D�marrer un projet	##

� Lancer un Android Virtual Device (Emulator)
Entrer cette commande dans le r�pertoire projet
> react-native run-android

## 	D�marrer l'�mulateur Android sans Android Studio 	##

C:\Users\Deimos\AppData\Local\Android\Sdk\emulator.exe -avd YourEmulatorPresetName

/!\ Need to try with Nexus_5X_API_28_2

##	nodes_modules 	##

$ npm install --save react-navigation
$ npm install --save react-native-gesture-handler
$ react-native link

## 	Afficher les logs	##

> react-native log-ios
> react-native log-android

##	Les "Components" React Native	##

	Les Components React Native ont besoin d'�tre import�s

import { View, TextInput, Button } from 'react-native'

<View></View> 			Cr�e une vue
<TextInput />			Cr�e un input
<Button />			Cr�e un bouton
	title={} onPress{}		/!\ attribut title & onPress obligatoires /!\



##	D�clarer & utiliser du style 	##

const styles = {
	textinput: {
		marginLeft: 5,
		marginRight: 5
	},
	button: {
		borderColor: '#XXXXXX'
	}
}

<TextInput style={styles.textinput} pla... />
<Button style={styles.button} titl... />

� � � 	Via StyleSheet 	� � �

import { StyleSheet } from 'react-native'

const styles = StyleSheet.create({
	textInput: {
		[...]
	}
})

/!\ 	On ne met pas de style sur un composant import� ex :

import CustomButton from '../../'

<CustomButton style={} />

=> On met le style sur le composant <View> � l'int�rieur du composant custom

# # #	Utiliser Flex 	# # #

� flex

flex: 1 	Prends toutes la taille d'�cran dispo

flex: 2		Prendra 2/5�me de la taille d'�cran dispo
flex: 3		Prendra 3/5�me de la taille d'�cran dispo

� flexDirection:
	- column		Affiche les blocs en colonne
	- row			Affiche les blocs en ligne

� justifyContent:		Permet d'aligner les �l�ments sur l'axe principal
	- center			Alignement au centre
	- flex-start			Alignement au d�but
	- flex-end			Alignement � la fin
	- space-between			Les �lements s'affichent sur tout l'axe et laissent de
					l'espace entre eux
	- space-around			Pareil que space-between sauf qu'il y a en plus de l'espace
					entre les extr�mit�s de la vue. Les espaces aux extr�mit�s
					sont 2 fois inf�rieurs aux espaces entre les �lements
	- space-evenly			Pareil que space-around sauf que les espaces entres les
					�lements sont les m�mes que ceux entre les �l�ments.

� alignItems:			Permet d'aligner les �l�ments sur l'axe secondaire
	- center
	- flex-start
	- flex-end
	- stretch			Les �l�ments s'�tirent sur tout l'axe.


#	RAPPEL SUR LES COMPONENTS NATIVE 	#

<TextInput
	style={styles.blabla}
	placeholder='Writesomethinghere'
	onChangeText={(text) => function(text)}
	onSubmitEditing={() => function()}			Validation par "Enter"
/>

<FlatList
	data={this.state.data}					Donn�es � exploiter
	keyExtractor={(item) => item.id.toString()}		Key id blabla
	renderItem={() => <Text />}				Item � render

/>

## DEBUG

### When react-native run-android BUG :app:installDebug

$ adb kill-server
$ adb start-server
