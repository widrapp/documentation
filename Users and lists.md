# Users and lists

## Users

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

#### Aliases

An alias is a user defined user that encapsulates a list of users, generally on other platforms. This is useful for creating a user that has multiple platforms as a single one and follow his activity easily.

## Lists

A list is a group of users or commands. An user can created as many lists as he likes, so he can then get all of the listed users' timelines, or execute a group of actions. As lists can be used for many things they are also sometimes refered as `groups`, but both are the same.

### The Following list

The `following` list is a system list that cannot be deleted. This list contains all users and commands that should be retrieved when getting the user's timelines (aka using the command `get timelines`). This is in fact a shortcut to using `@list[following] get timeline`.

This list is managed as regular lists, but keep in mind that all that is added to this list will be retrieved in the timelines, and all that is removed will stop showing up in the timelines.
