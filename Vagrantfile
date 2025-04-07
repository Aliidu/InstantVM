Vagrant.configure("2") do |config|
  # Demande à l'utilisateur quelle VM démarrer
  puts "Quelle VM voulez-vous démarrer ? (windows/ubuntu/all) [all par défaut] : "
  selected_vm = STDIN.gets.chomp.downcase
  selected_vm = "all" if selected_vm.empty?  # all comme valeur par défaut

  ## ======== VM Windows 10 ========
  if selected_vm == "all" || selected_vm == "windows"
    timestamp = Time.now.to_i  # Génère un ID unique pour chaque VM Windows

    config.vm.define "win10-#{timestamp}" do |win|
      win.vm.box = "StefanScherer/windows_10"  # Template de VM Windows 10 - A modifier si nécessaire
      win.vm.hostname = "win10-#{timestamp}"

      # Configuration matérielle
      win.vm.provider "virtualbox" do |vb|
        vb.memory = "4096"
        vb.cpus = 2
        vb.gui = true  # Activation de l'interface graphique, nécessaire pour le copier-coller/glisser-déposer
        vb.customize ["modifyvm", :id, "--clipboard", "bidirectional"]  # Copier-coller bidirectionnel
        vb.customize ["modifyvm", :id, "--draganddrop", "bidirectional"]  # Glisser-déposer bidirectionnel
      end

      win.vm.communicator = "winrm"   # Pour communiquer avec la VM pour la configurer
      win.winrm.username = "vagrant"
      win.winrm.password = "vagrant"

      # Exécution de commandes après le démarrage
      win.vm.provision "shell", inline: <<-SHELL
        echo "Configuration du clavier en AZERTY"
        powershell -Command "Set-WinUserLanguageList fr-FR -Force"
      SHELL
    end
  end

  ## ======== VM Ubuntu ========
  if selected_vm == "all" || selected_vm == "ubuntu"
    config.vm.define "ubuntu-vm" do |ubuntu|
      ubuntu.vm.box = "ubuntu/jammy64"   # Ubuntu Server 22.04 LTS
      ubuntu.vm.hostname = "ubuntu-vm"

      ubuntu.vm.provider "virtualbox" do |vb|
        vb.memory = "2048"
        vb.cpus = 1
      end

      ubuntu.vm.communicator = "ssh"

      # Mise à jour et configuration du clavier en AZERTY
      ubuntu.vm.provision "shell", inline: <<-SHELL
      echo "Configuration du clavier AZERTY"

      # Installation du package console-data si non installé
      sudo apt install -y console-data keyboard-configuration

      # Définition du clavier en français de manière persistante
      echo 'XKBLAYOUT="fr"' | sudo tee /etc/default/keyboard > /dev/null
      sudo dpkg-reconfigure -f noninteractive keyboard-configuration

      # Appliquer immédiatement la configuration
      sudo loadkeys fr
    SHELL
    end
  end
end
