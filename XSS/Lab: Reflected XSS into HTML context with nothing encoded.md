## That is the simplest lab as there is no any sanitization or security mechanism.
# Walk Through
## 1. Type any alphanumeric text and notice that it's reflected on the page.
![image](https://user-images.githubusercontent.com/31960035/222963604-94f4a873-6d1e-4a5e-84d5-35c52e90ffad.png)
## 2. inspect the page and notice your input is displayed in the HTML, so XSS attack is potential.
![image](https://user-images.githubusercontent.com/31960035/222963805-87f01c2f-a6a2-496b-8616-32ac6003b2be.png)
## 3. try to put any malicious payload, let's try: `<img src=x onerror=alert(1)>`
### this payload adds an image from unfound source so it will produce an error and execute `onerror` event which execute `alert(1)` and the lab will be solved.
![image](https://user-images.githubusercontent.com/31960035/222964035-95f6cd98-728f-4d00-a145-05f833f43797.png)
![image](https://user-images.githubusercontent.com/31960035/222964038-19c8a04c-1561-4355-9716-08c8d063a4ac.png)
