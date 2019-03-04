#  Vagrant Dokumentation

#### Installation

1. Vagrant herunterladen
2. Vagrant installieren
3. Vagrant VM erstellen


So sieht das Vagrant File dann aus
    
    $ vagrant box add http://10.1.66.11/vagrant/ubuntu/xenial64.box --name ubuntu/xenial64  #Vagrant-Box vom Netzwerkshare hinzufügen
    $ vagrant init ubuntu/xenial64        #Vagrantfile erzeugen
    $ vagrant up --provider virtualbox    #Virtuelle Maschine erstellen & starten
    
