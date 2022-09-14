# Compliance Traps of TDOSCA-TC12-PLAINHW

* This app uses internal classes licensed under different licenses:
  - Default License: M.I.T (see LICENSE in the top directory)
  - Greeter.java :- A.p.a.c.h.e-2.0 (see file header)
  - GreeterTest.java :- A.p.a.c.h.e-2.0 (see file header)
  - Tipster.java :- (see file header)
  - TipsterTest.java :- (see file header)

* The file LICENSE contains the text of the MIT license but does not explicitly declare to be the MIT license

* Additionally the software depends on the external 3rd party components
  * apache-log4j:
    - repository: https://logging.apache.org/log4j/2.x/download.html
    - license: Apache-2.0
    - NOTICE.txt: yes
  * joda-time
    - repository: https://github.com/JodaOrg/joda-time/releases
    - license: Apache-2.0
    - NOTICE.txt: yes

This 3rd Party software is integrated into the zip package created by ``mvn package``. Particularly the pom.xml does NOT declared these dependencies as *provided* etc. Hence, the scanning tools must find the respective compliance artifacts.

*Elucidation*:

* If one focuses on the upload of the repository content (sources and maven files), then one does not additionally distribute the 3rd party components. Hence, the repository on its own must only contain the compliance artifacts valid for the uploaded sources.
* But if one considers the fact, that in this case ``mvn package`` also creates a distributable zip file  containing the TC12-jar file, the 3rd-Party-jar files, and a start script (added by the maven plugin *assembly*), then it is clear, that this distributable zip file should also contain the compliance artifacts of the 3rd party components:
  - Hence the tested scanning tools should also deliver the compliance artifacts of these 3rd party tools
  - For the moment, this is not implemented

  **Why do we write the license names in a 'dotted' version in this file?**

  *In this text (and in some source files) we describe the used licenses. But these descriptions shall not be taken as licensing statements by the scanning tools.*
