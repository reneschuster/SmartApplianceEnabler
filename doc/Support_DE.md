# Fragen / Probleme

Wenn sich der *Smart Appliance Enabler* nicht starten lässt oder der *SMA Home Manager* die vom *Smart Appliance Enabler* verwalteten Geräte nicht finden kann, sollen folgende Punkte geprüft werden:

## Läuft der Smart Appliance Enabler?
Ruft man das Start-Script *smartapplianceenabler* mit dem Parameter `status` auf, kann geprüft werden, ob der Service läuft:
```console
pi@raspberrypi:~ $ sudo /etc/init.d/smartapplianceenabler status
Running
```
Wenn `Running` angezeigt wird, läuft der *Smart Appliance Enabler*.

## Log
Der *Smart Appliance Enabler* schreibt seine Log-Daten in das Verzeichnis ```/tmp```, wobei die Dateinamen mit ```rolling``` beginnen gefolgt vom jeweilgen Datum:
```
pi@raspi ~ $ tail -f /tmp/rolling-2018-04-08.log
2018-04-08 10:17:01,072 INFO [main] d.a.s.Application [StartupInfoLogger.java:48] Starting Application on raspi with PID 23914 (started by root in /)
2018-04-08 10:17:01,106 DEBUG [main] d.a.s.Application [StartupInfoLogger.java:51] Running with Spring Boot v1.3.0.RELEASE, Spring v4.2.3.RELEASE
2018-04-08 10:17:01,108 INFO [main] d.a.s.Application [SpringApplication.java:653] No profiles are active
2018-04-08 10:17:23,172 INFO [main] d.a.s.s.w.SempController [SempController.java:50] SEMP controller created.
2018-04-08 10:17:23,247 INFO [main] d.a.s.w.SaeController [SaeController.java:67] SAE controller created.
2018-04-08 10:17:24,301 DEBUG [main] d.a.s.w.WebConfig$SaeWebMvcAutoConfigurationAdapter [WebConfig.java:63] Registered de.avanux.smartapplianceenabler.webservice.GensonHttpMessageConverter
2018-04-08 10:17:29,970 INFO [main] d.a.s.Application [StartupInfoLogger.java:57] Started Application in 33.225 seconds (JVM running for 36.295)
2018-04-08 10:17:29,973 INFO [main] d.a.s.Application [Application.java:45] Running version 1.2.0-SNAPSHOT 2017-12-23 19:16
2018-04-08 10:17:29,975 DEBUG [main] d.a.s.Application [Application.java:72] Starting SEMP discovery ...
2018-04-08 10:17:30,250 INFO [main] d.a.s.s.d.SempDiscovery [SempDiscovery.java:55] SEMP UPnP will redirect to http://192.168.69.5:8080
2018-04-08 10:17:30,252 DEBUG [main] d.a.s.Application [Application.java:75] ... SEMP discovery started
2018-04-08 10:17:30,253 DEBUG [main] d.a.s.Application [Application.java:80] Starting appliance manager ...
2018-04-08 10:17:30,574 DEBUG [main] d.a.s.Application [Application.java:83] ... Appliance manager started
2018-04-08 10:17:30,576 INFO [Thread-7] d.a.s.u.FileHandler [FileHandler.java:55] Using appliance directory /app
2018-04-08 10:17:30,583 INFO [main] d.a.s.Application [Application.java:95] PID 23914 written to /var/run/smartapplianceenabler.pid
```
Der *Log-Level* steht defaultmäßig auf ```debug```, um im Fehlerfall detaillierte Informationen zu haben. Falls weniger geloggt werden soll, kann der Log-Level auf ```info``` geändert werden in der Datei ```/opt/sae/logback-spring.xml```:
```
...
<logger name="de.avanux" level="debug" additivity="false">
...
```

## Version des Smart Appliance Enabler
Direkt nach dem Start schreibt der *Smart Appliance Enabler* die Version in die Log-Datei:
```
2018-04-08 10:17:29,973 INFO [main] d.a.s.Application [Application.java:45] Running version 1.2.0-SNAPSHOT 2017-12-23 19:16
```

## Verbindung zwischen Home Manager und Smart Appliance Enabler
Home Manager auf den *Smart Appliance Enabler* müssen sich im gleichen Netz befinden!
Wenn der Log-Level mindestens auf DEBUG gesetzt wurde, kann man in der Log-Datei sehen, wenn der Home Manager auf den *Smart Appliance Enabler* zugreift:
```
20:25:17.390 [http-nio-8080-exec-1] DEBUG d.a.s.semp.webservice.SempController - Device info/status/planning requested.
```
## Analyse der Log Dateien des SEMP Moduls im Sunny Home Manager
Siehe https://www.photovoltaikforum.com/thread/104060-ger%C3%A4te-mit-home-manager-koppeln-via-semp-ethernet/?postID=1396300#post1396300

## Anwender-Forum
Fragen zur Verwendung des *Smart Appliance Enabler* sollten im SEMP-Thread des *photovoltaik-forums* im SMA Herstellerbereich gestellt werden: https://www.photovoltaikforum.com/geraete-mit-home-manager-koppeln-via-semp-ethernet-t104060.html.

Bitte keine Fragen direkt per Email an mich stellen! Wenn die Fragen im Forum gestellt werden, haben alle was davon und die Chance auf Antworten ist deutlich größer.

## Fehler melden
Bei Fehlern im *Smart Appliance Enabler* sollte ein [Issue](https://github.com/camueller/SmartApplianceEnabler/issues) erstellt werden.
