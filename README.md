# FCM for Mojo
Push QQ Messages to Android devices according Firebase Cloud Message (FCM) with [Mojo-WebQQ](https://github.com/sjdy521/Mojo-Webqq).
Design for Android 7.0+ specially, full use Android notification feature
(Reply in notification and bundled notifications, etc.)

[简体中文](/README_zh.md)

# Docker
It's very easy to install FFM by Docker. With [kotomei's guilde](https://github.com/kotomei/FCM-for-Mojo), you could finish it in a few minutes.

# Step by Step
## Mojo-Webqq
FFM is depending on Mojo-Webqq, you need install [Mojo-WebQQ](https://github.com/sjdy521/Mojo-Webqq) at first.

## Get Server
You need [install Node.js with npm](https://nodejs.org/en/download/package-manager) and Git at first.
And get server cilent files by Git. Then, install dependent modules runing node:

```Shell
git clone https://github.com/RikkaW/FCM-for-Mojo.git && mv FCM-for-Mojo/server ffm-server
rm -rf FCM-for-Mojo && cd ffm-server/node
npm install && cd ..
node node/index.js
```

Congratulation, HTTP FFM server running now at basic mode now!
But that's not finished yet, we need something to protect your messages.

### HTTP Basic Authorization
Generate a password with openssl:

```Shell
$ openssl passwd
Password:
Verifying - Password:
<MD5>
```

Copy MD5 and create a file with:

```
<username>:<MD5>
```

Edit ```config.json```, finding the line with ```basic_auth```
and del annotation (```/*``` and ```*/```) near that's line:

```js
	"basic_auth": {
		"file": "/path/to/passwd"
	},
```

### HTTPS
Attention, you need **SSL certificates** to set up HTTPS.

Edit ```config.js```, finding the line with "```https```"
and del annotation (```/*``` and ```*/```) near that's line:

```js
	"https": {
			"key": fs.readFileSync("/path/to/privkey.pem"),
			/* Add ca-cert here if you have
			"ca": fs.readFileSync("/path/to/ca-cert.pem"), */
			"cert": fs.readFileSync("/path/to/fullchain-or-server-cert.pem")
		}
```

Run ```node node/index.js```. [download cilent](https://github.com/RikkaW/FCM-for-Mojo/releases) to  finish last configuration!

PS: You can find out more usage about the ```config.conf``` in [wiki](https://github.com/RikkaW/FCM-for-Mojo/wiki/usage-of-config).
