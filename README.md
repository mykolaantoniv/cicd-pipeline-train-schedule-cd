# cicd-pipeline-train-schedule-cd

This is a simple train schedule app written using nodejs. It is intended to be used as a sample application for a series of hands-on learning activities.

## Running the app

You need a Java JDK 7 or later to run the build. You can run the build like this:

    ./gradlew build

You can run the app with:

    ./gradlew npm_start

Once it is running, you can access it in a browser at [http://localhost:3000](http://localhost:3000)

```
adduser deploy
echo "deploy:jenkins" | chpasswd
groupadd train-schedule
usermod -a -G train-schedule deploy
echo "deploy ALL=(ALL) NOPASSWD: /usr/bin/systemctl stop train-schedule" >> /etc/sudoers
echo "deploy ALL=(ALL) NOPASSWD: /usr/bin/systemctl start train-schedule" >> /etc/sudoers
echo -e "[Unit]\\nDescription=Train Schedule\\nAfter=network.target\\n\\n[Service]\\n\\nType=simple\\nWorkingDirectory=/opt/train-schedule\\nExecStart=/usr/bin/node bin/www\\nStandardOutput=syslog\\nStandardError=syslog\\nRestart=on-failure\\n\\n[Install]\\nWantedBy=multi-user.target" > /etc/systemd/system/train-schedule.service
/usr/bin/systemctl daemon-reload
mkdir -p /opt/train-schedule
chown root:train-schedule /opt/train-schedule
chmod 775 /opt/train-schedule/
yum -y install nodejs unzip
```
