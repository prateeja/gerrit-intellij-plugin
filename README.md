gerrit-intellij-plugin
======================

Introduction
-----------

Unofficial [IntelliJ Platform] plugin for [Gerrit Code Review Tool].
Only Gerrit 2.6 or newer is supported (missing / incomplete REST API in older versions).

[IntelliJ Platform]: http://www.jetbrains.com/idea/
[Gerrit Code Review Tool]: http://code.google.com/p/gerrit/

You can install this plugin from the [IntelliJ Plugin Manager].
If you install this plugin directly in your IDE's plugin manager, you will get notified when a new release is available.
[IntelliJ Plugin Manager]: http://plugins.jetbrains.com/plugin/7272


Important Note if you have Authentication Issues
-----------------------------------------------
If you have correctly set up a HTTP Password in Gerrit, but still have authentication issues, your Gerrit instance
might be behind a HTTP Reverse Proxy (like Nginx or Apache) with enabled HTTP Authentication. You can identify that if
you have to enter an username and password (browser password request) for opening the Gerrit web interface. Since this
plugin uses Gerrit REST API (with authentication enabled), you need to tell your system administrator that he should
disable HTTP Authentication for any request to <code>/a</code> path (e.g. https://git.example.com/a). For these requests
HTTP Authentication is done by Gerrit (double HTTP Authentication will not work). For more information see
[Gerrit documentation].
[Gerrit documentation]: https://gerrit-review.googlesource.com/Documentation/rest-api.html#authentication


Architecture
------------
### IntelliJ Integration
The plugin is integrated into the IntelliJ IDE with a [tool window].
[tool window]: http://confluence.jetbrains.com/display/IDEADEV/IntelliJ+IDEA+Tool+Windows
See package <code>com.urswolfer.intellij.plugin.gerrit.ui</code>.

### REST API
Most of the communication between the plugin and a Gerrit instance is based on the [Gerrit REST API].
[Gerrit REST API]: https://gerrit-review.googlesource.com/Documentation/rest-api.html
See package <code>com.urswolfer.intellij.plugin.gerrit.rest</code>.

### Git
Some actions like comparing and listing files are based on Git operations. [IntelliJ Git4Idea] is used for these operations.
[IntelliJ Git4Idea]:http://git.jetbrains.org/?p=idea/community.git;a=tree;f=plugins/git4idea
See package <code>com.urswolfer.intellij.plugin.gerrit.git</code>.


Building the plugin
------------------

To build the plugin on your machine you need to have at least a downloaded copy of IntelliJ.
The plugin depends on multiple jars of IntelliJ IDEA but as these are not available via Maven Central, you'll have to
install the various Intellij jars located in the lib folder of your IntelliJ install into your local Maven repository.

For your convienience there is a bash script which will do exactly this for you
```
    $ cd gerrit-intellij-plugin/
    $ ./install-intellij-libs.sh <IntelliJ Version> <Path to IntelliJ>
```

To run the maven build you'll also need to install an updated version of [ideauidesigner-maven-plugin].
See that readme for installation instructions.
[ideauidesigner-maven-plugin]: https://github.com/gshakhn/ideauidesigner-maven-plugin/tree/12.x

Current issue: You need to change the scope of idea and forms_rt in pom.xml from provided to compile in order to
successfully build it with maven.

After you install all jars which this plugin needs into your local repo, just run

    mvn package

The resulting zip file will be located in the target folder.


Credits
------
* https://github.com/gshakhn/sonar-intellij-plugin/ for code examples (e.g. Maven integration, IntelliJ Plugin setup)
* IntelliJ Github plugin (some code of this plugin is based on its code)


Donations
--------
If you like this work, you can support it with [this donation link]. If you don't like Paypal
(Paypal takes 2.9% plus $0.30 per transaction fee from your donation), please contact me.
Please only use the link from github.com/uwolfer/gerrit-intellij-plugin to verify that it is correct.
[this donation link]: https://www.paypal.com/webscr?cmd=_s-xclick&hosted_button_id=8F2GZVBCVEDUQ


Copyright and license
--------------------

Copyright 2013 Urs Wolfer

Licensed under the Apache License, Version 2.0 (the "License");
you may not use this work except in compliance with the License.
You may obtain a copy of the License in the LICENSE file, or at:

  [http://www.apache.org/licenses/LICENSE-2.0](http://www.apache.org/licenses/LICENSE-2.0)

Unless required by applicable law or agreed to in writing, software
distributed under the License is distributed on an "AS IS" BASIS,
WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
See the License for the specific language governing permissions and
limitations under the License.
