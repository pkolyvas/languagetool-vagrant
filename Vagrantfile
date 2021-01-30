# -*- mode: ruby -*-
# vi: set ft=ruby :

# All Vagrant configuration is done below. The "2" in Vagrant.configure
# configures the configuration version (we support older styles for
# backwards compatibility). Please don't change it unless you know what
# you're doing.
Vagrant.configure("2") do |config|
  config.vm.box = "ubuntu/focal64"
  config.vm.provider "virtualbox" do |v|
    v.cpus = 2
  end
  config.vm.provider "virtualbox" do |v|
    v.memory = 2048
  end


  config.vm.network "forwarded_port", guest: 8082, host: 8081

  config.vm.synced_folder "/Users/pkolyvas/Code/", "/home/vagrant/code/"

  config.vm.provision "shell", inline: <<-SHELL
     sudo apt-get update -y
     sudo apt-get upgrade -y
     sudo apt-get install unzip openjdk-11-jre-headless letsencrypt -y
     curl https://languagetool.org/download/LanguageTool-stable.zip -o LanguageTool.zip
     unzip LanguageTool.zip -d LanguageTool
     curl https://languagetool.org/download/ngram-data/ngrams-en-20150817.zip -o en-ngrams.zip
     mkdir -p ./LanguageTool/en
     uzip en-ngrams.zip -d ./LanguageTool/en/.
     java -cp languagetool-server.jar org.languagetool.server.HTTPServer --port 8081 --allow-origin "*" --languageModel /home/vagrant/LanguageTool/en
   SHELL
end
