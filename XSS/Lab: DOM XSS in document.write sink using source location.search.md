## As the title of This lab, it has vulnerability ,Dom XSS, in search input happend because the developer take the input from the user without any validation.

# Info
1. **queries**: URL parameters after `?`.
2. **URLSearchParams**: JavaScript object handels string into **queries** form.
3. **`window.location.search`**: return **queries** as string.
4. **`get`**: method returns the value of the given query. 
# Walk Through
## 1. Add random alphanumeric values in the search and notice that your input reflected on the page, so XSS is potentioal.
![image](https://user-images.githubusercontent.com/31960035/222966294-7af608ab-72ae-4234-ae12-d01b74e1491e.png)
## 2. inspect the page and notice that your input appears in the HTML.
![image](https://user-images.githubusercontent.com/31960035/222966410-b1d32637-2872-4158-b5e5-2d589ca1a256.png)
## 3. try to add some payloads like: `<script>alert(1)</script>`.
unfortunatly it doesn't work because the developer uses **HTML entities** which converts HTML symbols into form doesn't affect the page.
but when viewing the page source, we notice a JS script execute the search logic 
![image](https://user-images.githubusercontent.com/31960035/222966733-7f19c1d5-3221-40d4-9af7-d532d1c14f5b.png)
the developer takes the queries by `window.loaction.search` and pass it to `URLSearchParams` without any sanitization, so the exploitation may be here.
## 4. try to fail the logic of the DOM and execute `alert(1)`
### Try to fail the logic of `var query = (new URLSearchParams(window.location.search)).get('search');`
it's achievable by input `"alert(1)"` but it leads to only store the payload in the variable not execute it :(
#### explain `";alert(1)//`
1. the quote to end the string so it will be `var query = "";`
2. the `;` to end the variable statement to be `var query = "";;`
3. the alert(1) is clear
4. `//` for commenting remaining code to prevent interpreting errors.

### Try to fail the logic of 
```
if(query) {
  trackSearch(query);
 }
```
it's achievable by `');alert(1);//` but may stop payload execution cause of interpreting errors

### Try to fail the logic of `document.write('<img src="/resources/images/tracker.gif?searchTerms='+query+'">');`
acheivable by `" onload=alert(1) name="`
#### Explain
1. `"` to end the `src` and get `document.write('<img src="/resources/images/tracker.gif?searchTerms="">');`
2. `onload` to execute code when the image loaded
3. `name` is a random attribute to prevent potential error due to the quote at the end of `document.write('<img src="/resources/images/tracker.gif?searchTerms=" onload=alert(1)">');` after adding `name="` it will be `document.write('<img src="/resources/images/tracker.gif?searchTerms=" onload=alert(1) name="">');`
## SO:
![image](https://user-images.githubusercontent.com/31960035/222969404-2f9372e1-22f3-4ea7-b5cf-1e25c4e4409f.png)
