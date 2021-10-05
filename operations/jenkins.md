### Jenkins (Ubuntu VM)

#### Sources:
- https://www.digitalocean.com/community/tutorials/how-to-install-jenkins-on-ubuntu-20-04



1. Add the repository key for jenkins to your Ubuntu system

    ```bash
    $ wget -q -O - https://pkg.jenkins.io/debian-stable/jenkins.io.key | sudo apt-key add -
    ```
2. Append the Debian package address to the server's sources.list (we need this to update the apt packages)
    ```bash
    $ sudo sh -c 'echo deb http://pkg.jenkins.io/debian-stable binary/ > /etc/apt/sources.list.d/jenkins.list'
    ```

3. Update your aptitude and install jenkins
    ```bash
    $ sudo apt update
    $ sudo apt install jenkins
    ```

4. Start the systemctl service for Jenkins
    ```bash
    $ sudo systemctl start jenkins
    ```
    To check the status run the following:
    ```bash
    sudo systemctl status jenkins
    ```
    the output should be:
    ```bash
    Output
    ● jenkins.service - LSB: Start Jenkins at boot time
        Loaded: loaded (/etc/init.d/jenkins; generated)
        Active: active (exited) since Tue 2021-10-05 19:42:03 CEST; 50s ago
        Docs: man:systemd-sysv-generator(8)
        Tasks: 0 (limit: 18995)
        Memory: 0B
        CGroup: /system.slice/jenkins.service
    ```

5. Now it's time to open your ports and forward the data to your server.
Jenkinks runs on port :8080.
Be sure to disable firewall on that port by running the following:
    ```bash
    $ sudo ufw allow 8080
    ```

6. At this point Jenkins should be accesible from the internet. Surf to your ```ipaddress:/8080``` and you should get a prompt for a secret admin password. From your Ubuntu terminal run the following to get the password:

    ```bash
    $ sudo nano /var/lib/jenkins/secrets/initialAdminPassword
    ```
    Copy and paste the password into the prompt and you're ready to go. Let Jenkins install the recommended plugins.

Now all we need to do is create the build and attach it to a githook from the repository.