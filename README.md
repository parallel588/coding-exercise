# TSG Coding Exercise

## Introduction

We'd prefer the solution to be written in Elixir, but will also accept Ruby,
node.js.

The exercise should take an estimated ~30-60 minutes to complete.

Please send your solution via email (devs@tsgglobal.com). Along with the code, please include a written introduction to your solution, that explains the design and implementation decisions you made and why.

## Problem to Solve

In this exercise, you will be writing a webhook based chatbot to integrate with
a test server we've provided for you #{API DOCS}.

Your bot is supposed to be able to receive messages via the webhook, and respond
to them by doing a POST back to the API.

The bot itself should be a currency exchange bot, and internally use the
http://fixer.io/ API (simple & free, if using node.js, you can use their
money.js library).

1. It should parse messages in the format of "N X in Y", i.e. "10.5 USD in EUR",
"5.75 GBP in HKD" and respond with the converted amount ("8.9 EUR").

2. It should handle specifying the currency in both uppercase and lowercase,
   i.e. "10.5 USD to EUR" as well as "2 eur in usd".

3. It should handle multiple currencies, i.e."N X in Y, Z", "4 USD in EUR, JPY".
   We expect you to return multiple messages, one per currency.

Bonus points if you have the time to write tests for the webhook.

## Test Server

#{URL} #{API DOCS}

To use the test server, enter your webhook URL, and press start. A chat session
will open, which you can now use to interact with your webhook.

If you're testing your code locally, we recommend you use ![ngrok](https://ngrok.com/) for exposing your local endpoint.

```
$ ngrok http <local-port>

Session Status                online
Version                       2.2.8
Region                        United States (us)
Web Interface                 http://127.0.0.1:4040
Forwarding                    http://aaaaaaaa.ngrok.io -> localhost:720
Forwarding                    https://aaaaaaaa.ngrok.io -> localhost:720

Connections                   ttl     opn     rt1     rt5     p50     p90
                              0       0       0.00    0.00    0.00    0.00
```

Now you can use one of those ngrok.io URLs as your webhook URL.
