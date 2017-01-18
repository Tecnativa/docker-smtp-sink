# Fake SMTP server using [`smtp-sink`][]

[![](https://images.microbadger.com/badges/version/tecnativa/smtp-sink:latest.svg)](https://microbadger.com/images/tecnativa/smtp-sink:latest "Get your own version badge on microbadger.com")
[![](https://images.microbadger.com/badges/image/tecnativa/smtp-sink:latest.svg)](https://microbadger.com/images/tecnativa/smtp-sink:latest "Get your own image badge on microbadger.com")
[![](https://images.microbadger.com/badges/commit/tecnativa/smtp-sink:latest.svg)](https://microbadger.com/images/tecnativa/smtp-sink:latest "Get your own commit badge on microbadger.com")
[![](https://images.microbadger.com/badges/license/tecnativa/smtp-sink.svg)](https://microbadger.com/images/tecnativa/smtp-sink "Get your own license badge on microbadger.com")

[`smtp-sink`]: http://www.postfix.org/smtp-sink.1.html

## What?

This image spins up a fake SMTP server that responds correctly to all SMTP
calls in port `25`, but instead of sending the messages, it spits their
contents out to `STDOUT`.

BTW, we use [Alpine][]. I hope you like that.

  [Alpine]: https://alpinelinux.org/

## Why?

Because you will normally have a [real SMTP relay][] in your docker
environment, but when cloning a production database to your local development
environment, you will most likely want it to **send no messages to the outside
world**, while mocking the underlying app to make it think it sent it
correctly.

[real SMTP relay]: https://hub.docker.com/r/tecnativa/postfix-relay/

## How?

Just run your service in a similar manner to this `docker-compose.yaml` sample:

    version: "2.1"
    services:
        smtp:
            image: tecnativa/smtp-sink
        app:
            build: .
            links:
                - smtp
