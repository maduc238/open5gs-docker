# Cài jDiameter
https://github.com/RestComm/documentation/blob/master/core/src/main/asciidoc/tutorials/jdiameter-quick-telscale-diameter-performance-testing-using-seagull.adoc

Hướng dẫn JDiameter: https://github.com/RestComm/jdiameter/blob/master/core/docs/sources-asciidoc/src/main/asciidoc/Diameter_User_Guide.adoc

Hướng dẫn cài GMLC: https://github.com/RestComm/gmlc/blob/master/docs/installationguide/sources-asciidoc/src/main/asciidoc/GMLC_Installation_Guide.adoc

Hướng dẫn chạy GMLC: https://github.com/RestComm/gmlc/blob/master/docs/adminguide/sources-asciidoc/src/main/asciidoc/GMLC_Admin_Guide.adoc

# Dependencies
Cài **JDK**
```
sudo add-apt-repository ppa:openjdk-r/ppa
sudo apt update
apt search openjdk
```
Chọn bản **JDK** phù hợp, ở đây chọn bản 17
```
sudo apt install openjdk-17-jdk
export JAVA_HOME=/usr/lib/jvm/java-17-openjdk
export PATH=$PATH:$JAVA_HOME/bin
java -version
```
Cài **maven**
```
wget https://dlcdn.apache.org/maven/maven-3/3.8.6/binaries/apache-maven-3.8.6-bin.tar.gz
tar xzvf apache-maven-3.8.6-bin.tar.gz
sudo nano ~/.bashrc
```
Thêm dòng lệnh này vào cuối file. Phần `...` là đường dẫn tới `bin` của **maven**
```
export PATH=/home/.../bin:$PATH
```
Chạy lại và kiểm tra
```
source ~/.bashrc
mvn -version
```
Cài và chạy **jDiameter**
```
git clone https://github.com/RestComm/jdiameter.git
cd jdiameter
mvn clean install
```

# Chạy jDiameter

Nếu `[INFO] BUILD SUCCESS`, sửa 2 file [`ExampleClient.java`](https://github.com/maduc238/open5gs-docker/blob/main/jDiameter/ExampleClient.java) và [`ExampleServer.java`](https://github.com/maduc238/open5gs-docker/blob/main/jDiameter/ExampleServer.java) trong jdiameter/examples/guide1

Tự build:
```
mvn install -f "pom.xml" -Dcheckstyle.skip
```

Ném file `example1-1.7.0-SNAPSHOT-jar-with-dependencies.jar` vào đường dẫn `.../target/`
```
java -classpath target/example1-1.7.0-SNAPSHOT-jar-with-dependencies.jar org.example.server.ExampleServer
```
Chạy và bật wireshark trên `lo` để xem kết quả
