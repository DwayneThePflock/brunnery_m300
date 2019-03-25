**Konfiguration**  
In der Kopie von meinem Repository, erstellte ich mit vagrant init ein Vagrantfile.
Um die Firewall und den Webserver zu installieren und konfigurieren habe ich es folgendermassen angepasst.  
Es wird ubuntu xenial64 als Basis verwendet.
  >Vagrant.configure("2") do |config|  
  >config.vm.box = "ubuntu/xenial64"

Es wird ein privates Netzerk erstellt. (Host Only) Die IP gemäss Vorgabe ist 10.71.13.12.  
Für mich definierte IP wird konfiguriert.  
  >config.vm.network "private_network", ip: "10.71.13.12"

Es wird aus dem aktuellen Ordner ein shared Folder gemacht, der unter /var/www/html eingehängt wird.
Da dies der Ordner ist in dem der Webserver das html Dokument bezieht, kann ich im vornherein ein index file in den Ordner einfügen, welches vom Webserver verwendet werden wird.
  >config.vm.synced_folder ".", "/var/www/html"

Virtualbox wird als VMprovider genutzt
  >config.vm.provider "virtualbox" do |vb|

Es werden 4 GB Ram zur Verfügung gestellt-  
  >vb.memory = "4024"  
  >end  

Installieren von Apache2 und ufw. ufw erlaubt Ports von ssh und http und IPs vom 24-Netz 10.71.13.0
 >  config.vm.provision "shell", inline: <<-SHELL  
 >  apt-get update  
 > apt-get install -y apache2  
 >apt-get update  
 >apt-get install -y ufw  
 >ufw allow ssh  
 >ufw allow http  
 >ufw allow from 10.71.13.0/24  

Da ein Neustart unerwünscht ist, wird die Firewall manuell eingeschaltet. yes Y | führt dazu, dass die Abrage beim enablen mit Y beantwrtet wird.
  >   yes Y | ufw enable  
  > SHELL  
  >end  
  
**Starten**  
Die VM kann mit vagrant up gestartet werden, wenn man die Konsole im Ordner mit dem Vagrantfile ausführt.  
Danach wird durch vagrant ssh eine Verbindung hergestellt.
