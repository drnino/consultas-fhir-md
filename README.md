# Form 1: Registro de pacientes 
-----
## Information and suggested changes
- URL: [Forma de registro (Paciente)](https://consultas-panama.web.app/#/register)
- inputs: 4
- FHIR inputs: 2

| FHIR | Input /Placeholder | id/name     | Require   | objectData |
| ---- | ------------------ | ----------- |-----------|----------- |
|  🔥  |  Nombre            | name        | true      | name       |
|  🔥  |  Apellido          | lastName    | true      | lastname   |
|      |  Email             | email       | true      |            |
|      |  Password(*)       | password    |true       |            |

(*) Change placeholder: Password ▶ Contraseña 

---

## Example **XHR** request-response (req-res)

- ### Objective: **Create a new patient**
- ### FHIR url: https://app-ryjgytpm5q-uc.a.run.app/api/consultas/fhir/v1/Patient
- ### method = POST
- ### Headers = 
  - Content-Type: application/json

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
    // with new input fhir_id_pacient
    }
};
xhr.onerror = function(){
// xyz error handler...
};
xhr.send(objectDataString)
```

#### after recive the response
#### use the **responseText** as a value for new key:value pair 
#### [ fhir_id_pacient : xhr.responseText ]

---
## Example req
```json
{
	"name": "juan",
	"lastname": "nadie",
	"use": "official"
}
```
## Example resp
```json
{
  "fhir_id_patient": "450db9bc-0613-4ebb-aab5-595797290fcd"
}
```
