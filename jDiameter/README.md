# Cài jDiameter
https://github.com/RestComm/documentation/blob/master/core/src/main/asciidoc/tutorials/jdiameter-quick-telscale-diameter-performance-testing-using-seagull.adoc

## Cài VS Code:
```
sudo apt-get install wget gpg -y
wget -qO- https://packages.microsoft.com/keys/microsoft.asc | gpg --dearmor > packages.microsoft.gpg
sudo install -D -o root -g root -m 644 packages.microsoft.gpg /etc/apt/keyrings/packages.microsoft.gpg
sudo sh -c 'echo "deb [arch=amd64,arm64,armhf signed-by=/etc/apt/keyrings/packages.microsoft.gpg] https://packages.microsoft.com/repos/code stable main" > /etc/apt/sources.list.d/vscode.list'
rm -f packages.microsoft.gpg
sudo apt install apt-transport-https
sudo apt update
sudo apt install code -y
```

## Cài Java JDK
```
sudo apt-get install openjdk-11-jdk -y 
```

## Cài ksh
```
sudo apt-get install tcsh
sudo apt-get install nginx -y
wget http://mirrors.kernel.org/ubuntu/pool/universe/k/ksh/ksh_93u+20120801-3.1ubuntu1_amd64.deb
sudo apt install binfmt-support
sudo dpkg -i ksh_93u+20120801-3.1ubuntu1_amd64.deb
```

## Cài Seagull
Tải file .gz và cài rpm (nếu chạy được)
```
wget http://downloads.sourceforge.net/project/gull/seagull/1.8.2/seagull-1.8.2-Linux_RHEL6U1_X86_64.tar.gz
tar -xvf seagull-1.8.2-Linux_RHEL6U1_X86_64.tar.gz
cd packages
sudo apt install rpm -y
```
Cài Seagull
```
sudo rpm -ivh seagull-core-1.8.2-linux-2.6-intel.rpm
sudo rpm -ivh seagull-diameter-protocol-1.8.2-linux-2.6-intel.rpm
```
Kiểm tra: `seagull`

## Tải và cài Restcomm jDiameter
```
git clone https://github.com/RestComm/jdiameter.git
```
```
cd jdiameter
```
```
mvn clean install
```
Đợi dòng lệnh chạy...
```
cd examples
wget https://app.box.com/shared/static/zasdgurv1gbsi0jm46kqbwr06gincfas.zip
unzip zasdgurv1gbsi0jm46kqbwr06gincfas.zip
```
Nó sẽ tạo 2 folder
- charging-server-simulator-perf-config
- charging-server-simulator-perf-test
```
sudo apt install maven
```
```
cd charging-server-simulator-perf-test
mvn clean install -Prelease
```
Đợi dòng lệnh chạy...
```
cd target
```
Trong này sẽ chứa các file
- archive-tmp
- classes
- maven-archiver
- Restcomm-dcs-b20150728.1716.jar
- Restcomm-dcs-b20150728.1716-standalone.jar

## Chạy jDiameter Server
Mở một bash terminal

Tới directory **jdiameter/examples/charging-server-simulator-perf-test/**

Execute the file : **./ccr-cca-event-client.ksh**

Sau đó sẽ hiện terminal chạy...

## Changing Default settings
- Edit the file : **jdiameter/examples/charging-server-simulator-perf-test/src/main/resources/config-server.xml**
```
<LocalPeer>
    <URI value="aaa://127.0.0.1:3868" />
    <IPAddresses>
      <IPAddress value="127.0.0.1" />
    </IPAddresses>
    <Realm value="Restcomm.org" />
....

 <Network>
    <Peers>
      <Peer name="aaa://127.0.0.1:13868" attempt_connect="false" rating="1" />
    </Peers>
    <Realms>
      <Realm name="Restcomm.org" peers="127.0.0.1" local_action="LOCAL" dynamic="false" exp_time="1">
        <ApplicationID>
```
- Edit the file **jdiameter/examples/charging-server-simulator-perf-config/seagull/ccr-cca-event-client.xml**
```
...

<command name="CCR">
      <avp name="Session-Id" value="value_is_replaced"> </avp>
      <avp name="Auth-Session-State" value="0"> </avp>
      <avp name="Origin-Host" value="storm01.Restcomm.org"> </avp>
      <avp name="Origin-Realm" value="Restcomm.org"> </avp>
      <avp name="Destination-Realm" value="Restcomm.org"> </avp>
      <avp name="Destination-Host" value="127.0.0.1"> </avp>
      <avp name="Auth-Application-Id" value="4"></avp>
```
