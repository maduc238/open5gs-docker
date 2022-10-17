# Cài jDiameter
https://github.com/RestComm/documentation/blob/master/core/src/main/asciidoc/tutorials/jdiameter-quick-telscale-diameter-performance-testing-using-seagull.adoc

Hướng dẫn JDiameter: https://github.com/RestComm/jdiameter/blob/master/core/docs/sources-asciidoc/src/main/asciidoc/Diameter_User_Guide.adoc

Hướng dẫn cài GMLC: https://github.com/RestComm/gmlc/blob/master/docs/installationguide/sources-asciidoc/src/main/asciidoc/GMLC_Installation_Guide.adoc

Hướng dẫn chạy GMLC: https://github.com/RestComm/gmlc/blob/master/docs/adminguide/sources-asciidoc/src/main/asciidoc/GMLC_Admin_Guide.adoc

# Dependencies

```
sudo add-apt-repository ppa:openjdk-r/ppa
sudo apt update
apt search openjdk
...
sudo apt install openjdk-17-jdk
export JAVA_HOME=/usr/lib/jvm/java-17-openjdk
export PATH=$PATH:$JAVA_HOME/bin
java -version

--------------------

wget https://dlcdn.apache.org/maven/maven-3/3.8.6/binaries/apache-maven-3.8.6-bin.tar.gz
tar xzvf apache-maven-3.8.6-bin.tar.gz
sudo nano ~/.bashrc
-> export PATH=/home/.../bin:$PATH
source ~/.bashrc
mvn -version

--------------------

git clone https://github.com/RestComm/jdiameter.git
cd jdiameter
mvn clean install
```

https://www.h21lab.com/tools/jdiameter
