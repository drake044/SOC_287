# SOC287 - Arbitrary File Read on Checkpoint Security Gateway [CVE-2024-24919] [Let’s Defend]

Hello Guardians,
This writeup is a detailed walkthrough of  Lets Defend Lab - SOC287. 

![image.png](SOC287%20-%20Arbitrary%20File%20Read%20on%20Checkpoint%20Securit%2054f2405b780549d3a338990c29c20f1f/image.png)

1. Create the case from the investigations channel.

![image.png](SOC287%20-%20Arbitrary%20File%20Read%20on%20Checkpoint%20Securit%2054f2405b780549d3a338990c29c20f1f/image%201.png)

2. Start the playbook 

![image.png](SOC287%20-%20Arbitrary%20File%20Read%20on%20Checkpoint%20Securit%2054f2405b780549d3a338990c29c20f1f/image%202.png)

![image.png](SOC287%20-%20Arbitrary%20File%20Read%20on%20Checkpoint%20Securit%2054f2405b780549d3a338990c29c20f1f/image%203.png)

![image.png](SOC287%20-%20Arbitrary%20File%20Read%20on%20Checkpoint%20Securit%2054f2405b780549d3a338990c29c20f1f/image%204.png)

3. Common guide to assist in how to investigate an alert with proper precision.

![image.png](SOC287%20-%20Arbitrary%20File%20Read%20on%20Checkpoint%20Securit%2054f2405b780549d3a338990c29c20f1f/image%205.png)

4. Now we have to check  whether the traffic was malicious or not from the sources available to us.

![image.png](SOC287%20-%20Arbitrary%20File%20Read%20on%20Checkpoint%20Securit%2054f2405b780549d3a338990c29c20f1f/image%206.png)

5. Checking the Source IP  address (203.160.68.12) on virus total platform. Which shows certain vendors have flagged this as malicious. 

![image.png](SOC287%20-%20Arbitrary%20File%20Read%20on%20Checkpoint%20Securit%2054f2405b780549d3a338990c29c20f1f/image%207.png)

6. Checking the Threat Intel database of Lets Defend to check whether is it listed there or not , if yes then in which type. On investigating it checks out that its tagged the the CVE-2024-24919 vulnerability.

![image.png](SOC287%20-%20Arbitrary%20File%20Read%20on%20Checkpoint%20Securit%2054f2405b780549d3a338990c29c20f1f/image%208.png)

7. Now we are sure that the traffic is malicious.

![image.png](SOC287%20-%20Arbitrary%20File%20Read%20on%20Checkpoint%20Securit%2054f2405b780549d3a338990c29c20f1f/image%209.png)

8. Now go to log management   and check for  was the attackers request sucessfull
and what was the attacker trying to accomplish.

 

![image.png](SOC287%20-%20Arbitrary%20File%20Read%20on%20Checkpoint%20Securit%2054f2405b780549d3a338990c29c20f1f/image%2010.png)

9. previously we know that it was the attackers request , lets quicky search for the vulnerability on gihub to know more  more about the payload .

![image.png](SOC287%20-%20Arbitrary%20File%20Read%20on%20Checkpoint%20Securit%2054f2405b780549d3a338990c29c20f1f/image%2011.png)

10. We can see that  the request was actually a well crafted payload to access
important files on  the system  like /etc/passwd or shadow file which contains user information with the root priviledges , in the next step lets see if the 
requested was accepted and the payload was executed or not to check if the system is compromised or not .

![image.png](SOC287%20-%20Arbitrary%20File%20Read%20on%20Checkpoint%20Securit%2054f2405b780549d3a338990c29c20f1f/image%2012.png)

11. As we can see the logs.  we can clearly see that we have a response code 200 on the attacker’s request which means the attackers request was executed succesfully.

![image.png](SOC287%20-%20Arbitrary%20File%20Read%20on%20Checkpoint%20Securit%2054f2405b780549d3a338990c29c20f1f/image%2013.png)

12. Basically the answer to this is lfi and rfi , as  this vulnerability allows the  attacker to access and read  any file on the affected system , icluding sensitive system files containing password hashes by manipulating  file paths;

![image.png](SOC287%20-%20Arbitrary%20File%20Read%20on%20Checkpoint%20Securit%2054f2405b780549d3a338990c29c20f1f/image%2014.png)

13. To answer this we  have to check in the email security sections to  make a decision whether this was a planned testing or an anauthorized  breach.

![image.png](SOC287%20-%20Arbitrary%20File%20Read%20on%20Checkpoint%20Securit%2054f2405b780549d3a338990c29c20f1f/image%2015.png)

14. There’s no evidence which suggests whether the attack was planned , hence we will go with not planned.

![image.png](SOC287%20-%20Arbitrary%20File%20Read%20on%20Checkpoint%20Securit%2054f2405b780549d3a338990c29c20f1f/image%2016.png)

15. The answer is pretty straight forward which is  Internet —> Company Network as  the source ip is an External ip. 

![image.png](SOC287%20-%20Arbitrary%20File%20Read%20on%20Checkpoint%20Securit%2054f2405b780549d3a338990c29c20f1f/image%2017.png)

16. Oh yes the attack was succesfull as seen in  step 11 , feel free to check again, we saw that the response code recieved and logged was 200 which means a green flag for the  attacker/s requests.

![image.png](SOC287%20-%20Arbitrary%20File%20Read%20on%20Checkpoint%20Securit%2054f2405b780549d3a338990c29c20f1f/image%2018.png)

17. Since we know that the device CP-Spark-Gateway-01 is compromised we have to isolate it from the company network so that no more further damage is possible.

![image.png](SOC287%20-%20Arbitrary%20File%20Read%20on%20Checkpoint%20Securit%2054f2405b780549d3a338990c29c20f1f/image%2019.png)

18. To contain it we simply have to search the device in endpoint security section.

![image.png](SOC287%20-%20Arbitrary%20File%20Read%20on%20Checkpoint%20Securit%2054f2405b780549d3a338990c29c20f1f/image%2020.png)

19. Turn device Containment on  to isolate the device from the network.

![image.png](SOC287%20-%20Arbitrary%20File%20Read%20on%20Checkpoint%20Securit%2054f2405b780549d3a338990c29c20f1f/image%2021.png)

20. Add relevant artifacts to the investigation 

Attackers’s ip : 203.160.68.12

Victim’s ip :  172.16.20.146 [CP-Spark-Gateway-01] 

Payload used by the attacker :  aCSHELL/../../../../../../../../../../etc/passwd [path traversal]

![image.png](SOC287%20-%20Arbitrary%20File%20Read%20on%20Checkpoint%20Securit%2054f2405b780549d3a338990c29c20f1f/image%2022.png)

21.   Yes it is required because the attack was successful/

![image.png](SOC287%20-%20Arbitrary%20File%20Read%20on%20Checkpoint%20Securit%2054f2405b780549d3a338990c29c20f1f/image%2023.png)

22. write a note to summarize your investigation.

![image.png](SOC287%20-%20Arbitrary%20File%20Read%20on%20Checkpoint%20Securit%2054f2405b780549d3a338990c29c20f1f/image%2024.png)

23. finish the playbook.

![image.png](SOC287%20-%20Arbitrary%20File%20Read%20on%20Checkpoint%20Securit%2054f2405b780549d3a338990c29c20f1f/image%2025.png)

24. Click on close alert 

![image.png](SOC287%20-%20Arbitrary%20File%20Read%20on%20Checkpoint%20Securit%2054f2405b780549d3a338990c29c20f1f/image%2026.png)

25. write a note to close the alert and mark it as a true positive as the alert was genuine and after that close that alert.

---
