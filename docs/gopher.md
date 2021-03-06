---
id: gopher
title: Gopher Support
sidebar_label: Gopher Support
---


KeyDB contains an implementation of the Gopher protocol, as specified in
the [RFC 1436](https://www.ietf.org/rfc/rfc1436.txt).

The Gopher protocol was very popular in the late '90s. It is an alternative 
to the web, and the implementation both server and client side is so simple
that the KeyDB server has just 100 lines of code in order to implement this
support.

What do you do with Gopher nowadays? Well Gopher never *really* died, and
lately there is a movement in order for the Gopher more hierarchical content
composed of just plain text documents to be resurrected. Some want a simpler
internet, others believe that the mainstream internet became too much
controlled, and it's cool to create an alternative space for people that
want a bit of fresh air.

## How it works?

The KeyDB Gopher support uses the inline protocol of KeyDB, and specifically
two kind of inline requests that were anyway illegal: an empty request
or any request that starts with "/" (there are no KeyDB commands starting
with such a slash). Normal RESP2/RESP3 requests are completely out of the
path of the Gopher protocol implementation and are served as usually as well.

If you open a connection to KeyDB when Gopher is enabled and send it
a string like "/foo", if there is a key named "/foo" it is served via the
Gopher protocol.

## SECURITY WARNING

If you plan to put KeyDB on the internet in a publicly accessible address
to server Gopher pages **make sure to set a password** to the instance.
Once a password is set:

1. The Gopher server (when enabled, not by default) will kill serve content via Gopher.
2. However other commands cannot be called before the client will authenticate.

So use the `requirepass` option to protect your instance.

To enable Gopher support use hte following configuration line.

    gopher-enabled yes

Accessing keys that are not strings or do not exit will generate
an error in Gopher protocol format.
