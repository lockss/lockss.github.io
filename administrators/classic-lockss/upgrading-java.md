---
layout: page
title: Upgrading LOCKSS Box to Java 8
---

To get back to the Classic LOCKSS Homepage use [this link](./index.md)

## Upgrade instructions

1. Login as root (or gain root privilege)

2. Check the currently installed Java version; if Java 8 (1.8.x) is
  already installed, no further action is needed.

    ```java -version```

3. Stop the LOCKSS daemon:

    ```service lockss stop  (RHEL 6 and variants)```

    ```systemctl stop lockss  (RHEL 7 and variants)```

4. Uninstall Java 7; the two versions can live alongside each other but 
   we recommend uninstalling Java 7:

    ```yum remove java-1.7.0-openjdk```
    ```yum remove java-1.7.0-openjdk.headless```

    If you install the Java 7 JDK, remove it too:

    ```yum remove java-1.7.0-openjdk-devel```

5. Install the Java 8 JRE:

    ```yum install java-1.8.0-openjdk```

6. Verify that Java 8 is installed by checking the version number:

    ```java -version```

7. Restart the LOCKSS daemon:

    ```service lockss start  (RHEL 6 and variants)```

    ```systemctl start lockss  (RHEL 7 and variants)```
