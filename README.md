Automated Deployment of Java Applications to Apache Tomcat using Jenkins.
=========================================================================

![Devops Mini Porject](https://miro.medium.com/v2/resize:fit:1400/format:webp/1*oGtIwKVjsPF7AzhSNu_WpQ.png)

[Reference](https://medium.com/@nikhilsiri2003/automated-deployment-of-java-applications-to-apache-tomcat-using-jenkins-63e593cd0696)

by [Nikhil Raj A](https://medium.com/@nikhilsiri2003?source=post_page---byline--63e593cd0696---------------------------------------)

**Introduction**
----------------

This project aims to automate the deployment of Java applications to an Apache Tomcat server using Jenkins. Instead of manually building and copying `.war` files, we use a CI/CD pipeline where Jenkins pulls code from a Git repository, builds it using Maven, and deploys it to Tomcat automatically. This streamlines the development process, reduces human error, and enables faster, more reliable application delivery, following modern DevOps practices.

![workflow of the project](https://miro.medium.com/v2/resize:fit:1400/format:webp/1*oMozmovOngL95mnnnQzCow.png)

Why This Project?
=================

Manual deployment of Java applications is time-consuming and error-prone. This project solves that by introducing **automation** using Jenkins, which ensures that every time code is updated, it is **built, tested, and deployed automatically** to a Tomcat server. It saves developer time, reduces bugs, and supports faster and more reliable software delivery — all of which are essential in modern **DevOps** and **agile** environments.

Prerequsities :
---------------

*   Tomcat Server
*   Jenkins Server
*   A java Project

References
----------

*   **Tomcat Setup** : [https://github.com/NikhilRaj-2003/java-web/blob/main/src/main/webapp/Installations%20/apache%20tomcat/Tomcat%20Installation%20on%20Amazon-Linux-2.md](https://github.com/NikhilRaj-2003/java-web/blob/main/src/main/webapp/Installations%20/apache%20tomcat/Tomcat%20Installation%20on%20Amazon-Linux-2.md)
*   **Jenkins** : [https://github.com/NikhilRaj-2003/java-web/blob/main/src/main/webapp/Installations%20/Jenkins/Jenkins%20Installation%20on%20Amazon-Linux-2.md](https://github.com/NikhilRaj-2003/java-web/blob/main/src/main/webapp/Installations%20/Jenkins/Jenkins%20Installation%20on%20Amazon-Linux-2.md)
*   **Java Project** : [https://github.com/NikhilRaj-2003/java-web.git](https://github.com/NikhilRaj-2003/java-web.git)

 Step — 1 : Install Git into your Jenkins server
-----------------------------------------------

1.  install git and check the git version .

```
# Become a root 
sudo su -
# Install git.
yum install git -y
# Check Version of git.
git --version
```

2. Open Jenkins in web-browser, click on manage jenkins then select Global Tool Configuration.

![captionless image](https://miro.medium.com/v2/resize:fit:1400/format:webp/0*aaDZAB5jgvdrGdSX.jpg)

3. Then under Global tool configuration , add git in Git Installations

![captionless image](https://miro.medium.com/v2/resize:fit:1400/format:webp/0*GnMr7wQrl_xu8YKC.jpg)

4. In git installations , click **Add git** then select git.

![captionless image](https://miro.medium.com/v2/resize:fit:1400/format:webp/0*1zg2ubmS5TT3UOn-.jpg)![captionless image](https://miro.medium.com/v2/resize:fit:1400/format:webp/0*o2DMBonmURiFUNWp.jpg)

5. Enter the Git name and path , later click **apply and save**

![captionless image](https://miro.medium.com/v2/resize:fit:1400/format:webp/0*xvtVIhbQ3MlRCkOj.jpg)

6. Now we have successfully integrated Git with Jenkins . Then click on **Global Tool Configuration ,** under that go to **Maven installtions .** After giving the details click on **apply and save .**

![captionless image](https://miro.medium.com/v2/resize:fit:1400/format:webp/0*XxuUHvhzdgUSGf61.jpg)

> Now **Maven** is also successfully integrated with jenkins .

Steps — 2 : Install a Plugin called ‘Deploy to container ‘
----------------------------------------------------------

1.  Go to **manage jenkins > plugins > Available plugins > Deploy to container .**

![captionless image](https://miro.medium.com/v2/resize:fit:1400/format:webp/0*ky81Viuv6Wrahi58.jpg)

2. Click on the **restart jenkins after installations ,** after the installations the jenkins will restart and you need to enter the username and password .

![captionless image](https://miro.medium.com/v2/resize:fit:1400/format:webp/0*xKglVtLKkl1nNrMy.jpg)

step — 3 : Create a Global Credentials
--------------------------------------

1.  Go to **Credentials > Select system > Select Global Credentials** then click on **Add Credentials .**

![captionless image](https://miro.medium.com/v2/resize:fit:1400/format:webp/0*8zYZ7098AYxRwvS4.jpg)

2. After clicking on add credentials , Enter the **username** and **password**

![captionless image](https://miro.medium.com/v2/resize:fit:1366/format:webp/1*d9XhwQuiB3LIVfxdrIQaCQ.png)

3. Once your done giviing the details , then you can see the credentails you have created .

![captionless image](https://miro.medium.com/v2/resize:fit:1400/format:webp/1*h_BQcwadqSrIDCgcneBQVA.png)

Step — 4: Create a Jenkins Job
------------------------------

1.  Head to **Dashboard > New Item ,** then provide a name for the jenkins job and select **freestyle project** as project type .

![captionless image](https://miro.medium.com/v2/resize:fit:1400/format:webp/1*a1vw8_UZRlWQsDUQU1OLBg.png)

2. Enter the **github repo** and also **change the branch name from master to main ,** because there is no master branch .

![captionless image](https://miro.medium.com/v2/resize:fit:1400/format:webp/1*zVA_rKBl1zcBZ_c_wjwdIA.png)

3. Under **Build steps > invoke top level maven targets ,** then provide maven command ‘ **clean package’ .** And there is no need to mention **mvn** as we give in the terminal , it automatically takes as mvn and then runs the command .

![captionless image](https://miro.medium.com/v2/resize:fit:1400/format:webp/0*gjHUWqNNno4sjfZz.jpg)

4. In Post-build Actions click Add Post-build Actions and Select **Deploy war/ear to container.**

![captionless image](https://miro.medium.com/v2/resize:fit:1400/format:webp/0*Jqe8iOaqF2iwyOme.jpg)

5. Enter the details as following then click on **apply and save.**

![captionless image](https://miro.medium.com/v2/resize:fit:1152/format:webp/1*HWc8BRPtLYjLQmz4Mn8gPw.png)

> Now Click on **Build Now**

![captionless image](https://miro.medium.com/v2/resize:fit:1400/format:webp/1*0oLwd1x0YO8P7G86Cy9llQ.png)

> The Build is Successfull .

![captionless image](https://miro.medium.com/v2/resize:fit:1400/format:webp/1*re5_IH3OwX9578ugXHoBAg.png)

Output of the project
---------------------

![Web application deployed](https://miro.medium.com/v2/resize:fit:1400/format:webp/1*BxAsoGGsMOC7GHIcuvoXWg.png)

Why to use Github Webhook ?
---------------------------

Using a **GitHub webhook** with **Jenkins** allows you to **automatically trigger a build and deploy** your Java web application whenever someone pushes code to your GitHub repository.

Step — 5 : Automate Build and Deploy using Github webhook
---------------------------------------------------------

1.  Go to **Github Account > Settings > Webhook ,** then create a webhook.

*   Payload URL is **public ip if jenkins server.**

```
http://<public-ip address>:8080/github-webhook/
```

*   Set content type as **application/JSON .**
*   Select Event Trigger as **just the push event .e**

![captionless image](https://miro.medium.com/v2/resize:fit:1400/format:webp/1*AJluDIFFXuhU6rGULozXMA.png)

2. Then go to **jenkins dashboard > tomcat-jenkins > configure > Triggers,** there you need to enable the **Github hook trigger for GITscm polling.**

![captionless image](https://miro.medium.com/v2/resize:fit:1400/format:webp/1*DF0Ytnc8D4tBOA5ctl2Ipg.png)

3. Whenever there is a commit / changes made in the java web — application , then the webhook will automatically create build . Later click on **Commit .**

![captionless image](https://miro.medium.com/v2/resize:fit:1400/format:webp/1*x49bjsOBknofDcSTMF_f6A.png)

4. After the Changes made when you click on commit , a build will be created in jenkins dashboard automatically where it **builds** and **deploys** the web application with (._war )_ file.

![captionless image](https://miro.medium.com/v2/resize:fit:1400/format:webp/1*Zg5Jm6gTZA36sUEliWT7Wg.png)

5. The changes made in github repository will be automatically changed in the web — application without any manual intervention . Webhook trigger whenever there is a commit in that repository .

![Final output of web application](https://miro.medium.com/v2/resize:fit:1400/format:webp/1*IB9s0wOtuDbFo2II9SEhJw.png)

Conclusion
----------

This mini project successfully demonstrates a **CI/CD pipeline** where a Java web application is automatically **built and deployed to Apache Tomcat using Jenkins**. By integrating **GitHub Webhooks**, the pipeline is triggered instantly upon every code push, ensuring that the latest changes are continuously tested and deployed without manual intervention.
