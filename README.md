# Form 1: Registro de pacientes 
-----
## Information and suggested changes
- URL: [Registro de pacientes](https://consultas-panama.web.app/#/register)
- inputs: 4
- FHIR inputs: 2

| FHIR | Input /Placeholder | id/name     | Required   | objectData |
| ---- | ------------------ | ----------- |-----------|----------- |
|  🔥  |  Nombre            | name        | true      | name       |
|  🔥  |  Apellido          | lastName    | true      | lastname   |
|      |  Email             | email       | true      |            |
|      |  Password(*)       | password    | true      |            |

(*) Change placeholder: Password ▶ Contraseña 

---

## Example **XHR** request-response (req-res)

- ### Objective: **Create a Patient**
- ### FHIR url: https://app-ryjgytpm5q-uc.a.run.app/api/consultas/fhir/v1/Patient
- ### method = **POST**
- ### Headers = 
  - Content-Type: **application/json**

```javascript
document.getElementById("form_1_form").addEventListener("submit", (e)=>
        {
            e.preventDefault();
            forma1();
        });
```

```javascript
// create the objectDataString
let name = document.getElementById('name').value;
let lastname = document.getElementById('lastName').value;
let objectData = {
  name : name,
  lastname : lastname,
  use : 'official'
};
let objectDataString = JSON.stringify(objectData);
```

```javascript
// url
let url = 'https://app-ryjgytpm5q-uc.a.run.app/api/consultas/fhir/v1/Patient'
// xhr req
let xhr = new XMLHttpRequest();
xhr.responseType = 'json';
xhr.open('POST', url, true);
xhr.setRequestHeader('Content-Type','application/json');
xhr.onload = function(){
  if(xhr.status == 200){
    let resp = xhr.responseText
    // save the response id and 
    // send the original form to the database
    // with (new input) fhir_id_pacient
    }
};
xhr.onerror = function(){
// xyz error handler...
};
xhr.send(objectDataString)
```

```javascript
//Form 1 Function
document.getElementById("form_1_form").addEventListener("submit", (e)=>{
  e.preventDefault();
  forma1();
});
function forma1(){
  let name = document.getElementById('name').value;
  let lastname = document.getElementById('lastName').value;
  let objectData = {
    name : name,
    lastname : lastname,
    use : 'official'
    };
  let objectDataString = JSON.stringify(objectData);
  // url
  let url = 'https://app-ryjgytpm5q-uc.a.run.app/api/consultas/fhir/v1/Patient'
  // xhr req
  let xhr = new XMLHttpRequest();
  xhr.responseType = 'json';
  xhr.open('POST', url, true);
  xhr.setRequestHeader('Content-Type','application/json');
  xhr.onload = function(){
    if(xhr.status == 200){
      let jsonResponse = xhr.response;
      let resp_final = jsonResponse['fhir_id_patient']
      document.getElementById('target_value').innerHTML = resp_final; 
      document.getElementById('target_value').value = resp_final;
      document.getElementById("ver_respuestas").style.display = "block";
      };
    };
    xhr.onerror = function(){
      // error 
    };
    xhr.send(objectDataString);
};
```

#### after receive the resp object
#### use the **responseText** as a value for a new key:value pair 
#### [ **fhir_id_pacient** : xhr.responseText ]

---
## req:
```json
{
	"name": "juan",
	"lastname": "nadie",
	"use": "official"
}
```
## resp:
```json
{
  "fhir_id_patient": "450db9bc-0613-4ebb-aab5-595797290fcd"
}
```

# Form 2: Registro de Doctor 
-----
## Information and suggested changes
- URL: [Registro de Doctor](https://consultas-panama.web.app/#/register)
- inputs: 4
- FHIR inputs: 2

| FHIR | Input /Placeholder | id/name     | Required   | objectData |
| ---- | ------------------ | ----------- |-----------|----------- |
|  🔥  |  Nombre            | name        | true      | name       |
|  🔥  |  Apellido          | lastName    | true      | lastname   |
|      |  Email             | email       | true      |            |
|      |  Password(*)       | password    |true       |            |

(*) Change placeholder: Password ▶ Contraseña 

---

## Example **XHR** request-response (req-res)

- ### Objective: **Create a Practitioner**
- ### FHIR url: https://app-ryjgytpm5q-uc.a.run.app/api/consultas/fhir/v1/Practitioner
- ### method = **POST**
- ### Headers = 
  - Content-Type: **application/json**

```javascript
// create the objectDataString
let name = document.getElementById('name').value;
let lastname = document.getElementById('lastName').value;
let objectData = {
  name : name,
  lastname : lastname,
  use : 'official'
};
let objectDataString = JSON.stringify(objectData);
```

```javascript
// xhr req
let xhr = new XMLHttpRequest();
xhr.open('POST', url, true);
xhr.setRequestHeader('Content-Type','application/json');
xhr.onload = function(){
  if(xhr.status == 200){
    let resp = xhr.responseText
    // save the response id and 
    // send the original form to the database
    // with (new input) fhir_id_pacient
    }
};
xhr.onerror = function(){
// xyz error handler...
};
xhr.send(objectDataString)
```

#### after receive the resp object
#### use the **responseText** as a value for new key:value pair 
#### [ **fhir_id_practitioner** : xhr.responseText ]

---
## Example req
```json
{
	"name": "juana",
	"lastname": "nadie",
	"use": "official"
}
```
## Example resp
```json
{
  "fhir_id_practitioner": "f4d497dc-faed-4367-a538-13fff37b0580"
}
```

# Form 3: Editar Perfil (Patient)
-----
## Information and suggested changes

### Base Form
- URL: [Forma de perfil (Paciente)](https://consultas-panama.web.app/#/patients/settings)
- inputs: 10
- FHIR inputs: 6

| FHIR | Input /Placeholder | id/name     | Required   | objectData |
| ---- | ------------------ | ----------- |-----------|----------- |
|  🔥  |  Nombre            | name        | true      | name       |
|  🔥  |  Apellido          | lastName    | true      | lastname   |
|  🔥  |  Numero de contacto| phone       | true      | name       |
|      |  Nacionalidad (+)     | nationality |true       |         |
|  🔥  |  Género            | gender      | true      | gender       |
|      |  Grupo Sanguíneo   | bloodType   | false     |            |
|  🔥  |  Nacimiento        | dob         | true      | dob       |
|  🔥  |  Cédula o pasaporte | document   | true      | identifier       |
|      |  Cédula o pasaporte(++) | file    | true      |            |

(+) Nationality or country of residence?  
(++) Género ➡ Género biologico asignado al nacer  
(+++) Change placeholder [duplicated]: Cédula o pasaporte ➡ Foto de cédula o pasaporte 

### **Inputs to add**
- new inputs: 16
- hidden inputs: 1
- autocalc inputs: 1
- FHIR inputs: 11

| FHIR | Input /Placeholder | id/name     | Required   | objectData | type |
| ---- | ------------------ | ----------- |-----------|----------- | ------ |
|  🔥  |  idioma(+++)            | language     | true      | language  | string |
|  🔥  |  ubicación          | address_line    | true      | address_line   | string |
|  🔥  | ciudad | address_city       | true      | address_city       | string |
|  🔥  | distrito | address_district       | true      | address_district       | string |
|  🔥  | provincia | address_state      | true      | address_state       | string |
|  🔥  | pais | address_country       | true      | address_country       | string |
|  | altura | heigth       | true      |        | string |
|  | peso | weigth       | true      |        | string |
| {autocalc} | imc | bmi       | true      |        | string |
| 🔥 | fhir ID | fhir_id_pacient       | true      | fhir_id_pacient       | string |
|   (+) | contacto de urgencia | contact_bool       | false      |        | bool |
|  🔥{disp(++)}  |  Nombre            | name_contact        | true      | name_contact       | string
|  🔥 {disp} |  Apellido          | lastName_contact    | true      | lastname_contact   | string
|  🔥 {disp} |  Género            | gender_contact      | true      | gender_contact       | string
|  🔥 {disp} |  Numero de contacto| phone_contact       | true      | phone_contact       | string
|  🔥 {disp} |  email            | email_contact      | true      | email_contact       | string

(+) use a boolean variable (default==False) if change to True then display the **disp** variables. (Trigger a popup, show hidden varaibles, ...)

(++) **disp** = display if contact_bool == True

(+++)**idioma**
  - fetch ➡ from valid URL languages: https://app-ryjgytpm5q-uc.a.run.app/api/consultas/fhir/v1/languages
  - type: string
  - description: dropdown + search 
  
--- 

## Example **XHR** request-response (req-res)

- ### Objective: **Update or Insert patient data**
- ### FHIR url: https://app-ryjgytpm5q-uc.a.run.app/api/consultas/fhir/v1/Patient
- ### method = POST
- ### Headers = 
  - Content-Type: application/json

```javascript
// create the objectDataString
let name = document.getElementById('name').value;
let lastname = document.getElementById('lastName').value;
let phone = document.getElementById('phone').value;
let gender = document.getElementById('gender').value;
let dob = document.getElementById('dob').value;
let personaldocument = document.getElementById('document').value;
let objectData = {
  name : name,
  lastname : lastname,
  phone : phone,
  gender : gender,
  dob : dob,
  personaldocument : personaldocument
};
let objectDataString = JSON.stringify(objectData);
```

```javascript
// xhr req
let xhr = new XMLHttpRequest();
xhr.open('POST', url, true);
xhr.setRequestHeader('Content-Type','application/json');
xhr.onload = function(){
  if(xhr.status == 200){
    // send the original form to the database
    }
};
xhr.onerror = function(){
// xyz error handler...
};
xhr.send(objectDataString)
```

#### **upsert** the new data in FHIR and the application database

---
## Example req
```json
{
	"name": "juana",
	"lastname": "nadie",
	"use": "official"
}
```
## Example resp
```json
{
  "fhir_id_practitioner": "f4d497dc-faed-4367-a538-13fff37b0580"
}
```

# Form 4: Editar Perfil (Profesional)
-----
## Information and suggested changes

### Base Form
- URL: [Forma de perfil (Paciente)](https://consultas-panama.web.app/#/patients/settings)
- inputs: 10
- FHIR inputs: 6

| FHIR | Input /Placeholder | id/name     | Required   | objectData |
| ---- | ------------------ | ----------- |-----------|----------- |
|  🔥  |  Nombre            | name        | true      | name       |
|  🔥  |  Apellido          | lastName    | true      | lastname   |
|  🔥  |  Numero de contacto| phone       | true      | name       |
|      |  Nacionalidad (+)     | nationality |true       |         |
|  🔥  |  Género            | gender      | true      | gender       |
|      |  Grupo Sanguíneo   | bloodType   | false     |            |
|  🔥  |  Nacimiento        | dob         | true      | dob       |
|  🔥  |  Cédula o pasaporte | document   | true      | identifier       |
|      |  Cédula o pasaporte(++) | file    | true      |            |

(+) Nationality or country of residence?  
(++) Change placeholder [duplicated]: Cédula o pasaporte ▶ Foto de cédula o pasaporte 

### **Inputs to add**
- new inputs: 16
- hidden inputs: 1
- autocalc inputs: 1
- FHIR inputs: 11

| FHIR | Input /Placeholder | id/name     | Required   | objectData | type |
| ---- | ------------------ | ----------- |-----------|----------- | ------ |
|  🔥  |  idioma            | language     | true      | language  | string |
|  🔥  |  ubicación          | address_line    | true      | address_line   | string |
|  🔥  | ciudad | address_city       | true      | address_city       | string |
|  🔥  | distrito | address_district       | true      | address_district       | string |
|  🔥  | provincia | address_state      | true      | address_state       | string |
|  🔥  | pais | address_country       | true      | address_country       | string |
|  | altura | heigth       | true      |        | string |
|  | peso | weigth       | true      |        | string |
| {autocalc} | imc | bmi       | true      |        | string |
| 🔥 | FHIR ID practitioner | fhir_id_practitioner       | true      | fhir_id_practitioner       | string |
|   (+) | contacto de urgencia | contact_bool       | false      |        | bool |
|  🔥{disp(++)}  |  Nombre            | name_contact        | true      | name_contact       | string
|  🔥 {disp} |  Apellido          | lastName_contact    | true      | lastname_contact   | string
|  🔥 {disp} |  Género            | gender_contact      | true      | gender_contact       | string
|  🔥 {disp} |  Numero de contacto| phone_contact       | true      | phone_contact       | string
|  🔥 {disp} |  email            | email_contact      | true      | email_contact       | string

(+) use a boolean variable (default==False) if change to True then display the **disp** variables. (Trigger a popup, show hidden varaibles, ...)

(++) **disp** = display if contact_bool == True
  
--- 

## Example **XHR** request-response (req-res)

- ### Objective: **Update or Insert patient data**
- ### FHIR url: https://app-ryjgytpm5q-uc.a.run.app/api/consultas/fhir/v1/Patient
- ### method = POST
- ### Headers = 
  - Content-Type: application/json

```javascript
// create the objectDataString
let name = document.getElementById('name').value;
let lastname = document.getElementById('lastName').value;
let phone = document.getElementById('phone').value;
let gender = document.getElementById('gender').value;
let dob = document.getElementById('dob').value;
let personaldocument = document.getElementById('document').value;
let objectData = {
  name : name,
  lastname : lastname,
  phone : phone,
  gender : gender,
  dob : dob,
  personaldocument : personaldocument
};
let objectDataString = JSON.stringify(objectData);
```

```javascript
// xhr req
let xhr = new XMLHttpRequest();
xhr.open('POST', url, true);
xhr.setRequestHeader('Content-Type','application/json');
xhr.onload = function(){
  if(xhr.status == 200){
    // send the original form to the database
    }
};
xhr.onerror = function(){
// xyz error handler...
};
xhr.send(objectDataString)
```

#### **upsert** the new data in FHIR and the application database

---
## Example req
```json
{
	"name": "juana",
	"lastname": "nadie",
	"use": "official"
}
```
## Example resp
```json
{
  "fhir_id_practitioner": "f4d497dc-faed-4367-a538-13fff37b0580"
}
```

# Form 5: Inicia una consulta
-----
## Information and suggested changes

### Base Form (3 steps)
- URL: [Inicia una consulta (Paciente)](https://consultas-panama.web.app/#/patients/home)
---

### **Step 1**

# **Delete the step**
this information is going to be acquired in the form #3
---
---

### **Step 2**

# **Do Nothing**
this step is going to remain equal
---
---
### **Step 3**

- inputs: 2
- FHIR inputs: 0

| FHIR | Input /Placeholder | id/name     | Required   | objectData | type |
| ---- | ------------------ | ----------- |-----------|----------- |----- |
|      |  ¿Cuales son tus síntomas? **(+)**| |   true |            |
|      |  ¿Cuál es el motivo de la consulta?  **(++)** | reasonConsultation    | true      |    | string {in a textarea}


(+) Remove input ➡ ¿Cuales son tus síntomas?  
**(++) kazay triage AI integration**
