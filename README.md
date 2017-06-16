# Widr documentation

This page describes the public API of the Widr app.

* [General](#general)
* [Commands](#commands)

## General

Everything in Widr is done via language-like commands. There is only one API endpoint which takes one
unique parameter: the command the be executed. Everything is built around this.

There are a number of commands, but all of them are built around the same semantic structure. 

Each command is made up of 3 main parts:
* `subject` : indicates which controller should be used. This is left blank in general. Values can be: 
"" (blank), "user", "app", "fs". Refer to the "Controller" section for more details.
* `action` : what action should be executed. Default is `get` if not specified.
* `action complement` : what action complement should be executed. Controllers and platforms have default action complements that are specific to each.

### Platforms



### Controllers

### Target and request users

A command will target 2 types of users:
* a `request user`
* a `target user`

The request user is the user launching the command. It is usually implicit and doesn't have to be specified, but it can be forced in some cases.

The target user is the user targeted by the command. This means that the command can be executed against a specified user.

For instance, to send a message to the user `nico` a command would be : `@nico send message 'hello'`

In this example, the user target is a Widr user as no specific platform was specified. But when targeting a specific platform the target user will always apply to the platform.

Therefore, when the command `@nico youtube get likes` is executed, the user `nico` will in that case not be the user `nico` in Widr, but instead be the user named `nico` on YouTube.

### Parameters

## Commands

The following commands are available in Widr. This list is not exhaustive and should be modified with different target/request users and specific parameters.

### Users

### Timelines

### Platforms

#### Tumblr

Get the current user's timeline: `tumblr get timeline`

### Apps
