# Browser Technologies @cmda-minor-web 2022 - 2023

The course Browser Technologies is about learning to build robust and accessible websites using Progressive Enhancement and testing. Browser Technologies is part of the half year minor programme about Web Design and Development in Amsterdam. Bachelor Communication and Multimedia Design, Amsterdam University of Applied Science.

For Browser Technologies we had to research functionality, accessibility and (browser) support:

* How are different features supported by different browsers
* How to take care of a good fallback
* Test the functions on different (obscure) browsers

***

## Table of content
* Chosen user story
* Moodboard
* HTML validation
* CSS form on next page
* Javascript cache
* Browser test
* Obscure browser

### Chosen user story

Survey about the minor Web Design and Development

Requirements for the survey:

* Student data (name + studentnumber) required
* Per subject
   - Name
   - Teacher(s)
   - Weeks in which you did the course
   - Rating on a scale of 1-10 how difficult it was
   - Rating on a scale of 1-10 how cleary it is explained
   - Rating on a scale of 1-10 how well did you understand it
   - Make sure the user doesn't see too many form fields at once

* Validation: make sure that the form is filled in completely. Provide clear error messages. Decide for yourself when and how the validation will take place
* If I don't finish the survey, I want to pick up where I left off
* Clear interface that allows users to return to previous questions. (And maybe also skip a question?)
* Clear interface that indicates where you are in the form
* You may not use visible radio buttons
* The form must have a light mode and dark mode

***

### Moodboard

![Enquête moodboard](https://user-images.githubusercontent.com/40611000/230055295-310f823e-2971-4463-b48d-14314038b7a9.png)

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
