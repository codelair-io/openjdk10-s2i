# OpenJDK 10 UberJAR-Runner S2I

An S2I-image intended for OpenShift 3.x to run UberJARs on OpenJDK 10 (specifically [Azul Zulu 10](https://www.azul.com/downloads/zulu/zulu-linux/)).

## Usage

This image in itself is (at the moment) entirely designed to take a single all-containing UberJAR which is placed in /opt/app-root. Building from actual source (using Maven or Gradle) may come at a later point but building a new image based off of this image or adding *Maven/Gradle/Ant/SBT* manually through an **assemble**-script should work fine.

## CA-Certificates

In some business environments there may be a self-signed internal CA. This image is prepared for it, so you can add all certificates you need to **/etc/pki/ca-trust/source/anchors** and run `update-ca-trust` from a Dockerfile that inherits from this one.
