## 2.2.1.1 Standardisation d’un modèle d’envoie de donnée

Il n’existe pas encore de standardisation de format de données pour l’envoie de données cérébrales, il existe quelques tentatives sur Internet qui rassemblent des scientifiques du monde entier mais cette standardisation n’est pas encore adopté par tout les équipementier qui capturent de l’EEG et d’autre données biologique. L’objectif est de repartir de ces recherches pour approfondir et améliorer les premières tentatives de standardization et de définir le format de donnée incluant les données cérébrales et leurs méta-donnée qui seront utilisé par la base de donnée pour traiter et analyser ses données biologiques.

###### Cahier des charges pour un format standard pour l’envoie de données cérébrales et biologique :

Notre base de données est programmé en langage web mais les casques EEG sont programmé en C en Java ou d’autre langage utilisé pour l’électronique il nous faut un format récent / portable / déjà utilisé sur le web et l’électronique. le meilleur candidat est le format de description .JSON (JavaScript Object Notation) 
Notre casque est programmé en C il communique via une puce Wifi en NodeJS vers notre serveur aussi programmé en Javascript le format qui aura la meilleur compatibilité entre les différents maillons de la chaine est le JSON.
Le fichier JSON doit encapsuler les différents standard qui nous permet définir un standard international pour les Bio Data et les Informations mais de quand même ajouter des Meta Données propre à la structure de la base de données

```
{
  "app": [],
  "mentalista": [],
  "info": [],
  "biodata": []
}
```

Ce qui donne 4 entrée pour ce fichier deux standardisé ("info", "biodata") en accord avec les besoins des scientifiques. Et deux  autre propre au besoin de chaque projet la section "mentalista" décrivant les besoin de la base de données pour classifier le ficher et "app" les informations spécifique à l’application qui a tiré ces données cérébrales.

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

**info :** décrit les méta-données de la session d’enregistrement

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
		"timestamp": 1497479774194733.0
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
		"timestamp": 1497479774194733.0
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
		"timestamp": 1497479774194733.0
	}
]
```

**biodata :** décrit l’enregistrement des données en fonction de la topologie d’un timestamp et de l’unité
L’exemple ici montre trois enregistrement cérébralaux à 8 channel avec chacun un timestamp leur donnant un repère temporelle précis.