# First Steps

After your first login you will see that everything is rather empty. A good starting point are the general application settings, groups and modules.

## Application Settings

The general application settings can be found in the Admin settings.

Go to:

`Modules (on the side navigation) > Admin > Settings`

On this page you may change the general application settings such as login behavior, server localization, logging etc.

## Modules

Under `Modules` on the side navigation you can see all installed modules. By clicking on them you will get additional module information and module specific settings.

If you want to install additional settings search for specific keywords on the module page and you will receive suggestions based on these keywords. You can then check out the detailed information of these modules in order to further inspect the features the modules provides.

## Groups

Groups are an easy solution to managing multiple users at the same time. After the installation only a handful of groups exist. Feel free to create additional groups based on your requirements.

* `Guest`: Users in this group have no permissions (cannot even login by default)
* `User`: Users in this group have basic read and write permissions
* `Admin`: Users in this group have all permissions

If a user is part of multiple groups (this is often the case in more complex permission handling) the user has the permissions of all groups he is part of. This allows to configure groups very carefully with only the necessary permissions.

### Permissions

Groups (and accounts) can have the following permissions:

* `READ`: The user can read/see certain content
* `CREATE`: The user can create/write certain content
* `MODIFY`: The user can modify/change certain content
* `DELETE`: The user can remove certain content
* `PERM`: The user can change permissions

It's also possible to assign permissions directly to individual users but this is **not** recommended as this makes managing permissions much more difficult.

When you assign the above mentioned permissions to a group you will see that you can also define:

* The `Unit` this permission is for (after the installation you only have one unit but you maybe want to have additional units/sub-organizations later on)
* The `App` this permission is for (after the installation you only have the `Backend` and the `Api` but in the future you may have additional apps, which sometimes even get provided by other modules e.g. `TicketApp`)
* The `Module` this permission is for (e.g. the group only has create/write permissions for a certain module)
* The `Category` is  module specific and can be found in the module help. This can be e.g. news-article in the News module, account in the Admin module etc.
* The `Element` is the specific model/element (e.g. a specific news article). This is represented by the element ID/number.
* The `Component` is the specific component of a element/model (e.g. the title of a news article).

These restrictions show that it is possible to do very fine/granular permissions. It is possible to leave some of the above mentioned restrictions empty to allow a broader permission definition. Examples:

* Everything empty = Group/user has the permissions (e.g. read, create, ...) on everything
* Only define module = Group/user has the permissions (e.g. read, create, ...) on everything in this module
* Only unit and module is defined = Group/user had the permissions(e.g. read, create, ...) on everything in this module but only for the specified unit/sub-organization.

## Accounts

By default only admin users can create new accounts. However it is possible to allow users to register by themselves in the admin module settings. Self-registered users are always part of the `user` group. Make sure the `user` group permissions are designed while keeping that in mind.

If a admin user creates a new account you must decide if the user/account should also be allowed to login/have a profile or if this account is just an internal account.

If the user should be allowed to login/active user you should click on `Create Profile` to also create a profile for the user. Upon doing this the user will receive a registration email in the same way as if he registered by himself. The registration email contains a preliminary password which the user should change.
