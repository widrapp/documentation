# Drives

A drive is a global folder, available on Widr (in this case the `//home` drive) or on a platform that supports drives.

The complete list of drives is :

* `//home` : the logged user's folder in Widr
* `//googleDrive` : the logged user's folder on Google Drive
* `//flickr` : the logged user's folder on Flickr
* `//youtube` : the logged user's folder on Youtube
* `//dropbox` : the logged user's folder on dropbox

Note that using a drive other than Widr requires that the user has authentified and allowed the access to the platform. If not, an AuthorizationRequest will be sent so the user allows access via the Oauth workflow.
