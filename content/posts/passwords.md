---
aliases:
    - "/posts/passwords-suck/"
date: 2022-12-19
description: "This password must contain least eight letters and one capital? MickeyMinniePlutoHueyLouieDeweyDonaldGoofySacramento."
showTableOfContents: true
slug: "stop-reusing-passwords"
tags: ["cybersecurity", "passwords", "KeePass"]
title: "Stop reusing passwords – use this instead!"
type: "post"
---

## Introduction

Nobody likes passwords. They're difficult to remember, and you need a lot of them.

In the past, users were advised to compose passwords of lower and upper case letters, numbers and symbols.

Unsurprisingly, `password` became `P455w0rd!`. This increase in complexity translated well to machines, but not human beings.

The irony is that a password consisting of random words is stronger and more memorable, as depicted in the following comic:

{{< figure src="/images/password-strength.webp" alt="A comic depicting the flaws with the password 'Tr0ub4dor&3', in contrast to a passphrase comprised of four random words: 'correct horse battery staple'." attr="[Password Strength](https://xkcd.com/936) by [Randall Munroe](https://xkcd.com/about/) is licensed under [CC BY-NC 2.5](https://creativecommons.org/licenses/by-nc/2.5/)." >}}

So, if passwords aren't dead yet, what can you do to secure your accounts and devices?

## The solution

Use a password manager. What can a password manager do?

- Store all of your passwords in one place
- Generate strong, unique passwords

    Passwords should never be reused.

- Reduce the number of passwords you need to remember

    One of the exceptions to this rule is the passphrase which locks the password manager. Use [the diceware method](https://diceware.dmuth.org/) to construct a robust passphrase for this purpose.

    The National Cyber Security Centre recommend an overlapping approach, known as [three random words](https://www.ncsc.gov.uk/blog-post/three-random-words-or-thinkrandom-0), which may be the best middle ground for many users.

Now whenever you need to enter a password, you can unlock the password manager and find the password you need.

### Password policies

Some organisations just can't let go of [ineffectual password policies](https://www.ncsc.gov.uk/collection/passwords/updating-your-approach).

If a password must have a minimum or maximum length, capital letters or symbols, you can adjust how the password is generated to conform to these requirements.

In this example, using KeePassXC:

{{< figure src="/images/password-generator.webp" alt="A screenshot of KeePassXC's Password Generator, showing Length and Character Types options." caption="Change the length and permitted characters as required." >}}

Services are increasingly allowing longer passwords without complexity requirements. In these cases, you may prefer to generate passphrases over passwords, to make them easier to type.

## Conclusion

Password managers are a stopgap measure until something better arrives. The more that can be abstracted away from the user, the better.

You should enable multi-factor authentication ([excluding anything which relies on your phone number](https://krebsonsecurity.com/2016/09/the-limits-of-sms-for-2-factor-authentication/)) wherever it's available. In the event of a breach or attack, this will do more to protect you than a password on its own.

Security is a process. If the passwords you need to unlock your devices (and thus access your password manager) are weak, this reduces your operational security.

- Make sure devices are encrypted, and that user accounts have limited privileges
- Generate new passphrases for disk encryption and user passwords, and memorise them

Lastly - don't trust, verify. Do your own research, and establish a threat model that works for you.

### Further reading

#### Password managers

- [What is a password manager?](https://www.malwarebytes.com/what-is-password-manager)
- [Password managers: using browsers and apps to safely store your passwords](https://www.ncsc.gov.uk/collection/top-tips-for-staying-secure-online/password-managers)

#### Three random words

- [The logic behind three random words](https://www.ncsc.gov.uk/blog-post/the-logic-behind-three-random-words)
- [NCSC lifts lid on three random words password logic](https://www.ncsc.gov.uk/news/ncsc-lifts-lid-on-three-random-words-password-logic)
- [Top tips for staying secure online - Three random words](https://www.ncsc.gov.uk/collection/top-tips-for-staying-secure-online/three-random-words)
