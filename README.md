# OpenJDK 10 UberJAR-Runner S2I

An S2I-image intended for OpenShift 3.x to run UberJARs on OpenJDK 10 (specifically [Azul Zulu 10](https://www.azul.com/downloads/zulu/zulu-linux/)).

## Usage

This image in itself is (at the moment) entirely designed to take a single all-containing UberJAR which is placed in /opt/app-root. Building from actual source (using Maven or Gradle) may come at a later point but building a new image based off of this image or adding *Maven/Gradle/Ant/SBT* manually through an **assemble**-script should work fine.

### Multiple JARs

The **run**-script is fairly simple, if the user has populated the container with multiple JARs it will simply execute the first it encounters using **java -jar [first_jar_found.jar]**.

### Java Options

The **run**-script checks if the user has provided a **JAVA_OPTS**-environment variable. If that is not the case, it sets sensible defaults (in short: crash on OOM and use half of the available memory limit for heap).

### Modules

At this moment the image is not yet considering Java 9/10 modules and as such, it does no magic around this. It simply invokes the first JAR it finds using **java -jar**.

## CA-Certificates

In some business environments there may be a self-signed internal CA. This image is prepared for it, so you can add all certificates you need to **/etc/pki/ca-trust/source/anchors** and run `update-ca-trust` from a Dockerfile that inherits from this one.
