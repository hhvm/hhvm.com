---
title: GPG Key Migration
author: fred
layout: post
category: blog
---

As part of modernizing and automating our binary packaging infrastructure, we're rotating the GPG key we use to sign our apt repositories; we will also be signing our source tarballs in the future. We expect to switch the key later this week.

The new key can be installed with:

```
sudo apt-key adv --recv-keys --keyserver hkp://keyserver.ubuntu.com:80 0xB4112585D386EB94
# or...
curl https://dl2.hhvm.com/conf/hhvm.gpg.key | sudo apt-key add
```

The full public key is:

```
-----BEGIN PGP PUBLIC KEY BLOCK-----

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
=3DTP
-----END PGP PUBLIC KEY BLOCK-----
```

Verifying This Post
===================

This key is signed with the previous key; if you have both keys added, you can verify this with:

```
gpg --keyring /etc/apt/trusted.gpg --list-sigs
```

Alternatively, this message is signed by both keys:

```
-----BEGIN PGP SIGNED MESSAGE-----
Hash: SHA256

In November 2017, the HHVM project will be migrating from GPG key 0x1BE7A449, with fingerprint:

36AE F64D 0207 E7EE E352  D487 5A16 E728 1BE7 A449

to GPG key 0xD386EB94, with fingerprint:

0583 41C6 8FC8 DE60 17D7  75A1 B411 2585 D386 EB94
-----BEGIN PGP SIGNATURE-----

iQE+BAEBCAAoFiEENq72TQIH5+7jUtSHWhbnKBvnpEkFAloLG/wKHHB0QGZiLmNv
bQAKCRBaFucoG+ekSe/ZB/4tuH5ZgV1whKPgZIlhi9iDdqTEbANT2nuCaCQuSupU
Dfha1KiYYqnZraw2EBDs0Ve6xrfIdhMKEoF7L2yRsWq/2i490Tf1Ug28MWaLiI23
ZqBpmv9djA9l/xi4CjWWjJaI60kZOL4WUzXrwlU6g6GwcObJweBjrZgA0NMrZwQP
F3Ll0czrxXxUS4ujpv5wSwYVGpJ0zZik8krFzb80Ttkum6icYJuTV8/85VEh8qHo
0557G94w8p5iAUNIdYbG510A0WfKe9s/5CEFCDyYuo3igFYipFWPy5/jK2j7F3VU
4LaWbSfzMMyVI746AMr5LJeFFTRi9YhQg9nnwgay+/yNiQJLBAEBCAA1FiEEBYNB
xo/I3mAX13WhtBElhdOG65QFAloLG/wXHG9wZW5zb3VyY2UraGh2bUBmYi5jb20A
CgkQtBElhdOG65R+ag//SVhZyYiJj35UK8rdKe9y53VdJtDQdD4GGJk/Y52c2pAi
xgs5AdHuTwVb+OzPJMUf/HpBFfNR6Ny86LlFEGqJvnWTJ5gVM6iN+UhPqgFBviqN
Xc6U+Ix3XF0vx6fQSNtK8YSP201psV7d7QKvDTaIEt0pm5JkrCp4VCwwiEAK/R0S
RcFh3cghSzCrdYbmr5lX4I6jkjEw/DyjqGsM9ctldNmqxGC55MfYMrx3tw+PiHTx
eivtw6L0X9z4mRJ0ONs9ULjtamurQbHWyVw8CA/BJ89X/1B9mNyLCxJlT5vrlb6a
ctzbowOFH9IviKFMxIqdRdenDOjIvWdvIf6jloT8ibt5s+ZGixf/0rWYzCTdi+fS
cjbuc7DW4Aru2i6DdQb63mXCjhpmEnkX3gvq1b2TYYQSCm7bd6vSwEQmoTUGOkDZ
Jm7sH97WgiOOBw5EmyBM1Coa5OaOq8qWghE5buzFpONA9gBXTxgJRS8lxswC0K5o
od+AhGTEuecVCEl7lIP/N5ASjrEBkEVKsFaGCX0tSDfgqCZW1JJ+WPD+TllUoEfd
m9jEaNjiApKSOxYg94+1M5Mv+BWh3AoEwz5Jm1xFnVhEocPqhX5Bh53OEfVWoPNX
Po7IgHHd574CLddZrzCslCsnhISm/ARHA2MZBLhfgl71eqz4nqiSwQ4IkUHEMGQ=
=WORw
-----END PGP SIGNATURE-----
```

If you have either, you can verify this message by copying the above into a file, then

```
gpg --keyring /etc/apt/trusted.gpg --verify < file_containing_message_above
```

If you have either existing key, you will see at least 1 "gpg: Good signature" line in the output; unless you have both keys, you will also see "gpg: Can't check signature: public key not found" for whichever key you do not have installed.
