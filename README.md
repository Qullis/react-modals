
# React Modals
Easy to use popup modals for react, based on Bootstrap Modal. 

This project started when I was making a reusable form modal for my own website, and suddenly it was it's own project. The form modal is built on react-hook-form and features form validation with Yup. All modals use bootstraps css and js, but the css is scoped so it should not interfere with a project that does not use it. Currently implemented modals are Form, Confirm and Info modals.
Modals are called with code only, no component needed. See further below for a complete documentation for each modal.



## Installation

```bash
  -npm install react-modals-
  //not yet published to npm, todo soon
```
    
## Example usage

```javascript
import useReactModals from "react-modals"
import { myYupSchema } from "./myOptionalYupSchema";

const postFields = [
        { name: 'postTitle', label: 'Post title', type: 'text' },
        { name: 'email', label: 'Email', type: 'email' },
        { name: 'numberOfbirds', label: 'Number of birds sighted', type: 'text' },
        { name: 'descriptionOfBirds', label: 'Short description of birds', type: 'textarea' }
    ];

function App() {
  const { showModal } = useReactModals();

  const submitFunction = async (formData) => {
        //do something with the data
    };

  const handleClick = () => {
    showModal({
            type: 'form',
            modalHeader: 'Add new bird sighting',
            fields: postFields,
            schema: myYupSchema,
            callback: submitFunction,
            theme: 'light',
            buttonText: {
                actionButton: 'Submit',
                closeButton: 'Cancel'
            },
        });
  };

  return (
    <>
      <h1>Bird sightings log</h1>
      <hr />
      <button onClick={handleClick} >Add new</button>
    <>
  )
}
```


## Reference

### useReactModals

```javascript
  import {useReactModals} from "react-modals"
  const { showModal } = useReactModals(options);
```

| Parameter | Type     | Description                |
| :-------- | :------- | :------------------------- |
| `options` | `object` | **Optional**. See below |

#### Options

| Parameter | Type     | Description                       |
| :-------- | :------- | :-------------------------------- |
| `useValidation`      | `boolean` | Validates the modalProperties passed to a modal, useful in developement but should be set to false in production, as to not affect performance. Defaults to true.|

#### Return values

| Value | Description                
| :-------- | :------- | 
| `showModal` | Shows a modal based on the type passed in the modalProperties.  |
| `createStoredModal` | Creates a stored modal that can be used in different components/pages.  |
| `showStoredModal` | Used to show a stored modal based on the id passed.  |

### Modal types and options.
The showModal and createStoredModal functions both takes a modalProperties object. To choose a modal type you need to specify the type by setting type in modalProperties.
Below all types and their properties.

#### Type: form

#### modalProperties

| Parameter | Type     | Description                       |
| :-------- | :------- | :-------------------------------- |
| `type`      | `string` | **Required.** Can be "form", "confirm" or "info"|
| `modalHeader`      | `string` | **Optional.** The header of the modal, can be left out.|
| `fields` | `array` | **Required.** Array of objects. Used to define the form input fields. See further down for reference on fields."|
| `schema`| `yupschema` | **Optional.** Yup validation schema, must match the fields of the form" |
| `callback`      | `function` | **Required.** The function that is run when the form is submitted. The formdata will be passed to this function."|
| `theme`      | `string` | **Optional.** 'light' or 'dark'. Defaults to light."|
| `buttonText`      | `object` | **Required.** { closeButton: 'text for close button', actionButton: 'text for submit button' }|
| `style` | `object` | **Optional.** Object with string values. Used to override the styling See further below"|
| `formDefaultData` | `object` | **Optional.** The default data for the form input fields. The key names of the object should match the field names in the fields objects. See below for reference on "fields". Note that for a stored modal, if you need to pass in default data dynamically, this is done in the "showStoredModal" call. See reference on stored modal for more information.|

...To be expanded...
