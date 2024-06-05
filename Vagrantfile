# Vagrantfile

Vagrant.configure("2") do |config|
  
  # VM для Jenkins Server
  config.vm.define "jenkins_server" do |server|
    server.vm.box = "ubuntu/focal64"
    server.vm.hostname = "jenkins-server"
    server.vm.network "forwarded_port", guest: 8080, host: 8080 # Перенаправлення порту
    server.vm.network "private_network", ip: "192.168.50.10"

    server.vm.provision "shell", inline: <<-SHELL
      # Оновлення пакетів
      sudo apt-get update

      # Встановлення Java (необхідно для Jenkins)
      sudo apt-get install -y openjdk-11-jdk

      # Встановлення Jenkins
      sudo wget -O /usr/share/keyrings/jenkins-keyring.asc \
      https://pkg.jenkins.io/debian-stable/jenkins.io-2023.key
      echo "deb [signed-by=/usr/share/keyrings/jenkins-keyring.asc]" \
      https://pkg.jenkins.io/debian-stable binary/ | sudo tee \
      /etc/apt/sources.list.d/jenkins.list > /dev/null

      sudo apt-get update
      sudo apt-get install -y jenkins

      # Запуск Jenkins
      sudo systemctl start jenkins
      sudo systemctl enable jenkins

      # Встановлення Docker
      sudo apt-get install -y apt-transport-https ca-certificates curl software-properties-common
      curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo apt-key add -
      sudo add-apt-repository "deb [arch=amd64] https://download.docker.com/linux/ubuntu bionic stable"
      sudo apt-get update
      sudo apt-get install -y docker-ce

      # Встановлення Docker Compose
      sudo curl -L "https://github.com/docker/compose/releases/download/1.29.2/docker-compose-$(uname -s)-$(uname -m)" -o /usr/local/bin/docker-compose
      sudo chmod +x /usr/local/bin/docker-compose
    SHELL
  end

  # VM для Jenkins Worker
  config.vm.define "jenkins_worker" do |worker|
    worker.vm.box = "ubuntu/focal64"
    worker.vm.hostname = "jenkins-worker"
    worker.vm.network "private_network", ip: "192.168.50.20"

    worker.vm.provision "shell", inline: <<-SHELL
      # Оновлення пакетів
      sudo apt-get update

      # Встановлення Java (необхідно для Jenkins)
      sudo apt-get install -y openjdk-11-jdk

      # Встановлення Docker
      sudo apt-get install -y apt-transport-https ca-certificates curl software-properties-common
      curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo apt-key add -
      sudo add-apt-repository "deb [arch=amd64] https://download.docker.com/linux/ubuntu bionic stable"
      sudo apt-get update
      sudo apt-get install -y docker-ce

      # Встановлення Jenkins агенту (worker)
      wget https://repo.jenkins-ci.org/public/org/jenkins-ci/main/remoting/4.6/remoting-4.6.jar -P /home/vagrant
    SHELL
  end

end