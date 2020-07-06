---
layout: default
title: DKIM
parent: DNS

---
# DomainKeys Identified Mail \(DKIM\)
{: .no_toc }

## Table of contents
{: .no_toc .text-delta }

1. TOC
{:toc}

---

## TLDR

DKIM provides an encryption key and digital signature to verify that what you sent was not changed, spoofed, or modified in any way.

## How It Works

DKIM relies on a public/private key pair to sign and verify email messages. A public key is posted on DNS as a TXT record under _**selector**_**.\_domainkey.example.com.** Your sending server would then sign the email messages with the private key that can later be verified by the sending server with the public key. Once verified, the receiving server can be sure that the message was authorized and was not modified in transit.

> **NOTE:** Appended headers and footer messages \(compliance disclosures or cybersecurity reminders\) must be attached at the signing sender or receiving server in order to not fail DKIM.

## How It Is Set Up

### Exchange

A project called DKIM-exchange is a great tool to sign messages that are routed through Exchange. You can find this project at [https://github.com/Pro/dkim-exchange](https://github.com/Pro/dkim-exchange). Verify that your version of exchange is compatible with this project. Install information copied from their project.

{% embed url="https://github.com/Pro/dkim-exchange" %}

#### Install:

* Download the latest GUI package: [https://github.com/Pro/dkim-exchange/releases/latest](https://github.com/Pro/dkim-exchange/releases/latest) \(Configuration.DkimSigner.zip\)
* Extract it somewhere on your Server \(e.g. Desktop\)
* Start Configuration.DkimSigner.exe
* Select `Install`
* In the new opened window, select the version you like to install. If you want to install a prerelease version, check the corresponding box
* Press install and wait until the installation successfully finished, then close the window.
* Now configure the DKIM Signer with the installed GUI \(located under `"C:\Program Files\Exchange DkimSigner\Configuration.DkimSigner.exe"`
* Once you save the config, the Signer Agent will automatically reload these changes

#### Configuration:

After installing the agent, you can use the Configuration.DkimSigner.exe within `C:\Program Files\Exchange DkimSigner` to configure the agent and all the settings. If the GUI doesn't work, you can also configure it manually \(see section below\).

> **Please Note:**  
> If you have configured your server to only send in the TNEF message format, your mails will not be signed. To disable it, use the following powershell command

```text
Set-RemoteDomain -Identity * -TNEFEnabled $false
```

**DKIM Settings Tab**

* Set Canonicalization for Header and Body to **Relaxed**. This allows very minor changes to the email message \(such as extra blank lines at the bottom of the message and allows the header names \(not values\) to be switched to lower case.
  * Header - Simple allows no changes to the header in any way. Relaxed allows for converting header names to lower case, converting multiple spaces to a single spaces, and other minor changes.
  * Body - Simple ignores empty lines at the end of the body with no other changes to the body. Relaxed allows for blank lines at the bottom, ignores spaces at the ens of lines, reduces all multiple spaces in a line to a single space, and other minor changes.

> Reference: [http://help.altn.com/mdaemon/en/security--dkim\_options.htm](http://help.altn.com/mdaemon/en/security--dkim_options.htm)

**Domain Settings Tab**

* Select **Add** to add a new domain to sign for
* Set your sending **domain name** like example.com
* Set a **selector.** This can be anything. This is what you will reference in DNS
* Give it a **filename** if required
* Set a desired **key length**
* Select **Generate New Key**
* You will see a **Suggested DNS name.** Create a new TXT DNS record at that location on your public DNS \(and private DNS if you use the same domain privately\).
* You will see a **Suggested DNS record.** Copy this record to your clipboard and paste this as the value to that TXT DNS record.
* Verify the DKIM signer sees that DNS record by selecting **Check.**
* Select **Save Domain**

#### Updating Exchange:

The DKIM-Exchange project gave some special instructions for when you update Exchange:

> Before you update the Exchange Server, you have to make sure that the DKIM Signer Version is compatible with the new Exchange Version. Thus the following steps are suggested to avoid any Upgrade problems:
>
> * Disable the DKIM Signer \(Open the configuration executable, on the `Information` tab press `Configure`, then disable the DKIM Signer\)
> * Update the Exchange Server
> * Update the DKIM Signer \(using the configuration executable\)
>   *  If you want to update the Exchange DKIM Transport Agent simply run Configuration.DkimSigner.exe and on the `Information` tab press the Upgrade button. \(If no new version is available the button shows 'Reinstall'\).
> * Re-enable the DKIM Signer

## Example DKIM Public Record

TXT DNS - **selector.\_domainkey.example.com:**

"v=DKIM1; k=rsa; p=MIIBIjANBgkqhkiG9w0BAQEFAAOCAQ8AMIIBCgKCAQEAsiv4mVODIx6hAfsjPoxRl+h0AvN8MviDRoMiJxe0NzpslN2NH2xofQgQpIVBkkexZpC9m0E6gp3ES3tPutyglcS2pps+DHbOegfi/nY3l69JVhBjNXl0whN20/FC3Adh0CETyRtKpI0HJStzr1A4+Q9cAGW4hmAguJ1iwZ1FsFEOrI8Qe/ZtxZo8V1x4oWauhk9XOU+ZUGRYDXTXeuEWyvtlfr5WN7N9I5tlD3BFMyB74k/LaVw6/kRC2fm6ug8MoM11hYxt2f1s0jLeDSLh7Jyju9jHSaVJy1nRRDsf4veyA/JCtmvwPJE3teYWlXIqTksMciWij4vyCTgAGmopxQIDAQAB"

> **NOTE**: Not an actual record for that domain and a random key generated just for this example.

