---
title: "HTML attribute: autocomplete"
short-title: autocomplete
slug: Web/HTML/Reference/Attributes/autocomplete
page-type: html-attribute
browser-compat:
  - html.elements.form.autocomplete
  - html.elements.input.autocomplete
  - html.elements.select.autocomplete
  - html.elements.textarea.autocomplete
sidebar: htmlsidebar
---

The HTML `autocomplete` attribute lets web developers specify what if any permission the {{Glossary("user agent")}} has to provide automated assistance in filling out form field values, as well as guidance to the browser as to the type of information expected in the field.

It is available on {{HTMLElement("input")}} elements that take a text or numeric value as input, {{HTMLElement("textarea")}} elements, {{HTMLElement("select")}} elements, and {{HTMLElement("form")}} elements.

{{InteractiveExample("HTML Demo: autocomplete", "tabbed-shorter")}}

```html interactive-example
<label for="firstName">First Name:</label>
<input name="firstName" id="firstName" type="text" autocomplete="given-name" />

<label for="lastName">Last Name:</label>
<input name="lastName" id="lastName" type="text" autocomplete="family-name" />

<label for="email">Email:</label>
<input name="email" id="email" type="email" autocomplete="off" />
```

```css interactive-example
label {
  display: block;
  margin-top: 1rem;
}
```

## Description

The `autocomplete` attribute provides a hint to the user agent specifying how to, or indeed whether to, prefill a form control. The attribute value is either the keyword `off` or `on`, or an ordered list of space-separated tokens.

```html
<input autocomplete="off" />
<input autocomplete="on" />
<input autocomplete="shipping street-address" />
<input autocomplete="section-user1 billing postal-code" />
```

If an {{HTMLElement("input")}}, {{HTMLElement("select")}} or {{HTMLElement("textarea")}} element has no `autocomplete` attribute, the browser will use the [`autocomplete` attribute of the element's **owning form**](/en-US/docs/Web/HTML/Reference/Elements/form#autocomplete). The owning form is either the {{HTMLElement("form")}} matching the `id` specified by the [`form`](/en-US/docs/Web/HTML/Reference/Elements/input#form) attribute of the element (if present) or, more commonly, the `<form>` the element is nested in.

> [!NOTE]
> In order to provide autocompletion, user-agents might require `<input>`/`<select>`/`<textarea>` elements to:
>
> 1. Have a `name` and/or `id` attribute
> 2. Be descendants of a `<form>` element
> 3. Be owned by a form with a {{HTMLElement("input/submit", "submit")}} button

If the same list of tokens is used in more than one form control, the user-agent will autocomplete all occurrences of the same `autocomplete` value with the same data value.

Some tokens may be used more than once with potentially different expected values, such as the `zip-code` token in a form that contains both shipping and billing addresses. Including multiple different tokens in a space-separated list causes the associated form controls to be given unique autocomplete values: in this case, `autocomplete="shipping zip-code"` and `autocomplete="billing zip-code"`.

Some autocomplete values may need to be re-used multiple times. For example, a form may contain multiple shipping addresses and therefore multiple occurrences of `"shipping zip-code"` while still expecting different values. To make the autocomplete value unique in these cases, the first token in the space-separated list of tokens can be a `section-*` token, where the token's first eight characters are always the string "section-", followed by an alphanumeric string. All form fields given the `section-*` token with the same alphanumeric string belong to the same **named group**.

If including the `autocomplete` attribute on {{HTMLElement("input/hidden", "hidden")}} input elements (`<input type="hidden">`), its value must be an ordered list of space-separated tokens; the `on` and `off` keywords are not allowed.

The source of the suggested values is generally up to the browser; typically values come from past values entered by the user, but they may also come from pre-configured values. For instance, a browser might let the user save their name, address, phone number, and email addresses for autocomplete purposes. The browser may also offer the ability to save encrypted credit card information, for autocompletion following an authentication procedure.

> [!NOTE]
> The `autocomplete` attribute also controls whether Firefox will — unlike other browsers — [persist the dynamic disabled state and (if applicable) dynamic checkedness](https://stackoverflow.com/questions/5985839/bug-with-firefox-disabled-attribute-of-input-not-resetting-when-refreshing) of an `<input>` element, `<textarea>` element, or entire `<form>` across page loads. The persistence feature is enabled by default. Setting the value of the `autocomplete` attribute to `off` disables this feature. This works even when the `autocomplete` attribute would normally not apply by virtue of its `type`. See [Firefox bug 654072](https://bugzil.la/654072).

## Value

The attribute value is either the keyword `off` or `on`, or a space-separated `<token-list>` that describes the meaning of the autocompletion value.

- `off`
  - : The browser is not permitted to automatically enter or select a value for this field. It is possible that the document or application provides its own autocomplete feature, or that security concerns require that the field's value not be automatically entered.

    > [!NOTE]
    > In most modern browsers, setting `autocomplete` to `"off"` will not prevent a password manager from asking the user if they would like to save username and password information, or from automatically filling in those values in a site's login form. See [Managing autofill for login fields](/en-US/docs/Web/Security/Practical_implementation_guides/Turning_off_form_autocompletion#managing_autofill_for_login_fields).

- `on`
  - : The browser is allowed to automatically complete the input. No guidance is provided as to the type of data expected in the field, so the browser may use its own judgement.

- `<token-list>`
  - : An ordered set of [space-separated tokens](#token_list_tokens) consisting of autofill detail tokens preceded by optional sectioning and either billing or shipping grouping tokens. Phone numbers, email addresses, and messaging protocol tokens are preceded by a token identifying the type of recipient.

See the [WHATWG Standard](https://html.spec.whatwg.org/multipage/forms.html#autofill) for more detailed information.

### Token list tokens

The `<token-list>` options include, in order:

1. [Group naming token](#named_groups)
2. [Grouping identifier](#grouping_identifier)
3. [Detail tokens](#detail_tokens)
4. [Web authorization](#web_authorization_token)

#### Named groups

To create a named group of form fields, the optional `section-*` token can be used. If present, this token must be the first token in the space-separated list of tokens.

- `section-*`
  - : Defines the name for a group of form controls. A token whose first eight characters are the string "section-", case-insensitive, followed by additional characters. All form controls that start with the same token belong to the named group.

#### Grouping identifier

An optional `shipping` or `billing` grouping identifier

- `shipping`
  - : The field identified by subsequent tokens is part of the shipping address or contact information
- `billing`
  - : The field identified by subsequent tokens is part of the billing address or contact information

#### Detail tokens

Each space-separated detail token list includes either a recipient type with digital contact information, in that order, or a space-separated token list of other tokens.

##### Recipient type

The tokens that identify the type of recipient include:

- `home`
  - : The contact type identified by subsequent tokens is for contacting the recipient at their residence.
- `work`
  - : The contact type identified by subsequent tokens is for contacting the recipient at their work.
- `mobile`
  - : The contact type identified by subsequent tokens is for contacting the recipient regardless of location.
- `fax`
  - : The recipient identified by subsequent tokens is for a fax machine.
- `page`
  - : The recipient identified by subsequent tokens is for a pager or beeper.

##### Digital contact tokens

The token or group of tokens for telephone numbers or a number's component parts, phone extensions, email addresses, or instant messaging protocols.

- `tel`
  - : A full telephone number, including the country code. If you need to break the phone number up into its components, you can use these values for those fields:
    - `tel-country-code`
      - : The country code, such as "1" for the United States, Canada, and other areas in North America and parts of the Caribbean.
    - `tel-national`
      - : The entire phone number without the country code component, including a country-internal prefix. For the phone number "1-855-555-6502", this field's value would be "855-555-6502".
    - `tel-area-code`
      - : The area code, with any country-internal prefix applied if appropriate.
    - `tel-local`
      - : The phone number without the country or area code. This can be split further into two parts, for phone numbers which have an exchange number and then a number within the exchange. For the phone number "555-6502", use `tel-local-prefix` for "555" and `tel-local-suffix` for "6502".

- `tel-extension`
  - : A telephone extension code within the phone number, such as a room or suite number in a hotel or an office extension in a company.
- `email`
  - : An email address.
- `impp`
  - : A URL for an instant messaging protocol endpoint, such as `xmpp:username@example.net`.

##### Other tokens

When the form field is not a phone number, email address, or instant messaging protocol, the space-separated list of tokens is not preceded by a contact type:

- `name`
  - : The field expects the value to be a person's full name. Using `name` rather than breaking the name down into its components is generally preferred because it avoids dealing with the wide diversity of human names and how they are structured; however, you can use the following `autocomplete` values if you do need to break the name down into its components:
    - `honorific-prefix`
      - : The prefix or title, such as "Mrs.", "Mr.", "Miss", "Ms.", "Dr.", or "Mlle.".
    - `given-name`
      - : The given (or "first") name.
    - `additional-name`
      - : The middle name.
    - `family-name`
      - : The family (or "last") name.
    - `honorific-suffix`
      - : The suffix, such as "Jr.", "B.Sc.", "PhD.", "MBASW", or "IV".
    - `nickname`
      - : A nickname or handle.

- `username`
  - : A username or account name.
- `new-password`
  - : A new password. When creating a new account or changing passwords, this should be used for an "Enter your new password" or "Confirm new password" field, as opposed to a general "Enter your current password" field that might be present. This may be used by the browser both to avoid accidentally filling in an existing password and to offer assistance in creating a secure password.
- `current-password`
  - : The user's current password.
- `one-time-code`
  - : A one-time password (OTP) for verifying user identity that is used as an additional factor in a sign-in flow.
    Most commonly this is a code received via some out-of-channel mechanism, such as SMS, email, or authenticator application.
- `organization-title`
  - : A job title, or the title a person has within an organization, such as "Senior Technical Writer", "President", or "Assistant Troop Leader".
- `organization`
  - : A company or organization name, such as "Acme Widget Company" or "Girl Scouts of America".
- `street-address`
  - : A street address. This can be multiple lines of text, and should fully identify the location of the address within its second administrative level (typically a city or town), but should not include the city name, ZIP or postal code, or country name.
    - `address-line1`, `address-line2`, `address-line3`
      - : Each individual line of the street address. These should only be present if the `street-address` is not present.
- `address-level4`
  - : The finest-grained [administrative level](#administrative_levels_in_addresses), in addresses which have four levels.
- `address-level3`
  - : The third [administrative level](#administrative_levels_in_addresses), in addresses with at least three administrative levels.
- `address-level2`
  - : The second [administrative level](#administrative_levels_in_addresses), in addresses with at least two of them. In countries with two administrative levels, this would typically be the city, town, village, or other locality in which the address is located.
- `address-level1`
  - : The first [administrative level](#administrative_levels_in_addresses) in the address. This is typically the province in which the address is located. In the United States, this would be the state. In Switzerland, the canton. In the United Kingdom, the county.
- `country`
  - : A country or territory code.
- `country-name`
  - : A country or territory name.
- `postal-code`
  - : A postal code (in the United States, this is the ZIP code).

- `cc-name`
  - : The full name as printed on or associated with a payment instrument such as a credit card. Using a full name field is preferred, typically, over breaking the name into pieces.
    - `cc-given-name`
      - : A given (first) name as given on a payment instrument like a credit card.
    - `cc-additional-name`
      - : A middle name as given on a payment instrument or credit card.
    - `cc-family-name`
      - : A family name, as given on a credit card.
- `cc-number`
  - : A credit card number or other number identifying a payment method, such as an account number.
- `cc-exp`
  - : A payment method expiration date, typically in the form "MM/YY" or "MM/YYYY".
    - `cc-exp-month`
      - : The month in which the payment method expires.
    - `cc-exp-year`
      - : The year in which the payment method expires.
- `cc-csc`
  - : The security code for the payment instrument; on credit cards, this is the 3-digit verification number on the back of the card.
- `cc-type`
  - : The type of payment instrument (such as "Visa" or "Master Card").
- `transaction-currency`
  - : The currency in which the transaction is to take place.
- `transaction-amount`
  - : The amount, given in the currency specified by `transaction-currency`, of the transaction, for a payment form.
- `language`
  - : A preferred language, given as a valid [BCP 47 language tag](https://en.wikipedia.org/wiki/IETF_language_tag).
- `bday`
  - : A birth date, as a full date.
    - `bday-day`
      - : The day of the month of a birth date.
    - `bday-month`
      - : The month of the year of a birth date.
    - `bday-year`
      - : The year of a birth date.
- `sex`
  - : A gender identity (such as "Female", "Fa'afafine", "Hijra", "Male", "Nonbinary"), as freeform text without newlines.
- `url`
  - : A URL, such as a home page or company website address as appropriate given the context of the other fields in the form.
- `photo`
  - : The URL of an image representing the person, company, or contact information given in the other fields in the form.

#### Web authorization token

With {{htmlelement("input")}} and {{htmlelement("textarea")}}, the `webauthn` token can be included last to indicate the user agent should show public key credentials when the user is interacting with the control.

- `webauthn`
  - : Passkeys generated by the [Web Authentication API](/en-US/docs/Web/API/Web_Authentication_API), as requested by a conditional {{domxref("CredentialsContainer.get()", "navigator.credentials.get()")}} call (i.e., one that includes `mediation: 'conditional'`). If included, this is the last token in the space-separated token list. See [Sign in with a passkey through form autofill](https://web.dev/articles/passkey-form-autofill) for more details.

## Examples

```html
<div>
  <label for="cc-number">Enter your credit card number</label>
  <input name="cc-number" id="cc-number" autocomplete="off" />
</div>
```

### Administrative levels in addresses

The four administrative level fields (`address-level1` through `address-level4`) describe the address in terms of increasing levels of precision within the country in which the address is located. Each country has its own system of administrative levels, and may arrange the levels in different orders when addresses are written.

`address-level1` always represents the broadest administrative division; it is the least-specific portion of the address short of the country name.

### Form layout flexibility

Given that different countries write their address in different ways, with each field in different places within the address, and even different sets and numbers of fields entirely, it can be helpful if, when possible, your site is able to switch to the layout expected by your users when presenting an address entry form, given the country the address is located within.

### Variations

The way each administrative level is used will vary from country to country. Below are some examples; this is not meant to be an exhaustive list.

#### United States

A typical home address within the United States looks like this:

432 Anywhere St
Exampleville CA 95555

In the United States, the least-specific portion of the address is the state, in this case "CA" (the official US Postal Service shorthand for "California"). Thus `address-level1` is the state, or "CA" in this case.

The second-least specific portion of the address is the city or town name, so `address-level2` is "Exampleville" in this example address.

United States addresses do not use levels 3 and up.

#### United Kingdom

Address input forms in the UK should contain one or two address levels and one, two or three address lines, depending on the address. A complete address would look like so:

103 Frogmarch Street
Upper-Wapping
Winchelsea
Whereshire
TN99 8ZZ

The address levels are:

- `address-level1`: The county — "Whereshire" in this case.
- `address-level2`: The post town — "Winchelsea" in this case.
- `address-line2`: The locality — "Upper-Wapping" in this case.
- `address-line1`: The house/street particulars — "103 Frogmarch Street".

The postcode is separate. Note that you can actually use just the postcode and `address-line1` to successfully deliver mail in the UK, so they should be the only mandatory items, but usually people tend to provide more details.

#### China

China can use as many as three administrative levels: the province, the city, and the district.

The 6 digit postal code is not always needed but when supplied it is placed separately with a label for clarity. For example:

北京市东城区建国门北大街 8 号华润大厦 17 层 1708 单元
邮编：100005

#### Japan

An address in Japan is typically **written in one line**, in an order from the least-specific to more-specific portions (in **reverse order to the United States**). There are two or three administrative levels in an address. Additional line can be used to show building names and room numbers. The postal code is separate. For example:

〒 381-0000
長野県長野市某町 123

"〒" and following seven digits shows the postal code.

`address-level1` is used for prefectures or the Tokyo Metropolis; "長野県" (Nagano Prefecture) is in this case. `address-level2` is typically used for cities, counties, towns and villages; "長野市" (Nagano City) in this case. "某町 123" is `address-line1` which consists of an area name and a lot number.

## Specifications

{{Specifications}}

## Browser compatibility

{{Compat}}

## See also

- The {{htmlelement("input")}} element
- The {{htmlelement("select")}} element
- The {{htmlelement("textarea")}} element
- The {{htmlelement("form")}} element
- [HTML forms](/en-US/docs/Learn_web_development/Extensions/Forms)
- All [global attributes](/en-US/docs/Web/HTML/Reference/Global_attributes)
