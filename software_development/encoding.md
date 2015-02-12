## Encoding

A computer cannot store letters or numbers. The only thing it can store and work with are *bits*. Therefore we use combination of bits to represent different characters. A *encoding scheme* is a set of rules that state how a particular character is represented by a sequence of bits.

<br />
### Theory

<br />
#### Important terms
* **encode**: convert into a coded form. In this case, to encode a character into ASCII means to transform that character into its representation in bits.
* **encoding**: is the set of rules with which to convert a character to a representation in bits.
* **charset**: the set of characters that can be encoded through a particular encoding.
* **code page**: synonymous to encoding. A.k.a "the table".

<br />
#### ASCII
```
0100 0010 -> b
0110 1001 -> i
0111 0100 -> t
0111 0011 -> s
```

The above encoding scheme is ASCII. The ASCII encoding specifies a table translating bytes into human readable letters. Each character is represented by 1 byte.

There are 95 human readable characters in ASCII, including the letters A to Z both in upper and lower case, the numbers 0 through 9 and a handful of other useful characters like punctuation marks.

It also includes 33 values for things like space, tab and so on.

In total there are 128 characters defined in ASCII encoding, a nice round number since it uses all possible combinations of 7 bits.

<br />
#### Problems with ASCII
In ASCII there is no representation for characters like ä ö å á é í... so you can't use them. ASCII worked for representing English words, but as soon as you wanted to write something in Swedish, Spanish or French ASCII was not enough. Not to mention languages like Chinese or Japanese which have tens of thousands of characters. Good luck representing them with 8 bits.

The world ended up with a wealth of encoding schemes.

<br />
#### Unicode
Somebody had enough of the mess and set out to create one encoding standard to unify all encoding standards. This standard is Unicode.

Unicode's character set includes ALL human language's written symbols. It includes the tens of thousands Chinese characters, math symbols, as well as characters of dead languages. It basically defines a ginormous table of 1,114,112 code points.

So, how many bits does Unicode use to encode all these characters? None. Because Unicode is not an encoding.

Unicode first and foremost defines a table of code points for characters. A *code point* is a unique ID (integer) associated with a character.

For example, the code point for the greek alpha α char is 945. In hexadecimal it's “3b1”. In the standard Unicode notation it is written as “U+03B1”.

How these code points are actually encoded into bits is a different topic. To represent 1,114,112 different values, two bytes aren't enough. Three bytes are, but three bytes are often awkward to work with, so four bytes would be the comfortable minimum. But, unless you're actually using Chinese or some of the other characters with big numbers that take a lot of bits to encode, you're never going to use a huge chunk of those four bytes. If the letter "A" was always encoded to `00000000 00000000 00000000 01000001`, "B" always to `00000000 00000000 00000000 01000010` and so on, any document would bloat to four times the necessary size.

To optimize this, there are several ways to encode Unicode code points into bits.

<br />
#### UTF-32
UTF-32 is such an encoding that encodes all Unicode code points using 32 bits. That is, four bytes per character. It's very simple, but often wastes a lot of space so it is not used much.

<br />
#### UTF-8
UTF-8 is a variable-length encoding. If a character can be represented using a single byte (because its code point is a very small number), UTF-8 will encode it with a single byte. If it requires two bytes, it will use two bytes and so on. It has elaborate ways to use the highest bits in a byte to signal how many bytes a character consists of. This can save space, but may also waste space if these signal bits need to be used often.

All characters available in the ASCII encoding only take up a single byte in UTF-8 and they're the exact same bytes as are used in ASCII. In other words, ASCII maps 1:1 unto UTF-8. Any character not in ASCII takes up two or more bytes in UTF-8.

UTF-8 is suitable for texts that are mostly Latin alphabet letters. For example, English, Spanish, French, and most web technology such as HTML, CSS, JavaScript. Most Linux's files are in UTF-8 by default

<br />
#### UTF-16
UTF-16 is another variable-length encoding system from Unicode. With UTF-16, every char is encoded into at least 2 bytes, and commonly used characters in Unicode are exactly 2 bytes. For Asian languages containing lots of Chinese characters, such as Chinese ＆ Japanese, UTF-16 creates smaller file size.

<br />
#### ISO 8859-1
Also called Latin1. It is a single-byte encoding that can represent the first 256 Unicode characters.

Comparison against UTF-8:
* UTF-8 can is variable-length encoding. Latin1 is single-byte.
* UTF-8 can represent any Unicode character. Latin1 can only represent the first 256 Unicode characters.
* Both encode ASCII characters (0-127) the same way.
* Characters 128-255 are represented differently by UTF-8 and Latin1. In UTF-8 these characters are 2-byte sequences whereas in Latin1 they are 1 byte.

<br />
### Utils

<br />

#### Decoding
When an editor opens a file, it needs to know the encoding scheme used, in order to decode the binary stream and map it to fonts to display the original characters properly. In general, the info about the encoding system used for a file is not bundled with the file.

When opening a file, applications may try to guess the encoding system used by some heuristics. If the application assumed the wrong encoding, typically the result is gibberish. The document is not broken, you simply need to tell your app what encoding scheme to use.

<br />
#### Resources

http://kunststube.net/encoding/<br />
http://www.joelonsoftware.com/articles/Unicode.html