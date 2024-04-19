# Application Security

## Passwords

While the application allows to fully customize the password policies it is recommended to not weaken the default settings too much.

### Structure

The password structure is a highly discussed topic however a password with

* At least one upper case letter
* At least one lower case letter
* At least one numeric character
* At least one special character
* At least 8 characters

is one of the business standards. Longer passwords may be required in the future. Just as a quick info in order to convey the importance of these suggestions, a 8 character password with only upper and lower case characters can be found in less than 6 hours. More and different (e.g. numeric and special) characters exponentially increase the time that is required to brute force a password.

### Aging

Passwords should be changed every 12 months. Enforced password changes are very common and prevent people from using the same passwords over a long period and potentially also for many other applications/services. More important this prevents people from using their standard password which they may use at home in a much less secure environment.

## Permissions

The application allows permission handling by user groups and directly by users. It is strongly recommended to lay out a basic organization schematic and job description for every area. Based on these job descriptions groups should be generated. The permission management through groups is preferred since it's much more verbose and shows a clear structure. While permissions on user basis are in some cases more convenient for quick permission handling they indicate that the actual job function compared to the organization layout is not coherent with the actual tasks that person is performing. Permission handling on user level is strongly advised against and re-structuring groups and creating new groups is much cleaner even if in some cases a group only has one account assigned. Permissions for accounts should also get re-evaluated on a regular basis in order to prevent non-active accounts or accounts whose job description changed to have permissions they no longer need.

## Updates

Updates are very important not only to implement the newest features but also to close potential security vulnerabilities. Depending on your server environment automatic security updates can be activated which then will be executed once a day. Alternatively these updates should be performed manually on a regular basis.

## Modules, Extensions, Themes etc.

Only download software components from the official website never trust any third party services. All software components on the official website get tested and reviewed internally in order to ensure no malicious behavior.

## Which security features does the application implement?

* We use Cross-Site Request Forgery tokens (`CSRF`) for API calls to prevent malicious executions through hidden third-party calls
* We use a strict Content Security Policy (`CSP`) and `nonces` to prevent malicious code infiltration such as Cross-Site Scripting (`XSS`)
* We use BCRYPT/Blowfish hashing with a randomly generated salt for user passwords
* Some selected sensitive data is encrypted in the database and on the file system using the encryption library `libsodium`
* We use backend validation on top of frontend validation
* We almost never sanitize data, data is either valid or gets dismissed
* We extensively test our source code
* We escape user generated text data
* Audit logs tracking changes in the database are first class citizens and are part of every installation by default
* In addition to database audit logs we also generate error logs
* Database query parameters are either simple datatypes (int, bool, float), use quotation for strings or use prepared statements
* File paths are guarded to be within the application path
* We mostly use soft deletes making it possible to restore most of the database data unless overwritten
* We provide extensive user and group permission handling
* Our default server configuration prevents the direct execution of any scripts aside from the main application