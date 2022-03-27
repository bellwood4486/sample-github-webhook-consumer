# GitHub Webhook Consumer Sample of Go

This is a sample of a consumer service to receive events from GitHub.

The sample uses [localhost.run](https://localhost.run/). This is because the local server receives events from GitHub.

## How To Run

Run the server with the following command. The server runs on `localhost:8080`.

```shell
❯ make run
go run main.go
```

Expose the server with the following command.  
The last line shows FQDN of the published server. In this case it is 'https://ed**************.lhrtunnel.link'.

```shell
❯ make expose
ssh -R 80:localhost:8080 localhost.run

===============================================================================
Welcome to localhost.run!

Follow your favourite reverse tunnel at [https://twitter.com/localhost_run].

**You need a SSH key to access this service.**
If you get a permission denied follow Gitlab's most excellent howto:
https://docs.gitlab.com/ee/ssh/
*Only rsa and ed25519 keys are supported*

To set up and manage custom domains go to https://admin.localhost.run/

More details on custom domains (and how to enable subdomains of your custom
domain) at https://localhost.run/docs/custom-domains

To explore using localhost.run visit the documentation site:
https://localhost.run/docs/

===============================================================================


** your connection id is ********-****-****-****-119f191cb35d, please mention it if you send me a message about an issue. **

ed**************.lhrtunnel.link tunneled with tls termination, https://ed**************.lhrtunnel.link
```
(The following output is partially masked.)

Open your repository and locate Settings > Webhooks.  
Set up as follows.
(It is recommended to check single event(ex. `Stars`) at first, as it is easier to test.)

<img width="1164" alt="image" src="https://user-images.githubusercontent.com/2452581/160272740-9983aff3-c2c9-4ba1-8378-71e05d1064d6.png">

Try adding and removing Star. If the configuration is successful, you will see the following output on the server's console.

```text
called from github
> Accept: */*
> Connection: close
> Content-Length: 6953
> Content-Type: application/json
> Forwarded: for=140.82.***.***;proto=https;host=ed**************.lhrtunnel.link
> User-Agent: GitHub-Hookshot/f0*****
> X-Forwarded-For: 140.82.***.***
> X-Forwarded-Host: ed**************.lhrtunnel.link
> X-Forwarded-Proto: https
> X-Github-Delivery: e9d1d150-ad9f-11ec-8076-************
> X-Github-Event: star
> X-Github-Hook-Id: 35013****
> X-Github-Hook-Installation-Target-Id: 47456****
> X-Github-Hook-Installation-Target-Type: repository
> X-Hub-Signature: sha1=967febcd9ff1bf26f4fb5d0b6669f85882a56953
> X-Hub-Signature-256: sha256=8b01caaa7f789fb3bb958b0b095fac1cc0e6846b45ef05a58a54376833108644
sha256: true
sha1: true
```
(The following output is partially masked.)

`sha256: true` means that the SHA256 signature verification was successful.
(`sha1: true` means the same thing.)

## References

* [Using SSH and localhost.run to test GitHub webhooks locally](https://andrewlock.net/using-ssh-and-localhost-run-to-test-github-webhooks-locally/)
* [About webhooks - GitHub Docs](https://docs.github.com/en/developers/webhooks-and-events/webhooks/about-webhooks)
