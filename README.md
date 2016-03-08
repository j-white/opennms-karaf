## Preface

This repository contains a custom distribute of Karaf that allows you to
add Maven repositories, Karaf feature repositories and features to boot
with .d style folders.

## Demo 

mvn clean install
pushd karaf/target/
tar zxvf karaf-container-1.0.0-SNAPSHOT.tar.gz
./karaf-container-1.0.0-SNAPSHOT/bin/karaf clean

...wait...

Ctrl+D

echo 'file:/home/jesse/git/minion-system-tests/docker/provisioning/dominion/minion@id=minion@snapshots,mvn:org.opennms.newts/newts-karaf/1.3.1/xml/features' > karaf-container-1.0.0-SNAPSHOT/etc/featurepacks.d/minion.pack
echo 'newts-api' > karaf-container-1.0.0-SNAPSHOT/etc/featuresboot.d/newts.boot
./karaf-container-1.0.0-SNAPSHOT/bin/karaf clean

...wait...

## Building Packages

pusdh karaf/target
rm -f opennms-karaf-1.0-1.x86_64.rpm && rm -rf opt/minion
mkdir -p opt/minion/
tar zxvf karaf-container-1.0.0-SNAPSHOT.tar.gz -C opt/minion/ --strip-components=1
fpm -s dir -t rpm -n "opennms-karaf" -v 1.0 opt
