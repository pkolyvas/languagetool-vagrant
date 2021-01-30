# LanguageTool Vagrant Box

This is a simple vagrantfile that will download and configure a local version of [LanguageTool](https://languagetool.org/). 

This install closely follows the [instructions](https://dev.languagetool.org/http-server) available for offline development with LanguageTool.

It will also [download and install the ngrams](https://dev.languagetool.org/finding-errors-using-n-gram-data) for the English Language. However the English-language ngram data is, as of this update, over 8GB in size. Fair warning.

If you do wish to skip the ngram data, you'll need to comment out the `curl` request used to download it and remove the `--languageModel` option from the command which starts up the `LanguagTool` server. Reviewing their installation instructions (linked above) would be valuable at that point.

Currently the `Vagrantfile` uses `curl` to download files instead of `wget` because the LanguageTool server will throttle multiple requests from the same IP - an issue I faced while trying to get things right. Totally reasonable on their part. 

## Using this box
- Ensure you have vagrant and virtualbox installed.
- `vagrant up`
- Access the server at http://localhost:8082

## Note

Letsencrypt and nginx are installed as part of the vagrant file should you want to setup an HTTPS reverse proxy (recommended).

You're on your own for configuring these but here's what I do:
- Run `certbot certonly --dns-route53 -d laguagetool.example.com`. I like this method because I'll never expose the LanguageTool box to the internet, but I can still get an HTTPS certificate for use within the network I control. 
- Edit the default `nginx` configuration in `/etc/nginx/sites-available/default` to include a name for your host and configure the proxy parameters and SSL/TLS options.
