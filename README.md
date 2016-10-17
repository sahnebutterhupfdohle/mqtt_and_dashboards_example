Der Helsingin Seudun Liikenne (HSL), der Verkehrsbetrieb für die Region Helsinki/Finnland, bietet eine MQTT über WebSockets-API[1] an, über die man in Echtzeit an die Verkehrsdaten gelangen kann. Auf der Seite wird unter anderem die Zusammensetzung des Topics und die Nutzdaten der JSON-Antwort erklärt. Mit dem Dashboard Freeboard[2] sollen bestimmte Daten ausgewertet und im Browser angezeigt werden.

Damit MQTT-Daten in Freeboard verwendet werden können, muss ein Plugin und die Paho MQTT Javascript Bibliothek installiert werden. Diese werden unter [3] bereitgestellt und die Installation erklärt. Im Beispiel, das hier heruntergeladen werden kann, ist das Plugin bereits installiert und auf die HSL-API konfiguriert. Zusätzlich liegt dem Beispiel die Datei freeboard.json bei, in der die Dashboards und die Datenquelle eingestellt sind.

Listing Ausschnitt aus freeboard.json:

	"datasources": [
		{
			"name": "Tram",
			"type": "paho_mqtt",
			"settings": {
				"server": "mqtt.hsl.fi",
				"port": 1883,
				"use_ssl": false,
				"client_id": "Client_134312",
				"username": "",
				"password": "",
				"topic": "/hfp/journey/tram/RHKL00205/#",
				"json_data": true
			}
		}
	]


Über den Button „Load Freeboard“ kann die Konfiguration geladen werden. 

Vorher müssen jedoch zwei Einstellungen vorgenommen werden. Zuerst muss die „client_id“ geändert werden, damit keine zwei User mit derselben ID auf die Schnittstelle zugreifen. Danach muss das „Topic“ angepasst werden. Auf der Seite [4] werden alle aktuellen Daten aufgelistet. Dort kann man beispielsweise nach „tram“ suchen und sich ein Topic aussuchen. Das Topic der Tram mit der ID RHKL00098, die als Linie 10 fährt, ist: „/hfp/journey/tram/RHKL00098/1010/#“.

Auf der Seite [5] kann auf einer Landkarte geprüft werden, ob die Tram aktiv ist oder nicht an der Endhaltestelle angekommen ist und dadurch das Dashboard an Informationsgehalt weniger aussagekräftig ist.

Wenn alles korrekt eingestellt und freeboard.json geladen wurde, kann man folgendes Dashboard sehen:

https://raw.githubusercontent.com/sahnebutterhupfdohle/mqtt_and_dashboards_example/master/screenshot.jpg
 
Angezeigt wird die Verspätung in Sekunden, die Linie, die Geschwindigkeit in km/h und die Position.

Eine Änderung des Topics ist nach dem Laden nicht mehr möglich. Dazu muss die Datei freeboard.json bearbeitet und erneut geladen werden.

Links:

[1] https://digipalvelutehdas.hackpad.com/HSL-MQTT-API-draft

[2] http://freeboard.io/

[3] https://github.com/alsm/freeboard-mqtt

[4] http://dev.hsl.fi/tmp/mqtt/browser/

[5] http://dev.hsl.fi/tmp/mqtt/map/#&topic=/hfp/journey/tram/RHKL00098/1010/#
