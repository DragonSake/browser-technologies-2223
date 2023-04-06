# Browser Technologies @cmda-minor-web 2022 - 2023

The course Browser Technologies is about learning to build robust and accessible websites using Progressive Enhancement and testing. Browser Technologies is part of the half year minor programme about Web Design and Development in Amsterdam. Bachelor Communication and Multimedia Design, Amsterdam University of Applied Science.

***

# Table of content
* HTML validation
* CSS form on next page
* Javascript cache
* Browser test
* Obscure browser

*** 

### HMTL validation

To fill in a studentnumber that starts with 500 and has a total of 9 numbers.

And an email that has an @ and .something in it.

```HTML
<input type="text" id="studentnumber" name="studentnumber" placeholder="Studentnumber*" pattern="500[0-9]{6}" required>
  </li>
  <li> 
    <input type="email" id="email" name="email" placeholder="Email*" pattern="[a-zA-Z0-9.!#$%&'*+/=?^_`{|}~-]+@[a-zA-Z0-9-]+(?:\.[a-zA-Z0-9-]+)*$" required>
  </li>
```

***

### CSS form on next page

```CSS

```

***

### Javascript cache

If you are filling in the form, I used Javascript to save your progress in the local storage.

```JS
const allForms = document.querySelectorAll('form');
const maxForms = 7;

if (window.localStorage) {
 const allSubmitInputs = document.querySelectorAll('input[type="submit"]');

 allSubmitInputs.forEach(elem => {
  elem.classList.add("invisible");
	});

 var formData = {
 forms: {}
 }

 function generateJsonFromForm(formID) {
  var form = {}
  const elements = Array.from(document.querySelectorAll(`#${formID} input:not([type="submit"]), #${formID} select`));
  elements.forEach(elem => {
    const elementName = elem.getAttribute('name');
    const elementValue = elem.value;
    form[elementName] = elementValue;
   })

 formData.forms[formID] = form;

 const formJSON = JSON.stringify(form);
 return formJSON;
	}

 async function putFormDataInLocalStorage(key, formJSON) {
 window.localStorage.setItem(key, formJSON);
	}

 function putFormInputValuesBackFromLocalStorage() {
  allForms.forEach(elem => {
  const formID = elem.getAttribute('id');

  if (window.localStorage.getItem(formID)) {
   const localStorageData = JSON.parse(window.localStorage.getItem(formID));

   Object.keys(localStorageData).forEach(key => {
    const inputElement = document.querySelector(`#${formID} input[name="${key}"], #${formID} select[name="${key}"]`);
    inputElement.value = localStorageData[key];
				})
			}
		})
	}

   putFormInputValuesBackFromLocalStorage()

   allForms.forEach(elem => {
     elem.addEventListener('input', event => {
	const formID = elem.getAttribute('id');
	const formJSON = generateJsonFromForm(formID);
	putFormDataInLocalStorage(formID, formJSON);
		})
	})
}
```
