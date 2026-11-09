# PortSwigger Practitioner Lab: Modifying Serialized Data Types

**Platform:** PortSwigger Web Security Academy  
**Difficulty:** Practitioner  
**Vulnerability:** Insecure Deserialization / Authentication Bypass  
**Tools:** Windows PowerShell, curl, Chrome Developer Tools  
**Status:** Solved

## 1. Objective

The objective of this lab was to exploit an insecure PHP serialization-based session mechanism to gain unauthorised access to the administrator account and complete the lab's administrative action.

The application stored user information in a Base64-encoded session cookie, which could be modified to manipulate authentication behaviour.

## 2. Analysing the Session Cookie

I first logged into the application using the provided test account (`wiener`) and inspected the `session` cookie through Chrome Developer Tools.

After Base64 decoding the cookie, I identified the following PHP serialized object:

```php
O:4:"User":2:{
  s:8:"username";s:6:"wiener";
  s:12:"access_token";s:32:"rbxa1gx3bqic6e4bdq7qgmizw6xbcqud";
}
```

The object contained two important properties: `username` and `access_token`.

**Screenshot 1:** Session cookie displayed in Chrome Developer Tools, with the token value redacted.

## 3. Modifying the Serialized Object

I modified the serialized object by changing the username to `administrator` and converting the access token from a string into the integer `0`.

```php
O:4:"User":2:{
  s:8:"username";s:13:"administrator";
  s:12:"access_token";i:0;
}
```

I then encoded the modified object using PowerShell:

```powershell
$payload = 'O:4:"User":2:{s:8:"username";s:13:"administrator";s:12:"access_token";i:0;}'
$cookie = [Convert]::ToBase64String(
    [Text.Encoding]::UTF8.GetBytes($payload)
)
```

This produced a modified session cookie suitable for testing the application's authentication handling.

## 4. Exploiting the Authentication Bypass

I submitted the modified cookie in an HTTP request to the administrator account page using `curl`.

The application returned **HTTP 200 OK**, displaying:

`Your username is: administrator`

The response also contained a link to the administrative panel.

This confirmed that the application accepted the manipulated serialized object and treated the request as authenticated to the administrator account.

**Screenshot 2:** Successful HTTP response showing the administrator username and admin panel link.

I then used the modified session to access the administrative deletion endpoint and completed the lab.

## 5. Impact and Remediation

**Impact:** An attacker able to manipulate the serialized session cookie could potentially impersonate privileged users and perform unauthorised administrative actions.

**Recommended remediation:**

- Avoid trusting client-controlled serialized objects for authentication or authorisation.
- Store session state securely on the server.
- Use cryptographically protected session identifiers.
- Enforce strict type comparisons when validating authentication tokens.
- Validate administrative permissions server-side on every sensitive request.

## 6. Conclusion

This lab demonstrated how insecure deserialization and weak PHP type comparisons can result in authentication bypass.

It strengthened my practical understanding of session handling, PHP serialized objects, HTTP request manipulation and privilege escalation through application logic weaknesses.

**Lab completed successfully in an authorised PortSwigger training environment.**
