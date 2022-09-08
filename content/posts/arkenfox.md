---
date: 2022-09-07
description: "Curb the Chromium monopoly"
showTableOfContents: true
slug: "supercharge-the-privacy-and-security-of-desktop-firefox"
tags: ["cybersecurity", "privacy", "firefox", "chromium"]
title: "Supercharge the privacy and security of desktop Firefox"
type: "post"
weight: 16
---

# Introduction

The Arkenfox user.js project configures desktop Firefox to use more of the security and privacy features already built into the browser[^what-is-arkenfox-user.js].

> arkenfox user.js ... aims to provide as much privacy and enhanced security as possible, and to reduce tracking and fingerprinting as much as possible - while minimizing any loss of functionality and breakage (but it will happen)[^what-is-arkenfox-user.js].

In my experience, modern and well-maintained websites work without issue. [Applying the base `user.js`](#applying-the-librewolf-configuration) will suit most use cases.

If a site doesn't function correctly, disabling Enhanced Tracking Protection can help. Be aware that doing this means no tracker blocking or first party isolation[^what-enhanced-tracking-protection-blocks].

[^what-is-arkenfox-user.js]: Thorin-Oakenpants. ‘Arkenfox/User.Js’. JavaScript. 2017. Reprint, arkenfox, 31 August 2022. https://github.com/arkenfox/user.js.
[^what-enhanced-tracking-protection-blocks]: AliceWyman, Chris Ilias, Michele Rodaro, Mozinet, Joni, Marcelo Ghelman, Lamont Gardenhire, et al. ‘Enhanced Tracking Protection in Firefox for Desktop’. Mozilla Support, 2022. https://support.mozilla.org/en-US/kb/enhanced-tracking-protection-firefox-desktop.

# Overrides
 
`user.js` can be modified with a `user-overrides.js` file[^what-are-user.js-overrides].

You can make your own by reading [the Wiki](https://github.com/arkenfox/user.js/wiki), referencing [the `user.js`](https://github.com/arkenfox/user.js/blob/master/user.js), and [adding recipes](https://github.com/arkenfox/user.js/issues/1080) to enable features such as DRM and Session Restore[^arkenfox-recipes].

[^arkenfox-recipes]: Thorin-Oakenpants. ‘Sticky: Override Recipes · Issue #1080 · Arkenfox/User.Js’. GitHub, 3 June 2022. https://github.com/arkenfox/user.js/issues/1080.

As an example, [my `user-overrides.js` file](https://codeberg.org/jamesericdavidson/user-overrides.js/src/branch/main/user-overrides.js) toggles the following preferences[^my-user-overrides.js]:

[^what-are-user.js-overrides]: Thorin-Oakenpants. ‘3.1 Overrides · Arkenfox/User.Js Wiki’, 19 March 2022. https://github.com/arkenfox/user.js/wiki/3.1-Overrides.
[^my-user-overrides.js]: Davidson, James. ‘User-Overrides.Js’. JavaScript, 31 August 2022. https://codeberg.org/jamesericdavidson/user-overrides.js.

| Disabled | Enabled | Changed |
| -------- | ------- | ------- |
| Google Safe Browsing | Address bar | Increase window size |
| DNS-over-HTTPS | Limit font visibility |
| Media (video and audio) autoplay | Save downloads to another directory |
| Colour visited links |
| Memory cache |
| Ask to save passwords |
| Certificate caching |
| Undo closed tabs |
| "Open with" download prompt |
| What's New |
| Pocket |
| Firefox Accounts |

These changes are made to reduce privacy exposure, decrease caching, remove annoyances, and add quality of life.

But what is my rationale for not wanting to use some of this functionality?

### Google Safe Browsing

Foremost, Safe Browsing is disabled to reduce exposure to Google, and diminish dependence on their services.

[I want to expand this badness enumeration point later on, insisting that we should insist on "foundational security" instead. Requires more research.]: #

Next, as an objection to badness enumeration. A cybersecurity faux pas, whereby 'all the bad things that we know about' are itemised[^enumerating-badness].

Finally – from a privacy perspective – the design of Safe Browsing is flawed. Purported to work from a local list[^how-safe-browsing-works], the remote database is sometimes queried to avoid hash collision. Rescorla postulates that hashes for more popular websites – and hashes for different pages on the same website – could be used to infer which websites the user is visiting[^safe-browsing-critique].

[^enumerating-badness]: Ranum, Marcus J. ‘The Six Dumbest Ideas in Computer Security’. Marcus J. Ranum, 1 September 2005. https://www.ranum.com/security/computer_security/editorials/dumb/.
[^how-safe-browsing-works]: Marier, François. ‘How Safe Browsing Works in Firefox’. Feeding the Cloud, 8 November 2022. https://feeding.cloud.geek.nz/posts/how-safe-browsing-works-in-firefox/.
[^safe-browsing-critique]: Rescorla, Eric. ‘Can We Make Safe Browsing Safer?’ Educated Guesswork, 16 August 2022. https://educatedguesswork.org/posts/safe-browsing-privacy/.

### DNS-over-HTTPS

DNS-over-HTTPS (DoH) bypasses enterprise policies and controls – namely filtering and monitoring – which should concern organisations[^doh-problems]:

- Command and control (C&C or C2) malware can use DoH[^doh-c2-proof-of-concept] to 'communicate ... unimpeded by local network monitoring solutions'
- DNS-based firewalls and blocklists are sidestepped when using DoH

As a consequence of performing DNS at the application layer, services at the network layer – chiefly the DNS root servers and ISP DNS servers – are ignored, undoing the traditional trust model[^doh-trust-model_1] [^doh-trust-model_2].

[^doh-c2-proof-of-concept]: Garmiza, Masha. ‘DNS over HTTPS as a Covert Command and Control Channel’. Inside Out Security, 30 June 2022. https://www.varonis.com/blog/dns-over-https-as-a-covert-command-and-control-channel.
[^doh-trust-model_1]: Hoffmann, Stacie. ‘Understanding DNS Over HTTPS - DoH’. Internet Governance & Cyber Security, 19 August 2019. https://oxil.uk/blog/understanding-dns-over-https-doh/.
[^doh-trust-model_2]: EfficientIP. ‘Why Using DoH Is Questionable’, 2 February 2021. https://www.efficientip.com/why-using-doh-is-questionable/.

#### Censorship

DoH does little to prevent tracking or circumvent censorship[^doh-problems] [^encrypted-dns-threat-model].

>  It is instrumental to see DoH as a 'very partial VPN' that only encrypts DNS packets, but leaves all other packets unmodified ...[^doh-problems]

DoH should only be used to overcome DNS redirects and 'basic' blocking – when there are no consequences to doing so – making it unsuitable for most threat models[^encrypted-dns-threat-model].

For citizens of Mainland China, TLS 1.3 and ESNI traffic are blocked outright[^china-blocks-tls] – including DoH[^china-blocks-doh] – making it a non-starter.

> This posed a problem for China, prompting them to make a change… to their Great Firewall to block all TLS 1.3 and ESNI traffic, effectively stopping people in China from using DoH to hide their DNS lookups[^china-blocks-doh].

If your goal is to defeat surveillance and censorship, use the Tor Browser Bundle[^tor-vs-vpn] [^encrypted-dns-threat-model].

[^china-blocks-doh]: Leyden, John. ‘Cat and Mouse: Privacy Advocates Fight Back after China Tightens Surveillance Controls’. The Daily Swig | Cybersecurity news and views, 1 July 2021. https://portswigger.net/daily-swig/cat-and-mouse-privacy-advocates-fight-back-after-china-tightens-surveillance-controls.
[^china-blocks-tls]: Cimpanu, Catalin. ‘China Is Now Blocking All Encrypted HTTPS Traffic That Uses TLS 1.3 and ESNI’. ZDNET, 8 August 2020. https://www.zdnet.com/article/china-is-now-blocking-all-encrypted-https-traffic-using-tls-1-3-and-esni/.
[^doh-problems]: Cimpanu, Catalin. ‘DNS-over-HTTPS Causes More Problems than It Solves, Experts Say’. ZDNET, 6 October 2019. https://www.zdnet.com/article/dns-over-https-causes-more-problems-than-it-solves-experts-say/.
[^encrypted-dns-threat-model]: jonaharagon and d4rklynk. ‘Introduction to DNS - Privacy Guides’. Privacy Guides, 7 August 2022. https://www.privacyguides.org/basics/dns-overview/.
[^tor-vs-vpn]: Tor vs VPN | Which One Should You Use for Privacy, Anonymity and Security, 2020. https://www.youtube.com/watch?v=6ohvf03NiIA.

# Doesn't LibreWolf already do this?

LibreWolf has endemic flaws which undermine security:

- No automatic updates, and inconsistent packaging[^privacyguides-discussions-add-librewolf]
- New versions are released multiple days after upstream Firefox[^firefox-104-release-notes] [^librewolf-104-release] *(hello, zero days :wave:)*

[^firefox-104-release-notes]: Mozilla. ‘Firefox 104.0, See All New Features, Updates and Fixes’, 23 August 2022. https://www.mozilla.org/en-US/firefox/104.0/releasenotes/.
[^librewolf-104-release]: stanzabird. ‘Release V104.0 · LibreWolf / Browser / Windows · GitLab’. GitLab, 27 August 2022. https://gitlab.com/librewolf-community/browser/windows/-/releases/v104.0-1.
[^privacyguides-discussions-add-librewolf]: tommytran732, SkewedZeppelin, ph00lt0, Thorin-Oakenpants, savolla, fxbrit, TheFrenchGhosty, et al. ‘Add Librewolf · Discussion #423 · Privacyguides/Privacyguides.Org’. GitHub, 31 July 2022. https://github.com/privacyguides/privacyguides.org/discussions/423.

## Applying the LibreWolf configuration

The improvements seen in LibreWolf[^librewolf-features] are applicable to upstream versions of Firefox:

[^librewolf-features]: LibreWolf. ‘LibreWolf Browser’, 6 July 2022. https://librewolf.net/.

- Apply the Arkenfox `user.js`[^arkenfox-apply-update-maintain]
	- Add `user.js` to the profile directory, seen in `about:support`
	- Update to new releases using `updater.sh`
	- After updating, close Firefox and reset unneeded preferences with `prefsCleaner.sh`

- Install [uBlock Origin](https://github.com/arkenfox/user.js/wiki/4.1-Extensions)

	[The list below is derived from Extensions which I believe are the most popular in privacy circles.]: #

	Note that most extensions which claim to improve privacy and security are not worth using, including NoScript, Ghostery, Privacy Badger, ClearURLs, Decentraleyes and Cookie AutoDelete[^arkenfox-extensions].

	[^arkenfox-extensions]: Thorin-Oakenpants. ‘4.1 Extensions · Arkenfox/User.Js Wiki’. GitHub, 18 August 2022. https://github.com/arkenfox/user.js.
	
- Use a privacy respecting search engine, such as [DuckDuckGo](https://duckduckgo.com/) or [StartPage](https://www.startpage.com/)[^privacyguides-recommendations-providers-search-engines]

[^arkenfox-apply-update-maintain]: Thorin-Oakenpants. ‘3.4 Apply & Update & Maintain · Arkenfox/User.Js Wiki’. GitHub, 29 August 2022. https://github.com/arkenfox/user.js.
[^privacyguides-recommendations-providers-search-engines]: jonaharagon, d4rklynk, mmistakes, tommytran732, mfwmyfacewhen, elitejake, and RoseTheFlower. ‘Search Engines - Privacy Guides’. Privacy Guides, 7 August 2022. https://www.privacyguides.org/search-engines/.

# Conclusion

Firefox is reaching parity with Chromium's security, while providing privacy features that Chromium does not include.

For example:

[Use contrasting emoji for ticks and crosses. Visible in both Gokarna's Light and Dark modes.]: #

| Feature | Firefox | Chromium |
| ------- | ------- | -------- |
| Site Isolation | :white_check_mark:[^site-isolation-in-firefox] | :white_check_mark:[^site-isolation-in-chromium] |
| (Dynamic) First Party Isolation | :white_check_mark:[^dynamic-first-party-isolation-in-firefox_1] [^dynamic-first-party-isolation-in-firefox_2] | :x: |

80% of desktop browsers are based on Chromium[^browser-market-share-in-2022] (including Edge[^edge-uses-chromium] and Opera[^opera-uses-chromium]). We're in danger of losing the only modern alternative to Google's browser monoculture.

{{< figure src="/images/StatCounter-202107-202207.png" alt="A line graph captioned 'Desktop Browser Market Share Worldwide from July 2021 - July 2022'" >}}[^browser-market-share-in-2022]

It's time to [switch to Firefox](https://support.mozilla.org/en-US/kb/switching-chrome-firefox).

[^site-isolation-in-firefox]: Gakhokidze, Anny. ‘Introducing Firefox’s New Site Isolation Security Architecture – Mozilla Hacks - the Web Developer Blog’. Mozilla Hacks – the Web developer blog, 18 May 2021. https://hacks.mozilla.org/2021/05/introducing-firefox-new-site-isolation-security-architecture.
[^site-isolation-in-chromium]: The Chromium Projects. ‘Site Isolation’, 2021. https://www.chromium.org/Home/chromium-security/site-isolation/.
[^dynamic-first-party-isolation-in-firefox_1]: Huang, Tim, Johann Hofmann, and Arthur Edelstein. ‘Firefox 86 Introduces Total Cookie Protection’. Mozilla Security Blog, 23 February 2021. https://blog.mozilla.org/security/2021/02/23/total-cookie-protection.
[^dynamic-first-party-isolation-in-firefox_2]: Mozilla. ‘Firefox Rolls Out Total Cookie Protection By Default To All Users | The Mozilla Blog’. The Mozilla Blog, 14 June 2022. https://blog.mozilla.org/en/products/firefox/firefox-rolls-out-total-cookie-protection-by-default-to-all-users-worldwide/.
[^browser-market-share-in-2022]: StatCounter Global Stats. ‘Desktop Browser Market Share Worldwide’, July 2022. https://gs.statcounter.com/browser-market-share/desktop/worldwide.
[^edge-uses-chromium]: Microsoft Support. ‘Microsoft Edge (Chromium)’, 14 June 2022. https://support.microsoft.com/en-us/topic/microsoft-edge-chromium-1ce9507c-f09d-4de6-a706-eb52f46be90c.
[^opera-uses-chromium]: WebProNews. ‘The Chromium-Powered Opera Is Finally Here’, 28 May 2013. https://www.webpronews.com/the-chromium-powered-opera-is-finally-here/.
