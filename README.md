# hyperpad

> A peer-to-peer collaborative text editor for humans and communities.

## What is it?

Hyperpad is a free, open source, peer-to-peer text editor for people and their
communities. Authors control who gets access, and data is hosted by the peers
who are interested in it.

## Current Status

I've paused work on the web client in favour of building out an Electron-based
native client, [hyperpad-desktop](https://github.com/noffle/hyperpad-desktop).
This lets me dodge some difficult problems around web tech (indexed-db
performance; webrtc) and focus on making the core
[hyper-string](https://github.com/noffle/hyper-string) primitive robust and
durable.

## Why another collaborative editor?

Some of the most popular collaborative document editors today include [Google
Docs](https://www.google.com/docs/about/) and [Etherpad](http://etherpad.org/).

Google Docs gets the fundamental piece right: real-time text editing. However,
all of your data is stored by and readable by Google, Inc. It is closed source
proprietary software.

Etherpad takes this a step further in multiple directions: it is [open
source](https://github.com/ether/etherpad-lite), and can be deployed by anyone
on any server. This lets any individual or group run etherpad and keep ownership
and privacy to their data.

Etherpad is most of the way there, but Hyperpad goes the rest of the way in two
crucial aspects:

### 1. No servers required

In peer-to-peer networks, all users are equal.

Nobody needs the monetary resources and technical know-how to run a server.

Unlike centralized services, you own each pad you create. Turn on encryption,
and your data becomes unreadable to anyone but those you grant access to. There
are no service providers to go out of business and lose your data.

Everything is client-side HTML and Javascript: you can just save the Hyperpad
website and run it locally on your computer, and it will function just fine!

### 2. Works great offline

Not everybody in the world is online. Among those who are, many do not have
consistent, broadband connections. People-respecting software must work
excellently offline; no exceptions.

Forgetting this is the *The Silicon Valley Privilege* (TODO: link to article).

Hyperpad uses an *eventually consistent* data structure called
[hyperlog](https://github.com/mafintosh/hyperlog), which operates happily
offline and will sync with other users whenever a network connection is
available.

## How does it work?

Hyperpad relies on the browser itself for storing documents, and powerful
peer-to-peer primitives like
[WebRTC](https://developer.mozilla.org/en-US/docs/Web/Guide/API/WebRTC) and
[hyperlog](https://github.com/mafintosh/hyperlog) to organize and transfer
documents to those with access.

The act of having a document open in your browser immediately lets a user act
as a host for that document's data, sharing it in real-time with others with
others. In the case that a user is offline, they can still freely make edits
locally, which will propagate to others storing the document when they
re-establish a network connection.

Hyperpad is built in a modular fashion atop a set of do-one-thing-well modules:

- [hyper-textarea](https://github.com/noffle/hyper-textarea): back a textarea
  with a hyper-string for conflict-free p2p replication
- [hyper-string](https://github.com/noffle/hyper-string): a conflict-free p2p
  string data structure
- [textarea-op-stream](https://github.com/noffle/textarea-op-stream): readable
  stream of a textarea's inserts and deletes
- lots of great modules from [mafintosh](https://github.com/mafintosh/):
  [hyperlog](https://github.com/mafintosh/hyperlog),
  [signalhub](https://github.com/mafintosh/signalhub), and others!

## Coming Soon(tm)

- [hyperpad-desktop](https://github.com/noffle/hyperpad-desktop)
- ~Faster operations (batching in the `hyper-string` layer)~
- Encryption (with separate read/write privileges)
- Secure app delivery (maybe [hyperboot](https://github.com/substack/hyperboot))

## License

[ISC](https://en.wikipedia.org/wiki/ISC_license)
