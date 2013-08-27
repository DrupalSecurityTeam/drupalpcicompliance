---
title: Top 12 Drupal PCI Compliance Myths
layout: post
category: article
author: Rick Manelius
tags : [Drupal, PCI compliance, security]
---

_[Jump right to the myths](#myths)_

True story: we had just completed a six figure eCommerce project for a client that wanted to improve their online sales (an admirable goal) to supplement their successful brick and mortar business. However, when it came to hosting they wanted to do it on the cheap with one of the many $7/month shared hosting plans advertised all over the internet. Ignoring the obvious performance considerations (of which there were many), there was simply no way our client was going to be able to implement the necessary security configurations on this shared-hosting environment to meet their PCI compliance obligations.

We immediately warned our client that this was a bad idea and cited the reasons why. To our dismay, our client then informed us that a support representative at the hosting company stated that there was nothing to worry about and that the servers were compliant. This was a blatant lie and our client wanted to believe it because nobody wants to feel duped. Thankfully, we were able to get the client to reconsider after we provided additional information.

This is just one example of the uphill battle we face...

In short, there is a lot of misinformation, disinformation, and lack of correct information out there regarding PCI compliance for the Drupal platform. To help fix this, two colleagues and I recently published a _[Drupal PCI compliance white paper](http://drupalpcicompliance.org/)_ that gives a high level overview of the subject matter as well as appropriate next steps for anyone involved in Drupal eCommerce([1](#cite-1)).

That said, there is only so much information we could pack into the paper while keeping it short enough in length to meet all the intended goals of the project (i.e. easy to read, concise, accurate).

This article expands upon the "myths" section of the paper. If you have any questions or constructive, then please leave us a comment below. We'll use said feedback to improve the quality of this article as well as the paper itself.

_If you have no idea what PCI compliance is and/or why you should care, we highly recommend reading the executive summary and introduction of the [white paper](http://drupalpcicompliance.org) before proceeding._

<a name="myths"> </a>

### Myth 1: Drupal is PCI Compliant.

Drupal _can_ be a part of a fully PCI compliant card data environment (CDE) when it is correctly setup, configured, and maintained within in the context of the rest of the system. The most important point to emphasize is that Drupal is only one component the total environment, which requires a holistic approach to ensure that entire process of processing, transmitting, and/or storing card data is secured from end to end.

Example: a developer can perform a thorough security audit and ensure that a website is properly configured and that all code has been updated with the latest security patches. However, if the server's password is simply "password" or an unauthorized person has physical access to the server, the integrity of that code can be compromised rather easily. This would undermine all the work done by the developer.

In short, the security of a Drupal site (with respect to credit card processing) is only as strong as the weakest link. Therefore, the question of whether or not Drupal is PCI compliant is ill posed because Drupal cannot become compliant by itself.

A second point to underscore is the highly configurable nature of Drupal and the impact that this can have on its security. One could completely configure it to adhere to best practices and (in combination with the rest of the CDE) achieve PCI compliance. However, changing a single configuration in an inappropriate manner could eliminate one's compliance (e.g. disabling a module that enforced HTTPS).

There are additional issues that affect a Drupal application's PCI compliance, such as password strength for administrative users, a company security policy, etc.

It's better to think of Drupal as PCI _compatible_ to emphasize that it can be properly used in the context of a secure, PCI compliant environment. However, it itself is *not* PCI compliant.



### Myth 2: Ubercart and Drupal Commerce are PCI Compliant

All responses to Myth #1 apply equally here with the addition of two other points. 

1) Installation and configuration is especially important here with respect to the payment gateways selected. A merchant-managed solution (where the credit card is sent directly to Drupal) has many more places that are vulnerable to a security breach when compared to shared-management solutions, such as redirecting to an externally hosted payment page secured by PayPal, Authorize.Net, etc.

2) There is an oddity in the PA-DSS standard that basically states that all open source code must be maintained as if the person using it was the creator/author of said code. Therefore the user is responsible for the security of the code and not the community from which it was derived. Therefore, even if was possible to claim that _Ubercart_ or _Drupal Commerce_ were PCI compliant, the onus would fall on the user to prove that.

### Myth 3: I Only Need HTTPs to Be Secure.

Securing the transaction from the Drupal application to the payment gateway addresses only one of the 12 sections of the PCI standard. There are a significant number of other vulnerabilities that can exist at the server, network, and application level.

For more examples specific to Drupal, see the _Drupal Specific Exploits_ section of the [white paper](http://drupalpcicompliance.org).

### Myth 4: I am PCI Compliant; Therefore I'm Untouchable. 

The unfortunate reality is that PCI compliance is not a guarantee against all possible attacks([2](#cite-2)). However, it _DOES_ offer a safe harbor for those that can prove they were compliant at the time of the incident. The main benefit of this safe harbor is that the company experiencing the breach will not have to incur the $25-$215 fine per transaction in the calendar year of the breach.

Two take home points:

1. PCI compliance should be considered a minimum level of security that should be attained and maintained when handling credit card transactions.
2. Part of the PCI DSS standard (Requirement 12) addresses a proper course of action in the event of a breach. The point of this requirement is to emphasize that one must still plan for that possibility despite having all the proper security measures in place because PCI compliance is not a silver bullet.

### Myth 5: I Can Achieve PCI Compliance Using Shared Hosting.

Shared hosting is simply not secure enough for PCI SAQ C because there are simply too many users (both customers and employees of the hosting company) that have access to the server and you simply do not have enough control in locking down the system.

It is possible to become PCI compliant using cloud hosting, but proper research must be done. Most reputable companies will explicitly state on their websites whether or not they can be compliant. Examples: 

1. Rackspace Cloud cannot be PCI compliant because of their multi-tenant data center infrastructure([3](#cite-3)).
2. Amazon AWS EC2 can be part of a PCI compliant CDE and will even provide you their documentation if you comply with their NDA([4](#cite-4)).

If you're hosting provider does not explicitly state this information, it's imperative that you communicate with them to get an answer in writing.

### Myth 6: Shared-management Methods are 100% Foolproof

This is false because modifying code at the Drupal application layer can result in a man in the middle attack, the introduction of a keylogger, etc.

The _Information Supplement: PCI DSS E-commerce Guidelines_ document from the _PCI Standards Security Council_([5](#cite-5)) states this very clearly in section 3.4.3.

_"PCI DSS Scoping Guidance: Merchants should understand that outsourcing to a third party via a shared- management implementation does not allow the merchant to outsource PCI DSS responsibility, regardless of whether a merchant is eligible to complete a self-assessment questionnaire (SAQ). With each of these shared-management implementations, there is still security risk for the merchant since weaknesses on the merchant’s website can lead to compromise of the payment card data during the transaction process. See “Security Considerations for Shared-Management E-commerce Implementations” on page 17 for risks specific to each implementation. Due to these risks to a merchant’s website and payment card data, even in outsourced scenarios, it is recommended that merchants implement applicable PCI DSS controls as needed to ensure the security of the website."_

The document event goes as far as outlining the specific means that each shared-management method can be attacked in section 3.4.3.4.

* _"Direct-post API Approach: With the direct-post API approach, the merchant is still responsible for the web page that is presented to the consumer, and the merchant hosts the fields on the payment page that accept the data—only the cardholder data is posted directly from the consumer to the service provider. Since the payment pages are hosted by the merchant, the payment pages are only as secure as the merchant’s web site, and a compromise of the merchant’s system could lead to a compromise of payment card data."_
* _"iFrame Approach: With the iFrame approach, the iFrame must be configured and managed to prevent it from being modified to send cardholder data to an alternate and unauthorized source."_
* _"Hosted-payment Page Approach: With hosted payment pages, a compromise of the merchant’s server could lead to redirection of communications intended for the e-commerce payment processor, allowing payment card data to be intercepted and stolen as transactions occur."_

The point is that shared-management solutions, while significantly more secure than merchant-managed solutions, are not silver bullet solutions that allow one to completely outsource their responsibility.

### Myth 7: PCI Compliance is _Their_ Responsibility.

The process of achieving compliance also requires a holistic approach and cannot be placed on just the development team, operations team, management, leadership, etc. Decisions and actions made by any one party can undermine the efforts of everyone else. Therefore, PCI compliance is a team effort.

### Myth 8: I Can Store Credit Card/CCV Numbers

Storing the 3-4 digit security code is never allowed under any circumstances. Storing the full credit card number at the Drupal layer is extremely risky and should not be done without a considerable amount of attention.

### Myth 9: I can set it and forget it.

PCI compliance is not a single event that is checked off a list and never revisited. Rather, it’s a continually changing state. If a security exploit is discovered and disclosed for Drupal or the OS running the server Drupal is hosted on, then your site is not PCI compliant. Therefore PCI compliance is a continual process that needs to be maintained through vigilance.

### Myth 10: PCI Compliance Doesn't Apply to Me Because I Only Sell a Few Items a Month.

Compliance begins at transaction zero (i.e. the moment you turn on your cart to begin accepting payments).

### Myth 11: Compliance is Optional.

While it's true that filling out the self-assessment questionnaire may be optional depending on the transaction volume, compliance itself is not optional. It is a contractual obligation that you must meet in order for the privilege us accepting credit card payments through a merchant account. Be sure to read the fine print!

### Myth 12: Ignorance is Bliss.

While it is possible to operate an eCommerce site for many years without a single issue, the risks that one places on their business are huge. One can experience heavy fines, a public relations nightmare, and the loss of the ability to accept payments in the future.

The best course of action is to get informed. There are solutions out there, particularly shared-management gateways, that can significantly reduce the risk of experiencing a breach and reduce the time, effort, and resources required to become compliant.

### Get the Paper

If you found this useful, we highly encourage you to download the full white paper, read it, and follow-up with any questions or feedback. Thanks for your time and attention on this important subject matter!

### References

1. &#x20;<a name="cite-1"></a>[Drupal PCI Compliance White Paper: Official Homepage](http://goo.gl/JNHNNs)
2. &#x20;<a name="cite-2"></a>[Cyberattacks on the rise as credit, debit card numbers become commodities](http://goo.gl/ER3w3l)
3. &#x20;<a name="cite-3"></a>[Rackspace: PCI Frequently Asked Questions](http://goo.gl/zRW9g0)
4. &#x20;<a name="cite-4"></a>[Amazon: PCI DSS Level 1 Compliance](http://goo.gl/n5n4lu)
5. &#x20;<a name="cite-5"></a> [Information Supplement: PCI DSS E-commerce Guidelines](http://goo.gl/Nqc25M)
