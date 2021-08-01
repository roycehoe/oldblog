### Description

Note: this is a challenge with intentionally vulnerable systems and applications, in which you are allowed to find vulnerabilities. For more information click [here.](https://portal.hackazon.org/resources/security-policy.html)

This challenge uses backend systems which need to be launched before it can be solved.Click the launch button above to start the backend systems.

[Invite only] - 75 points

Can you get a valid invite code? The flag is the invite code.

[Members only] - 75 points

Can you access the members-only area?

---

### Introduction

Well well well, what do we have here? A website challenge? Time to start playing around to get the invite code.

### Solving the challenge: Part 1

Clicking on `Contact us` brings up the invite code prompt. Thankfully, poking around in the elements yielded this gem:

```javascript
function contactus() {
        var code = prompt("This option is invitation only. Enter your invite code:");

        var verify = (function(code) {
            if (code.length != 12) { return false; }

            var parts = [code.substr(0,3), code.substr(4,4), code.substr(9,3)];
            if (parts.join("-") != code) { return false; }

            if (parts[0] != "UFO") { return false; }
            if (parts[1] != btoa("UFO")) { return false; }
            if (parts[2] != ("UFO".charCodeAt(0) + "UFO".charCodeAt(1) + "UFO".charCodeAt(2))) { return false; }
   
            return true;
        })(code);

        if (verify) {
            alert("Great, please continue the booking process by sending us an email with your invitation code.")        
        } else {
            alert("Wrong invite code.")
        }
    }
```

Basically, this javascript code is telling me how the invite code is validated. Here is what I understand. Whatever the invite code is, it:

- Must be 12 characters long
- Is made of 3 parts joined together whereby, under the [substr method](https://www.w3schools.com/jsref/jsref_substr.asp):
    - Part 1: Contains character index 0-3,
    - Part 2: Contains character index 4-7
    - Part 3: Contains character index 9-11
- Whereby
    - Part 1: Must be `UFO`
    - Part 2: Must be `UFO` [encoded in base64](https://www.w3schools.com/jsref/met_win_btoa.asp)
    - Part 3: Must be the [unicode number](https://www.w3schools.com/jsref/jsref_charcodeat.asp) of the letters in "UFO" added together

---
To solve for these, I got:
- Part 1: UFO
- Part 2: `VUZPCg==` (obtained via base64 on the linux command line)
- Part 3: `234`

And to put this code snippet as cherry on top:

`if (parts.join("-") != code) { return false; }`

which in plain English means, all Parts must be joined with the "-" character, I got the flag!

flag: UFO-VUZP-234

---

### Solving the challenge: Part 2

The challenge is `osint` which [means](http://ctfacademy.net/osint/index.php) that the vulnerability is not the website itself; the vulnerability is through publicly available sources.

Googling the company, I found one of the [CEO](https://www.linkedin.com/in/elliot-talton/?originalSubdomain=nl)s: Elliot Talton

Going to the "about" page, I found the following information about the other CEO, Ben Organa:

> Ben Organa (aka borgana), UFOria CEO

`borgana` is a valid username. And now I have a security question to answer:

> What is your place of birth?

Here's where Elliot Talton's LinkedIn profile came in handy. An innocent [LinkedIn post](https://www.linkedin.com/feed/update/urn:li:activity:6811178494656057344/)  about visiting a [cafe](https://www.google.com/search?q=Lands+Huys+Caf%C3%A9&oq=Lands+Huys+Caf%C3%A9&aqs=chrome.0.69i59.135j0j1&sourceid=chrome&ie=UTF-8) he used to visit in his childhood. And since, Ben Organa shares the same hometown as Eliot, I found Mr Organa's place of birth. Got the flag!

Flag: fataborgana42

---

I'm going to pause here for a moment to acknowledge another joke the creators of this CTF made. The CEO's name is Eliot Talton. [ET](https://en.wikipedia.org/wiki/E.T._the_Extra-Terrestrial).
