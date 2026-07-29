# Botsv1 Web Defacement: Complete Investigation Walkthrough
how I found the answers.

##### Understand the Incident
Reports indicate that the website www.imreallynotbatman.com has been compromised specifically through web defacement. 
My first objective is to determine if the website was really compromised. If confirmed, I will determine when the attack occurred and identify the affected web server.

Since this is a web defacement, the attacker most likely interacted with the web server using HTTP. I decided to begin by examining HTTP logs. 
We know that the index is botsv1 and  www.imreallynotbatman.com is a website. We dont know the source type it is. let us confirm first by this spl query:
