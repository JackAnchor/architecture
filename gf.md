### Custom validation error message 
If you can't bind to a JS event, you can customize the error by testing for a validation error <div>

```
<script type="text/javascript">
jQuery(document).ready(function(){

    if(jQuery("div.validation_error").length != 0){

        // code that should be run if the validation error exists goes here

    }

});
</script>
```


### Entry Object
The $entry object contains all properties of a particular entry (i.e. date created, client IP, submitted field values, etc…). It is formatted as an associative array with field Ids being the key to that field’s data.

#### Field Values
- FIELD_ID string: The value for all submitted fields can be retrieved by using the Field Id as the key to the $entry array

```
rgar( $entry, '1' );    // returns the value associated with field 1
rgar( $entry, '2.4' );  // returns the value associated with the state input for the address field 2
```

### Form Object
The gform object is the main object in GF, it contains all properties of a particular form (i.e. form title, fields, notification, scheduling, etc…)

- This object is available to most GF hooks and formatted as associative array (i.e. $form[‘title’] retrieves the form title)
- $form['title']                  //returns the form title
- $form['fields'][0]['type'];     //returns the type of the first field of the form

### Field Object
- Contains all settings for a particular field
- Is part of the Form Object and can be manipulated to dynamically change how fields are displayed

```
// returns the label of the first field on the form
$form['fields'][0]->label;
// displays the types of every field in the form
foreach ( $form['fields'] as $field ) {
   echo $field->type . '<br/>';
}
```

#### Field Object Properties 
- allowsPrepopulate (bool): Determines if the field’s value can be pre-populated dynamically. 1 to allow field to be pre-populated, 0 otherwise. Applies to: All fields
- errorMessage (string): Contains the message that is displayed for fields that fail validation. Applies to: All fields except html, section and hidden
- defaultValue (string): Contains the default value for the field. When specified, the field’s value will be populated with the contents of this property when the form is displayed. (Applies to: hidden, text, website, phone, number, date, textarea, email, post_title, post_content, post_excerpt, post_tags, post_custom_field)

### Notifications Object
- An associative array containing the properties for all the email notifications which exist for a form.

### Confirmation Object
- Contains the form confirmation settings such as confirmation text or redirect URL. Also an associative array.

### Form id test
- Apply rules in functions.php to narrow modifications to specific forms
- The following says: "if this form doesn't have an id of 6, let's stop and return the $form object as is"
if($form['id'] != 6) return $form;

