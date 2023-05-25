# Browser Technologies @cmda-minor-web 2022 - 2023

The course Browser Technologies is about learning to build robust and accessible websites using Progressive Enhancement and testing. Browser Technologies is part of the half year minor programme about Web Design and Development in Amsterdam. Bachelor Communication and Multimedia Design, Amsterdam University of Applied Science.

For Browser Technologies we had to research functionality, accessibility and (browser) support:

* How are different features supported by different browsers
* How to take care of a good fallback
* Test the functions on different (obscure) browsers

***

# Table of content
* Chosen user story
* Moodboard
* Email validation
* Dark mode
* CSS form on next page
* Javascript cache
* Browser test

## Chosen user story

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

## Moodboard

![Enquête moodboard](https://user-images.githubusercontent.com/40611000/230055295-310f823e-2971-4463-b48d-14314038b7a9.png)

*** 

## Email validation

To fill in a studentnumber that starts with 500 and has a total of 9 numbers.

And an email that has an @ and .something in it.

```HTML
<ul>
 <li>
  <input type="text" id="name" name="name" placeholder="Name*" required>
 </li>
  <li> 
   <input type="text" id="studentnumber" name="studentnumber" placeholder="Studentnumber*" pattern="500[0-9]{6}" required>
  </li>
  <li> 
    <input type="email" id="email" name="email" placeholder="Email*" pattern="[a-zA-Z0-9.!#$%&'*+/=?^_`{|}~-]+@[a-zA-Z0-9-]+(?:\.[a-zA-Z0-9-]+)*$" required>
  </li>
</ul>
```

```CSS
input[type=text]:valid {
    border-bottom: 3px solid rgb(75, 255, 175);
  }
  
input[type=text]:invalid {
    border-bottom: 3px solid red;
  }

input[type=text]:placeholder-shown:invalid {
    border-bottom: 3px solid black;
  }
```

***

## Dark mode

```CSS
@media (prefers-color-scheme: dark) {
    body{
        background: rgb(37, 37, 37);
    }

    main {
        background-color: rgb(53, 53, 53);
    }

    h1{
        color: white;
    }

    legend{
        color: white;
    }

    input{
        color: white;
        background-color: rgb(53, 53, 53);
    }

    input[type=text]:valid{
        color: white;
        background-color: rgb(53, 53, 53);
    }

    a{
        background: rgb(37, 37, 37);
    }

    a:hover{
        background: rgb(30, 30, 30);
    }

    input[type=submit]{
        background: rgb(37, 37, 37);
    }

    input[type=submit]:hover{
        background: rgb(30, 30, 30);
    }
}
```

***

## CSS form on next page

```CSS
form{
    display: none;
}

#personal:invalid a{
    background-color: grey;
    pointer-events: none;
    opacity: 30%;
}

form:first-of-type{
    margin-top: 5em;
}

fieldset{
    margin: 5em;
}

form#personal:target {
    display: block;
}

form#wafs:target{
    display: block;
}

form#cssttr:target{
    display: block;
}

form#pwa:target{
    display: block;
}
form#bt:target{
    display: block;
}

form#rtw:target{
    display: block;
}

form#hcd:target{
    display: block;
}
```

***

## Javascript cache

If you are filling in the form, I used Javascript to save your progress in the local storage.

```JS
const allForms = document.querySelectorAll('fieldset');
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

## Browser testing

I'm going to test the survey on different browsers and mobiles. The browsers I'm going to test are: Google Chrome, Mozilla Firefox, Safari and UC Browser. The mobiles I'm going to test on are iPhone, Huawei P30 lite and OnePlus 9 Pro (Chrome Browser).

### What do I want to test?
* Does the form validation work?
* Do the buttons work?
* Does it still work without CSS?
* Does it still work without Javascript?
* Is there a light and dark mode?

***

### Chrome light mode

<img src="https://github.com/DragonSake/browser-technologies-2223/assets/40611000/ecfaf680-472e-4b74-901a-ca707f6fd0be" width="260" />
<img src="https://github.com/DragonSake/browser-technologies-2223/assets/40611000/1e064103-b0ef-4c98-838f-98595d99b218" width="260" />
<img src="https://github.com/DragonSake/browser-technologies-2223/assets/40611000/a0cb434e-18c4-443c-bb71-89ca1bac8523" width="260" />

### Chrome dark mode  

<img src="https://github.com/DragonSake/browser-technologies-2223/assets/40611000/d2e9905a-71f6-452a-8c2b-7645acf444ad" width="260" />
<img src="https://github.com/DragonSake/browser-technologies-2223/assets/40611000/d2a9e486-88d7-40fe-994a-841095e4af44" width="260" /> 
<img src="https://github.com/DragonSake/browser-technologies-2223/assets/40611000/8b5d7ec0-9c20-4a27-bc3b-f6881def4b00" width="260" /> 

### Notes
* If the inputs are autofilled, then it changes the background-color of the inputfields.

### Checklist
- [X] Does the form validation work?
- [X] Do the buttons work?
- [X] Does it still work without CSS?
- [X] Does it still work without Javascript?
- [X] Is there a light and dark mode?

***

### Mozilla Firefox light mode

<img src="https://github.com/DragonSake/browser-technologies-2223/assets/40611000/72af5fd9-8f3e-4517-95b8-c70a80b9b640" width="260" />
<img src="https://github.com/DragonSake/browser-technologies-2223/assets/40611000/c62229e4-c682-4109-87f6-973b1e8ec6e9" width="260" />
<img src="https://github.com/DragonSake/browser-technologies-2223/assets/40611000/262be0ed-a7f1-49db-881a-80b310c979a8" width="260" />

### Mozilla Firefox dark mode

<img src="https://github.com/DragonSake/browser-technologies-2223/assets/40611000/f85fb099-2211-4405-84b7-bc5338d9bd2c" width="260" />
<img src="https://github.com/DragonSake/browser-technologies-2223/assets/40611000/6b0d1dea-c99e-4647-ae2c-45c8f99ac455" width="260" />
<img src="https://github.com/DragonSake/browser-technologies-2223/assets/40611000/42cb3a76-bdc7-4628-93e3-7652a7efdb08" width="260" />

### Checklist
- [X] Does the form validation work?
- [X] Do the buttons work?
- [X] Does it still work without CSS?
- [X] Does it still work without Javascript?
- [X] Is there a light and dark mode?

***

### Safari light mode

<img src="https://github.com/DragonSake/browser-technologies-2223/assets/40611000/2232e06a-c059-4109-a32f-0eb31521027a" width="260" />
<img src="https://github.com/DragonSake/browser-technologies-2223/assets/40611000/cc31a5eb-3905-4b24-856f-3cb3115259df" width="260" />
<img src="https://github.com/DragonSake/browser-technologies-2223/assets/40611000/d716d8d8-7388-48ea-8669-c312645eeba5" width="260" />
<img src="https://github.com/DragonSake/browser-technologies-2223/assets/40611000/6d7e91a4-b71a-4484-b7cc-2c48b8dda0d0" width="260" />

### Safari dark mode

<img src="https://github.com/DragonSake/browser-technologies-2223/assets/40611000/2d54d081-853e-420a-8a0c-8a7367f75555" width="260" />
<img src="https://github.com/DragonSake/browser-technologies-2223/assets/40611000/0cc469b5-9b07-4fc0-bd3d-0f498313ad9c" width="260" />
<img src="https://github.com/DragonSake/browser-technologies-2223/assets/40611000/6cb7c9ac-38e1-47b5-9255-31005189cf0d" width="260" />
<img src="https://github.com/DragonSake/browser-technologies-2223/assets/40611000/2f5c59e2-58cc-4dbd-8f4a-b0b7f906ffb0" width="260" />

### Checklist
- [X] Does the form validation work?
- [X] Do the buttons work?
- [X] Does it still work without CSS?
- [X] Does it still work without Javascript?
- [X] Is there a light and dark mode?

***

### UC Browser light mode

<img src="https://github.com/DragonSake/browser-technologies-2223/assets/40611000/2a8c5223-8fe2-4fd2-80ba-c1bd77d0ea45" width="260" />
<img src="https://github.com/DragonSake/browser-technologies-2223/assets/40611000/b84faba1-53af-4fbe-b18f-0487bf1204a5" width="260" />
<img src="https://github.com/DragonSake/browser-technologies-2223/assets/40611000/353843fa-488a-4e44-a5b7-62f2b0072c6e" width="260" />

### Notes
* Didn't find dark mode

### Checklist
- [X] Does the form validation work?
- [X] Do the buttons work?
- [X] Does it still work without CSS?
- [X] Does it still work without Javascript?
- [ ] Is there a light and dark mode?

***

## Mobile testing

### iOS light mode

<img src="https://github.com/DragonSake/browser-technologies-2223/assets/40611000/af5a0ed0-5c6f-4dc0-b4cc-489cc47a87a8" width="260" />
<img src="https://github.com/DragonSake/browser-technologies-2223/assets/40611000/dec5e70c-0e62-4666-89c0-7ce471525136" width="260" />
<img src="https://github.com/DragonSake/browser-technologies-2223/assets/40611000/4b508033-a406-49d2-96c6-f235124a7934" width="260" />

### iOS dark mode

<img src="https://github.com/DragonSake/browser-technologies-2223/assets/40611000/be80c2cf-9dbf-4333-9678-843ace9cdb7c" width="260" />
<img src="https://github.com/DragonSake/browser-technologies-2223/assets/40611000/66d8eb4d-9c4b-4d64-bc66-08c163ee3e97" width="260" />
<img src="https://github.com/DragonSake/browser-technologies-2223/assets/40611000/f1128e48-dcaa-447f-b244-99d3ef210e1b" width="260" />

### Notes
* Buttons are not always on the right place
* If the inputs are autofilled, then it changes the background-color of the inputfields.

### Checklist
- [X] Does the form validation work?
- [X] Do the buttons work?
- [X] Is there a light and dark mode?

***

### Huawei P30 Lite light mode

<img src="https://github.com/DragonSake/browser-technologies-2223/assets/40611000/ac977950-9768-46c1-afbc-2a78218e9b99" width="260" />
<img src="https://github.com/DragonSake/browser-technologies-2223/assets/40611000/9cfec596-3934-4514-8133-6f40fb95a9a2" width="260" />
<img src="https://github.com/DragonSake/browser-technologies-2223/assets/40611000/f72fd876-af2a-4e5b-8151-7ee53eb186c7" width="260" />

### Huawei P30 Lite dark mode

<img src="https://github.com/DragonSake/browser-technologies-2223/assets/40611000/f2135a72-beee-42a4-a66c-7551e699c96c" width="260" />
<img src="https://github.com/DragonSake/browser-technologies-2223/assets/40611000/53b5367e-6c5f-4ee8-bed9-aaa1335b6760" width="260" />
<img src="https://github.com/DragonSake/browser-technologies-2223/assets/40611000/04cc5410-e3b7-4813-a3ab-a64c5b968137" width="260" />

### Notes
* Buttons are not always on the right place

### Checklist
- [X] Does the form validation work?
- [X] Do the buttons work?
- [X] Is there a light and dark mode?

***

### OnePlus 9 Pro (Chrome Browser) dark mode

<img src="https://github.com/DragonSake/browser-technologies-2223/assets/40611000/cad57051-88b1-4565-af64-01499132022b" width="260" />
<img src="https://github.com/DragonSake/browser-technologies-2223/assets/40611000/ca44254d-0500-4e2a-b6f2-cb727a2937e3" width="260" />
<img src="https://github.com/DragonSake/browser-technologies-2223/assets/40611000/a671b744-7aff-40cf-9d05-b2f4d6d02050" width="260" />
<img src="https://github.com/DragonSake/browser-technologies-2223/assets/40611000/497bb98f-857a-4891-972a-9b475ae1c2a2" width="260" />

### Notes
* Can't click on the labels
* Buttons are not always on the right place

### Checklist
- [X] Does the form validation work?
- [X] Do the buttons work?
- [X] Is there a light and dark mode?

***

## Mobile button fix

```CSS
div{
    display: flex;
    justify-content: center;
    margin: 0 auto;
}

div ul{
    display: grid;
}

div ul li{
    margin: 3em auto;
}

div a{
    margin: 0 auto 1em auto;
}
```

<img src="https://github.com/DragonSake/browser-technologies-2223/assets/40611000/ec482aa9-9460-4ca7-b043-e6c35cddad97" width="260" />

***

## CSS disabled

If the CSS is disabled, you'll see the whole form on one page instead of parts of the form.

![screencapture-127-0-0-1-5500-2023-05-25-16_18_53](https://github.com/DragonSake/browser-technologies-2223/assets/40611000/133ed729-31bb-407d-b642-42e5335ddb68)

***

## Javascript disabled

If the Javascript is enabled, every answer you filled in will be saved in the local storage.
If the Javascript is disabled, then the form won't be saved. Everything you filled in will be deleted when you close the tabblad and then you can't continue to fill in the form where you left off.

***

