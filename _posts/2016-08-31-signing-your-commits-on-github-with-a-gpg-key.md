---
layout: post
title: Signing your commits on GitHub with a GPG key
tags:
- Mozilla
---

Every time [Chuck Harmston][1] commits to GitHub he has that fancy [verified]
tag next to his name and I'm super jealous.

<img src="/blog/public/img/2016-gpg-1.png" title="Screenshot of Chuck's fancy signed commits" />

I've been too lazy to add GPG signing to my Git commits because it seemed like
too much work, but I had some free time this afternoon and [Julien Vehent][2]
convinced me it wasn't that hard, so, here we are.  Writing this post is partly
to encourage everyone to sign their commits, and partly so I can find these
steps again when I forget how to do it in the future.

I already have a gpg key I use for Mozilla things, so I'll start with that.
Check out your current keys (if this list is empty, you'll need to make a key):

```bash
$ gpg --list-keys wclouser@mozilla.com
pub   4096R/4A403229 2013-08-19
uid                  Wil Clouser <wclouser@mozilla.com>
sub   4096R/B438E342 2013-08-19
```

I want to use a new subkey for GitHub signing, so I'll edit my existing master
key and add a new one:

```bash
gpg --edit-key 4A403229
gpg> addkey
<I choose to add a 4096 bit RSA signing-only key which expires in two years>
gpg> save
```

Reviewing my new key:

```bash
$ gpg --list-keys wclouser@mozilla.com
pub   4096R/4A403229 2013-08-19
 uid                  Wil Clouser <wclouser@mozilla.com>
sub   4096R/B438E342 2013-08-19
sub   4096R/04D1111C 2016-08-30 [expires: 2018-08-30]
```

Adding the key to GitHub
------------------------

Telling GitHub about the key is pretty straight forward.  Firstly, get your public key:

```bash
$ gpg --armor --export 04D1111C
-----BEGIN PGP PUBLIC KEY BLOCK-----
  ...
  <many lines of text here>
  ...
-----END PGP PUBLIC KEY BLOCK-----
```

Next, load [https://github.com/settings/keys][3] and click *New GPG Key*.  Then
copy and paste the entire output from the command you ran above into the
textarea on that page and click save.

Signing the commit
------------------

You're going to sign all your commits, right?  So let's just add this thing
globally (bonus note: you can add this, but it only works in git 2.0 and above.
If you have an old version you'll need to add the `-S` flag to your `git
commit` commands):

```bash
$ git config --global commit.gpgsign true
```

If you have more than one key you'll want to specify the key to use:

```bash
$ git config --global user.signingKey 04D1111C
```

You can change all this stuff in `~/.gitconfig` if you'd rather adjust it
directly.  While you're in there, double check that the `user.email` value lines
up with the email address assigned to your key and the email address that GitHub
knows about or else you'll have a mismatch when you try to use it.

Ready to commit something?  Edit your files like normal, and `git commit`.
You'll be prompted for your GPG password (unless you use an agent, and you
should) and everything else should just work like normal.  Github will
recognize the signed commit:

<img src="/blog/public/img/2016-gpg-2.png" title="Screenshot of my signed commit" />


Transferring the key to your laptop
-----------------------------------

Transferring secret keys around always raises some eyebrows, but the reality is
many of us make commits from multiple computers.  As long as you protect the
key in transit, this should be relatively secure.  Firstly, export it into a
couple of files:

```bash
gpg --export 04D1111C > key-pub.asc
gpg --export-secret-keys 04D1111C > key-sec.asc
```

Then securely transfer those files to your laptop (`scp` is a good choice) and run:

```bash
gpg --import key-pub.asc
gpg --import key-sec.asc
```

When you're done, securely delete the .asc files on both computers (I use
`shred` but there are other options).

And that's it.  Signed commits!

[1]: https://twitter.com/chuckharmston
[2]: https://twitter.com/jvehent
[3]: https://github.com/settings/keys
