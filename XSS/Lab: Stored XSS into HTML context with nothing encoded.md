this lab is just to learn you what is the **stored XSS**
# Walk Through
## 1. test each input (URL parameter, search, comment or any form).
### the first step to search for XSS is to tset each input field. after searching you will find a text input recieves a comment from the user
![image](https://user-images.githubusercontent.com/31960035/222964529-c8a93f08-0310-4782-9334-981004b07327.png)
## 2. Try random alphanumeric number and notice that it's reflected to the page, so XSS is potential.
![image](https://user-images.githubusercontent.com/31960035/222964604-af7580e0-b8e6-4e97-8133-d21a7d54cb43.png)
<hr>

![image](https://user-images.githubusercontent.com/31960035/222964852-87c4a28b-b6b0-4d53-82d9-2735895bf6b1.png)
## 3. inject some JS code, let's try `<script>alert(1)</script>`.
### alert displayed
![image](https://user-images.githubusercontent.com/31960035/222964955-1adf3c11-8de8-402d-82be-1787db2727e3.png)
## SO:

![image](https://user-images.githubusercontent.com/31960035/222964957-1051084e-a447-483d-87ee-433b46d242f2.png)
