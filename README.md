# Zooko
### Truly decentralized, immutable and uncensorable microblogging

# [Why I Quit Handshake](https://github.com/publiusfederalist/why-i-quit-handshake)

Zooko is a working-example, proof-of-concept proving that you can have a decentralized, immutable, and uncensorable microblog platform (like "twitter") in a truly decentralized manner without needing any 3rd party APIs and simply relying on cryptography.

## What is Zooko?

Zooko uses the [Handshake](https://handshake.org) blockchain which allows you to fully own and control a name.  While many use cases exist for Handshake, including [federalist](https://github.com/publiusfederalist/federalist), [DNS](https://www.namecheap.com/support/knowledgebase/article.aspx/10484/2278/namecheap-handshake-tlds/), and [decentralized identity](https://applause.chat/), Handshake is a versatile blockchain that also allows you to build any number of applications on top of it, without the need of smart contracts.

Zooko was named after [Zooko Wilcox O'Hearn](https://en.wikipedia.org/wiki/Zooko_Wilcox-O%27Hearn), one of the few remaining, original, Cypherpunks.

We're still writing code.

![Zooko](https://raw.githubusercontent.com/publiusfederalist/zooko/master/zooko.png)

## How it Works

Handshake is an incredibly secure blockchain.  While many other chains are easy to abuse, Handshake is not one of them.  That being said, there was one outlet that we could take advantage of, and that is the **UPDATE** [covenant](https://github.com/handshake-org/hsd/blob/master/lib/covenants/rules.js) which allows for a DNS resource record with several types, GLUE, NS, among others, and most importantly, TXT.

This is what we take advantage of.

### UPDATE Limitations

You can only call 1 UPDATE per block.  This means that with our implementation, you can only _Zooko_ once per block.  Additionally, TXT has a limit.  We are prepending our TXT with "zooko:" so the limit is 249 characters (255 less 6).  That's **9 more than the leading microblog**!

### Writing a new post

Zooko will copy your DNS resource records over everytime you post, while replacing the last Zooko.  Since TXT records are ignored when a NS record is present, this will not affect anything as we are using on-chain TXT records as opposed to authoritative server served TXT records which are preferred when an NS is present.

## Proof of Concept

This is a quick, and simple, proof of concept.  If someone was to build this into a full blown microblogging platform, a lot more "protocol" would likely need to be developed to integrate different kinds of interactions as well as 'compound interactions' using multiple strings in TXT records, which could allow for more than 1 action per block only limited by resource record max size limit.  One could also hook this into the websocket to watch both the mempool and, as well, for new blocks.  Finally, of course, someone could utilize web technologies and build a beautiful interface for this.

## Why Handshake?

Handshake has been gaining incredible traction, including from institutional bodies like Namecheap, the second biggest DNS registrar on the Internet.  This traction means that Handshake is winning favor with the community and that the Handshake blockchain has secured its space in the cyberworld.  Some questions arise as to whether or not Zooko will bloat the blockchain.  With the UPDATE limitation to one (1) per block, I don't think it will.  However, it was important to use Handshake because doing so anywhere else would cause this to be blockable.  By leveraging Handshake, the entire blockchain would have to be blocked in order to block Zooko.  This is highly unlikely because Handshake is too popular.

This is why I chose to build this on Handshake.

## How to Install
1. Clone
```
git clone https://github.com/publiusfederalist/zooko
```

2. Get prepared
```
cd zooko
npm install hs-client hsd prepend readline stream
```

3. Setup wallet and node keys in the `keys` folder.


4. Now, just try it!

## Commands

#### zpull

Updates the latest posts.
```
./zpull
```

#### zread

Reads the posts.
```
./zread
./zread <name>
./zread <block>
```

#### zpost

Posts a new microblog.
```
./zpost <wallet-id> <name> "<message>"
```
This will prompt you for your password (the password will not echo back to the terminal).

## License and Copyright

(C) 2022 Publius Federalist

All Rights Reserved.


MIT LICENSED



