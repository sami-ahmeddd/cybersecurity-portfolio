# SQL Injection — Login Bypass

**Platform:** PortSwigger Web Security Academy  
**Difficulty:** Apprentice  
**Status:** Solved  
**Vulnerability:** SQL Injection (Authentication Bypass)

## Objective

The objective was to exploit an SQL Injection vulnerability in a login form to authenticate as the administrator without knowing the correct password.

## Steps Taken

1. Opened the PortSwigger lab and navigated to the login page.
2. Entered the following payload into the username field:

   `administrator'--`

3. Entered an arbitrary password and submitted the login form.
4. Successfully authenticated as the administrator, and the lab was marked as Solved.

## How the Vulnerability Works

The application incorporated user input into an SQL query without safely separating it from SQL commands.

The single quotation mark (`'`) terminated the username string, while `--` commented out the remaining SQL statement, including the password condition.

This allowed authentication without supplying the correct password.

## Security Impact

An attacker exploiting this vulnerability could potentially bypass authentication and gain unauthorised access to privileged accounts.

## Recommended Mitigation

- Use parameterised SQL queries (prepared statements).
- Avoid directly concatenating user input into SQL statements.
- Apply least-privilege database permissions.
- Monitor suspicious authentication activity.

## Outcome

Successfully completed the PortSwigger SQL Injection login bypass lab.

This exercise demonstrated how insecure SQL query construction can undermine authentication controls.
