## Tips & Tricks

#### Configuration of  Jenkins

- Use [supervisor](http://supervisord.org) to run the Java process on **slaves** which connects to your **master**. You can use the SSH plugin but is more tedious.
- Integrate authentication system with [LDAP](https://wiki.jenkins-ci.org/display/JENKINS/LDAP+Plugin), if you are using it - if not, do so. Also, create a user for the **slaves** to connect to **master**.
- Use [Discard Old Build Plugin](https://wiki.jenkins-ci.org/display/JENKINS/Discard+Old+Build+plugin) to clean your jobs history, otherwise your disk will be full in no time,
or you will be left without inode space.

### More

You can find out more about optimizing Jenkins in [this article](http://www.cloudbees.com/sites/default/files/whitepapers/7WaysToOptimizeJenkins.pdf).
