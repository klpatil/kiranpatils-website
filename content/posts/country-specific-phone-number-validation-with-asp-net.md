---
_edit_last: "2"
_oembed_5d7d0f28b80cb66fa8eb868a1707c9ad: '{{unknown}}'
_oembed_5087752cd221531f6e27d0f87f9016fd: '{{unknown}}'
_oembed_86971373304a68f48fe9c007144cfe4a: '{{unknown}}'
_publicize_done_external:
  twitter:
    "84883544": true
_wpas_done_49263: "1"
_wpas_skip_49263: "1"
author: kpatil
categories:
  - asp.net
  - asp.net-controls
  - goodtoknow
  - javascript
  - jquery
  - uncategorized
  - web-dev-(.net,-html,-etc)
date: "2014-02-15T18:10:04+00:00"
geo_accuracy: "0"
geo_latitude: "0"
geo_longitude: "0"
geo_public: "0"
guid: http://kiranpatils.wordpress.com/?p=1101
parent_post_id: null
post_id: "1101"
publicize_twitter_url: http://t.co/cy5H7a9f15
publicize_twitter_user: kiranpatils
tags:
  - customvalidator
  - libphonenumber
  - validation
title: Country specific phone number validation with ASP.NET
url: /2014/02/15/country-specific-phone-number-validation-with-asp-net/

---
### Challenge:

Before few weeks back, I have been assigned a task, Where I need to validate a phone number. Sound simple? Yes it is! But I needed to do it country specific? Now, how it sounds?
Basically, User will have a list of countries to select. And based on his/her country selection he/she will provide phone number and we should validate based on country selection. Sounds challenging? That's how life should be!
You are also working on such thing and looking for a way to get out of it? Then this post is for you!

### Solution:

As per every software engineer's practice, I started my research and our common friend. Google presented option of using Regex for each country. But it sounded bit complex to me. Then continued my research and found a super hero!
**[LibPhoneNumber](https://code.google.com/p/libphonenumber/) :** It's a library from Google champs to validate phone number (Excerpt from their main page -- _Google's common Java, C++ and Javascript library for parsing, formatting, storing and validating international phone numbers. The Java version is optimized for running on smartphones, and is used by the Android framework since 4.0 (Ice Cream Sandwich)._)
And after reading this description, It attracted me! (To you as well?). It's good we found HERO. But how to fit him in our picture? Then after doing bit of a research found this two nice components:

1. [http://phoneformat.com/](http://phoneformat.com/) \-\- Javascript version of Google’s libphonenumber library
1. [http://libphonenumber.codeplex.com/](http://libphonenumber.codeplex.com/) \- C# port of Google's libphonenumber

This was a Eureka moment. Just plugged both of this libraries with **CustomValidator** and you are done! So, here's how CustomValidator clientside and server-side functions looks like:
Blogs
SUGIN
\[sourcecode language="html"\]
<asp:<span class="hiddenSpellError">TextBox ID="txtPhone"  runat="server" />
<asp:<span class="hiddenSpellError">RequiredFieldValidator ID="reqTxtPhone"
runat="server" ErrorMessage="Please enter a phone number" Text="\*" ControlToValidate="txtPhone"
></asp:RequiredFieldValidator>
<asp:<span class="hiddenSpellError">CustomValidator ID="custPhoneNumber" runat="server"
OnServerValidate="PhoneNumberValidate"
ErrorMessage="Please enter valid phone number"
Text="\*"
ControlToValidate="txtPhone"
ClientValidationFunction="PhoneNumberValidate"
/>
\[/sourcecode\]

\[sourcecode language="javascript"\]
/\*
This function will be used to validate
Phone Number client side by CustomValidator
\*/
function PhoneNumberValidate(oSrc,args) {
// Call PhoneFormat.JS function which takes Phone Number and Country Code
// in ISO 3166-1 format
var isValidNumberOrNot = isValidNumber(txtPhone.value, ddlcountry.value);
arg.IsValid = isValidNumberOrNot;
}
\[/sourcecode\]
\[sourcecode language="csharp"\]
/// <summary>
/// This function will be used to validate
/// Phone Number server side by CustomValidator
/// </summary>
/// <param name="source">Source</param>
/// <param name="args">Arguments</param>
protected void PhoneNumberValidate(object source, ServerValidateEventArgs args)
{
PhoneNumberUtil phoneUtil = PhoneNumberUtil.Instance;
// TODO : EXCEPTION HANDLING
string countryCode = ddlcountry.SelectedItem.Value
if (string.IsNullOrEmpty(countryCode))
{
args.IsValid = false;
}
else
{
PhoneNumber phoneNumber = phoneUtil.Parse(txtPhone.Text, countryCode);
bool isValidNumber = phoneNumber.IsValidNumber;
args.IsValid = isValidNumber;
}
}
</span></span></span>
\[/sourcecode\]
_Just a note : LibPhoneNumber accepts country code in [ISO 3166-1](http://en.wikipedia.org/wiki/ISO_3166-1) format. But if you've drop down Text and Value both in full form e.g. "India" and you need to pass it as "IN" and If it's not possible to do any change at your DropDown value level then you can use function, Which has been submitted at -- [https://github.com/albeebe/phoneformat.js/issues/9](https://github.com/albeebe/phoneformat.js/issues/9) It converts CountryName to CountryCode_
Happy Phone Number Validation! :-)
