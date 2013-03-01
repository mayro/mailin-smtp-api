# Mailin SMTP Library 1.0 #
http://mysmtp.mailin.fr

This library can be used in your PHP script to send the emails using MAILIN-SMTP Services. 

**(c) 2013 Mailin**

<hr>

# How To Install The Mailin SMTP Library #

## Step 1: ##
Download the Mailin SMTP Library “Mailin.php” from 
<code>https://github.com/DTSL/mailin-smtp-api.git</code>

## Step 2: ##
Include the "Mailin.php" file that you have downloaded.
```php
<?php
include 'path/to/mailin-api/Mailin.php';
?>
```

## Step 3: ##
Initialized the Mailin object with your Mailin SMTP credentials. Credentials can be found at <code>http://mysmtp.mailin.fr/parameters</code>
```php
<?php
$mailin = new Mailin('username', 'password');
?>
```

## Step 4: ##
With the help of Mailin object create your email message: 
```php
<?php
$mailin->
  addTo('foo@bar.com', 'Foo')-> 

  addCc('cc@example.com','example cc')-> 

  addBcc('bcc@example.com','example bcc')->

/**
If you need to send the email to more than 1 recipient, you can add them in an array format.
    addTo(
        array(
            'test_one@example.com' => 'example one',
            'test_two@example.com' => 'example two'
   )
    )->

Similarly an array can be created to send multiple carbon copy recipients.
    addCc(
        array(
            'test_one@example.com' => 'example one',
            'test_two@example.com' => 'example two'
	 )
    )->

Again for multiple blind carbon copy recipients we can use array.
    addBcc(
        array(
            'test_one@example.com' => 'example one',
            'test_two@example.com' => 'example two'
	 )
    )->

*/

  setFrom('me@example.com', 'mailin')->
  setReplyTo('reply@example.com','reply name')->
  setSubject('Subject goes here')->
  setText('Hello World!')->
  setHtml('<strong>Hello World!</strong>')->
  addAttachment("path/foo.txt");

/**
   If you wan to attach multiple attachments, you can use an array with the addAttachment function. For example:
addAttachment(array("path/filename1.txt","path/filename2.txt"))

*/
?>
```

## Step 5: ##
Now call the send function using the Mailin object:
```php
<?php

$res = $mailin->send();

/**
The return format is JSON.


Successful email sent message will be returned as:
{'result' => true, 'message' => 'Email sent successfully.'}

In case of unsuccessful email sent, the result will be false with the appropriate failure message.

*/
?>
```
 
## Error Codes ##
Below is a list of common Mailin SMTP error codes and their meanings.

```php
Error Code: 421
Error Description: Unable to send email. Exception message was:  Hourly Quota Exceeded.

Error Code: 902
Error Description: Unable to send email. Exception message was:  Account Terminated.

Error Code: 902
Error Description: Unable to send email. Exception message was:  Attachment data too large. Maximum attachment limit is 3 MB.

Error Code: 0
Error Description: Unable to send email. Exception message was:  No body specified.
```
