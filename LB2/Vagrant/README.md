#  Vagrant Dokumentation

#### Installation

1. Vagrant herunterladen
2. Vagrant installieren
3. Vagrant VM erstellen


So sieht das Vagrant File dann aus
    
    $ vagrant box add http://10.1.66.11/vagrant/ubuntu/xenial64.box --name ubuntu/xenial64  #Vagrant-Box vom Netzwerkshare hinzufügen
    $ vagrant init ubuntu/xenial64        #Vagrantfile erzeugen
    $ vagrant up --provider virtualbox    #Virtuelle Maschine erstellen & starten
    
# Vagrant Befehle

Hier sind die wichtigsten Vagrant Befehle aufgelistet:

| Befehl           |Beschreibung                                                                             |
| -----------------|:---------------------------------------------------------------------------------------:|
| Vagrant init     |Initialisiert die Vagrant Umgebung im aktuellen Verzeichnis und erstellt ein Vagrantfile |
| Vagrant up       |Erzeugt und Konfiguriert eine Virtuelle Maschine basierend auf dem Vagrantfile           |
| Vagrant ssh      |Verbindung zur VM per SSH wird hergestellt                                               | 
| Vagrant status   |Zeigt den aktuellen Status der VM an                                                     | 
| Vagrant port     |Zeigt die Weitergeleiteten Ports der VM an                                               | 
| Vagrant halt     |VM wird gestoppt                                                                         | 
| Vagrant destroy  |VM wird gestoppt und gelöscht                                                            | 

##  Vorgefertigte VM mit Vagrant aufsetzen

Aus dem M300 Repository, setzte ich automatisiert eine Ubuntu VM mit Apache2 auf.
Dazu musste ich nur in das Verzeichnis /M300/vagrant/web wechseln und "vagrant up" ausführen. 
Die VM wird daraufhin installiert und in Virtualbox angezeigt.  

![brunnery_m300](pictures/virtualbox)