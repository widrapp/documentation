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

### Targeted and requested users

### Controllers

### Parameters

## Commands

The following commands are available in Widr. This list is not exhaustive and should be modified with different target/request users and specific parameters.

### Users

### Timelines

### Platforms

#### Tumblr

Get the current user's timeline: `tumblr get timeline`

### Apps