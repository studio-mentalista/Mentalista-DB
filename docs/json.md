## 2.2.1.1 Standardisation d’un modèle d’envoi de donnée

Il n’existe pas encore de standardisation d'un format de données pour l’envoi de données cérébrales, il existe quelques [tentatives](https://github.com/NeuroJS/eeg-stream-data-model/issues/1) sur Internet qui rassemble des scientifiques du monde entier mais cette standardisation n’est pas encore adoptée par tous les équipementiers qui capturent de l’EEG et d’autres données biologiques. L’objectif est de repartir de ses recherches pour approfondir et améliorer les dernières tentatives de standardisation et de définir le format de données incluant les données cérébrales et leurs méta-données qui seront utilisées par la base de données.

###### Cahier des charges pour un format standard pour l’envoie de données cérébrales et biologique :

Notre base de données est programmée en langage web mais les casques EEG sont programmés en C et en Java et d’autres langages utilisés pour l’électronique. Il nous faut un format récent / portable / déjà utilisé sur le web et l’électronique. le meilleur candidat est le format de description **.JSON** ([JavaScript Object Notation](https://fr.wikipedia.org/wiki/JavaScript_Object_Notation)).

***Cerveau (Électricité) > OpenBCI (C) > Wifi Shield (C) > Streaming (NodeJS + JSON) > Mentalista DB (Javascript)***

Une illustration du chemin de l'onde cérébrale vers la base de données.

Le fichier JSON doit encapsuler les différents standards. Ceux utilisés à l'échelle internationale utilisée par d'autres scientifiques et les standards propores à la structure de la base de données et ses futures applications.

Ce qui donne 4 entrées pour le fichier JSON :

- deux standardisé ("info", "biodata") en accord avec les besoins des scientifiques, qui sont respectivement les méta donnée de la captation et les données cérébrales.
- deux  autres propre au besoin de chaque projet, la section "mentalista" décrivant les besoins de la base de données pour classifier le ficher et "app" les informations spécifiques à l’application qui a permis de recueillir ces données cérébrales.

```
{
  "app": [],
  "mentalista": [],
  "info": [],
  "biodata": []
}
```

**info**: décrit les méta-données de la session d’enregistrement

```
"info": [{	
	"id": null,
	"session_id": null,
	"created_at": 1497479774194733,
	
	"name": "undifined",
	"metric": "EEG",
	"type":"FFT", // timeserie …
	
	"channel_count": 8, 
	"topology": [ "Pz", "Oz", "Cz", "C1", "FP1", "FP2", "F3", "F4"],
	"sampleRate": 2500, // always in hz
	"unit": "millivolts",
	
	"version": "1.1",
	
	"source": {
	  "name": "undefined",
	  "size": "undefined",
	  "type": "undefined"
	}
}],
```

**biodata**: décrit l’enregistrement des données en fonction du type, de la [topologie](https://en.wikipedia.org/wiki/10–20_system_(EEG)), d'un [timestamp](https://fr.wikipedia.org/wiki/Horodatage) et de l’unité.

L’exemple ici montre trois enregistrements cérébraux à 8 canaux avec chacun un timestamp leur donnant un repère temporel précis.

```
"biodata": [
	{ 
		"value":[
			7.056745022195285,
			4.754953953750924,
			7.056745022195285,
			4.754953953750924, 
			7.056745022195285,
			4.754953953750924,
			7.056745022195285,
			4.754953953750924
		],
		"timestamp": 1503311302182
	},{
		"value":[
			7.056745022195285,
			4.754953953750924,
			7.056745022195285,
			4.754953953750924, 
			7.056745022195285,
			4.754953953750924,
			7.056745022195285,
			4.754953953750924
		],
		"timestamp": 1503311310564
	},{ 
		"value":[
			7.056745022195285,
			4.754953953750924,
			7.056745022195285,
			4.754953953750924, 
			7.056745022195285,
			4.754953953750924,
			7.056745022195285,
			4.754953953750924
		],
		"timestamp": 1503311317143
	}
]
```

**mentalista**: héberge toutes les méta-données permettant de classifier l'enregistrement cérébral dans la base de données. 

```
"mentalista": [
	{ 
	}
]
```

**app**: indique tout les données propre à l'expérience qui a permis de receuillir ces données elle peuvent être varier.

Voici un exemple des applications qui peuvent receuillir des informations pour la base de données
- [MentalistaFoot](http://mentalista.fr/foot)
- [Mentalista Guinguette](http://mentalista.fr/guinguette)
- [BrainSound](http://mentalista.fr/brainsound)
- [Projet Levitation](http://mentalista.fr/levitation)

L'exemple qui suis montre les méta-données pour la classification d'objet par le cortex visuel utilisé pour *la libraire de pensée*

```
"app": [
	{ 
	}
]
```