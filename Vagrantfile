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
     sudo apt-get update
     sudo apt-get upgrade -y
     sudo apt-get install unzip openjdk-11-jre-headless letsencrypt nginx -y
     curl https://languagetool.org/download/LanguageTool-stable.zip -o LanguageTool.zip
     unzip LanguageTool.zip
     # TODO: Curl the directory and retreive the latest english ngram data
     curl https://languagetool.org/download/ngram-data/ngrams-en-20150817.zip -o en-ngrams.zip
     mkdir -p ./LanguageTool-5.2/en
     unzip en-ngrams.zip -d ./LanguageTool-5.2/en/.
     java -cp /home/vagrant/LanguageTool-5.2/languagetool-server.jar org.languagetool.server.HTTPServer --port 8082 --allow-origin "*" --languageModel /home/vagrant/LanguageTool-5.2/en &
   SHELL
end
