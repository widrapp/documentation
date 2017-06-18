# Widr documentation

This page describes the public API of the Widr app.

* [General](#general)
* [Commands](#commands)
* [Drives](#drives)
* [Platforms](#platforms)

## General

Everything in Widr is done via language-like commands. There is only one API endpoint which takes one
unique parameter: the command the be executed. Everything is built around this.

There are a number of commands, but all of them are built around the same semantic structure. 

Each command is made up of 3 main parts:
* `subject` : indicates which controller should be used. This is left blank in general. Values can be: 
"" (blank), "user", "app", "fs". Refer to the "Controller" section for more details.
* `action` : what action should be executed. Default is `get` if not specified.
* `action complement` : what action complement should be executed. Controllers and platforms have default action complements that are specific to each.

### Subjects & controllers

The subject indicates which controller should be used. A controller is a grouping of actions that are all working towards the same goal.

For instance, the `fs` controller groups all actions that interact with the filesystem, such as creating/reading/writing/deleting files or folders.

If an action is general it will in most cast use the general controller, which doesn't have to be specified.

In version 1.0 the controller has to be specified if different than general, so you need to know which one you are targeting when creating the command. That is likely to change in the future so commands are more human.

The following controllers are available:
* `fs` : manages all filesystem related actions
* `app` : manages external apps, such as the weather app
* `user` : manages all user related actions

### Platforms

In addition to controllers commands can be executed against a specific platform. Those are pre-defined in Widr and support a number of operations based on what is possible via their public APIs. See the list of platform commands for a detailed list of available platforms.

A platform can be specified using `@platform[platform_name]`, or can be abbreviated to only the platform name as the subject of the command.

For instance, both examples are valid:
* `@platform[youtube] get likes`
* `youtube get likes`

### Target and request users

A command will target 2 types of users:
* a `request user`
* a `target user`

The request user is the user launching the command. It is usually implicit and doesn't have to be specified, but it can be forced in some cases.

The target user is the user targeted by the command. This means that the command can be executed against a specified user.

For instance, to send a message to the user `nico` a command would be : `@nico send message 'hello'`

In this example, the user target is a Widr user as no specific platform was specified. But when targeting a specific platform the target user will always apply to the platform.

Therefore, when the command `@nico youtube get likes` is executed, the user `nico` will in that case not be the user `nico` in Widr, but instead be the user named `nico` on YouTube.

Request and target users can be specified at the same time, if this case both will be lined up as `@request_user@target_user do something`

### Parameters

Parameters can be added to a command after the action and/or action complement.

This is done in 2 ways, but the idea is to always set a value to a key:
* Using the `=` operator. Ex: `myvariable = value`
* Using the `set / is` keywords. Ex: `set myvariable is value`

## Commands

The following commands are available in Widr. This list is not exhaustive and should be adapted with different target/request users and specific parameters.

### Pipes

Using pipes in command is still in testing and will be documented later, but using pipes between 2 commands to share data is already possible when the command receiving the other command's data supports it.

The format for using pipes is :

`file //home/my_file.txt || echo 'inject this data'`

Note that not all commands support pipes and using pipes on non pipable commands could produce strange results in the current version.

### FS controller

Side note: All user files are listed in the `//home` folder. This folder acts as a drive (see the Drives section below for more details), and can therefore be directly refered as `//home`, without specifying the fs controller. In reality, this is then converted in the background as `fs folder //home`. But writing `//home` is just faster and more convenient.

* Read a given folder : `folder //home/my_folder` or `fs folder //home/my_folder`
* Read a file : `file //home/my_file.txt` or `fs file //home/my_file.txt`
* Create an empty file : `fs touch //home/new_file.txt`
* Delete a file : `fs delete //home/my_file.txt`

## Drives

Drives can be accessed in 2 ways:
* Using the drive shortcut `//drive_name`. Ex: `//home`, `//googleDrive`
* Using the full command `get drive name is 'drive_name'`. Ex: `get drive name is 'googleDrive'`

For more information about drivesrefer to the page [Drives](Drives.md)

#### Accessing folders and files in drives

Accessing folders and files in drives is done by refering the drive and the path to be accessed:

* `//home/my_folder/my_file.txt`
* `//googleDrive/my_file_id`

Note that in some cases the platform will use IDs instead of understandable paths. This is due to how the platform handles files and cannot be changed. This makes browsing the files via the command lines a bit more difficult but is transparent while using the UI.

#### Writing to a drive

Writing to a drive can be used via a pipe to write to a folder or to a file.

* `//home/my_folder || file //home/my_file.txt`
* `//googleDrive/my_file_id || echo 'some text'`

### User controller

The user controller manages all user related actions. Those include retrieving the list of Widr users, creating/retrieving aliases, creating/retriving lists and managing the logged user's profile.

For more information about users and lists refer to the page [Users and lists](Users%20and%20lists.md)

### Combining mutliple users with the '+' operator

It is possible to apply a single command on 2+ different users by combining the target users using the + operator.

Ex: `@user1+@user2 get likes` : this command will be transformed to `@user1 get likes && @user2 get likes` so the command `get likes` will be applied to both users.

#### Lists

A list is specified in a command using the `@list[list_name]` target.

A list will in fact be a combination of users or commands, meaning that all elements of this list will be taken each and the specified command will be executed against each item.

Examples of list operations:
* `@list[my_list] get timeline` : take each `person` element from the list and apply the `get timelines` command.
* `@list[my_list] #fun` : take each `person` element from the list and apply the special command `#fun` (= get tagged tag is 'fun') to each item.
* `@list[my_list]` : take each `person` element from the list only and execute it.


### App controller

To be completed.

## Platforms

When targeting a specific platform other than Widr the name of the platform has to be specified either as the subject or by using the platform accessor:
* As subject: youtube get likes
* Using the platform accessor : @platform[youtube] get likes

Both will produce exactly the same result.

### Tumblr

* Get the current user's timeline: `tumblr get timeline`
* Get the current user's likes: `tumblr get likes`
* Get the current user's profile: `tumblr get profile`
* Get the current user's items tagged with #fun: `tumblr #fun`

Note that all of these commands can be transposed to another Tumblr user by targeting it as @target_user:
* `@user_x tumblr #fun` : Will get the items tagged with #fun from the Tumblr user `user_x`

Documentation to be completed for each available platform.
