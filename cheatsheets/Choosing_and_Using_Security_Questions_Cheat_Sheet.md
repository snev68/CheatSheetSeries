# Introduction

Security questions are used by many websites to allow a user to regain access to their account if they have forgotten their password, or have lost their secondary authentication factors when multifactor authentication (MFA) is required. However, they are often a significantly weaker form of authentication than passwords, and there have been a number of high profile cases where they have allowed attacker to compromise users' accounts.

Security questions **should not be relied upon as a sole mechanism to authenticate a user**. However, they can provide a useful additional layer of security when [MFA](Multifactor_Authentication_Cheat_Sheet.md) is not available.

This cheat sheet provides guidance on both how to choose strong security questions, and how to use them securely within an application.

# Contents

**FIXME**

# Choosing Security Questions

## Desired Characteristics

Any security questions or identity information presented to users to reset forgotten passwords must meet the following characteristics:

| Characteristic | Explanation |
|----------------|-------------|
| Memorable | The user must be able to recall the answer to the question, potentially years after creating their account. |
| Consistent | The answer to the question must not change over time. |
| Applicable | The user must be able to answer the question.
| Confidential | The answer to the question must be hard for an attacker to obtain. |
| Specific | The answer should be clear to the user. |

## Types of Security Questions

Security questions fall into two main types. With *user defined* security questions, the user must choose a question from a list, and provide an answer to the question. Common examples are "What is your favourite colour?" or "What was your first car?"

These are easy for applications to implement, as the additional information required is provided by the user when they first create their account. However, users will often choose weak or easily discovered answers to these questions.

*System defined* security questions are based on information that is already known about the user. This can include personal details (such as  an address or date of birth), or details about the user's account (such as when the account was opened or details of recent transactions).

This approach avoids having to ask the user to provide specific security questions and answers, and also prevents them from being able to choose weak details. However it relies on sufficient information already being stored about the user, and on this information being hard for an attacker to obtain.

## User Defined Security Questions

### Bad Questions

Any questions that breaks one or more of the characteristics discussed above should be avoided. The table below gives some examples of bad security questions:

| Question | Problem |
|----------|---------|
| When is your date of birth? | Easy for an attacker to discover. |
| What is your memorable date? | Most users will just enter their birthday. |
| What is your favourite movie? | Likely to change over time. |
| What is your favourite cricket team? | Not applicable to most users. |
| What is the make and model of your first car? | Fairly small range of likely answers. |

Additionally, when the context of the application must be considered when deciding whether questions are good or bad. For example, a question such as "What was your maths teacher's surname in your 8th year of school?" would be very easy to guess if it was using in a virtual learning environment for a school, but would be much stronger for an online gaming website.

### Good Questions

Many good security questions are not applicable to all users, so the best approach is to give the user a list of security questions that they can choose from. This allows you to have more specific questions (with more secure answers), while still providing every user with questions that they can answer.

The following list provides some examples of good questions:

- What are the last four digits of your national insurance or social security number?
- What was your maths teacher's surname in your 8th year of school?
- What was the name of your first stuffed toy?
- What was your driving instructor's first name?

Much like passwords, there is a risk that users will re-use recovery questions between different sites, which could expose the users if the other site is compromised. As such, there are benefits to having unique security questions that are unlikely to be shared. An easy way to achieve this is to create more targeted questions based on the type of application. For example, on a share dealing platform, financial related questions such as "What is the first company you owned shares in?" could be used.

### Allowing Users to Write Their Own Questions

Allowing users to write their own security questions can result in them choosing very strong and unique questions that would be very hard for an attacker to guess. However, there is also a significant risk that users will choose weak questions. In some cases, users might even set a recovery question to a reminder of what their password is - allowing anyone guessing their email address to compromise their account.

As such, it is generally best not to allow users to write their own questions.

### Restricting Answers

Enforcing a minimum length for answers can prevent users from entering strings such as "a" or "123" for their answers. However, depending on the questions asked, it could also prevent users from being able to correctly answer the question. For example, if asking for a first name or surname could result in a two letter answer such as "Li", and a colour-based question could be four letters such as "blue".

Answers should also be checked against a blacklist, including:

- The username or email address.
- The user's current password.
- Common strings such as "123" or "password".

### Renewing Security Questions

If the security questions are not used as part of the main authentication process, then consider periodically prompting the user to review their security questions and verify that they still know the answers. This should give them a chance to update any answers that may have changed (although ideally this shouldn't happen with good questions), and increases the likelihood that they will remember them if they ever need to recover their account.

## System Defined Security Questions

System defined security questions are based on information that is already known about the user. The users' personal details are often used, including the full name, address and date of birth - however these can easily be obtained by an attacker from social media, and as such provide a very weak level of authentication.

The questions that can be used will vary hugely depending on the application, and how much information is already held about the user. When deciding which bits of information may be usable for security questions, the following areas should be considered:

- Will the user be able to remember the answer to the question?
- Could an attacker easily obtain this information from social media or other sources?
- Is the answer likely to be the same for a large number of users, or easily guessable?

# Using Security Questions

## When to Use Security Questions

Applications should generally use a password along with a second authentication factor (such as an OTP code) to authenticate users. The combination of a password and security questions **does not constitute MFA**, as both factors as the same (i.e, something you know).

**Security questions should never be relied upon as the sole mechanism to authenticate a user**. However, they can provide a useful additional layer of security when other stronger factors are not available. Common cases where they would be use include:

- Authenticating users.
- Resetting a forgotten password.
- Resetting a lost MFA token.

### Authentication Flow

- User enters username + password
- Ask security questions
- Login
- Consider account lockout

### Forgotten Password or Lost MFA Token Flow

- User enters email address (+CAPTCHA)
- Email random link to them
- User clicks link
- Ask security questions
- User enters new password

## How to Use Security Questions

### Storing Answers

- How to store answer (hash? encrypt?)

### Comparing Answers

Comparing the answers provided by the user with the stored answer in a case insensitive manner makes it much easier for the user. The simplest way to do this is to convert the answer to lowercase before hashing the answer to store it, and then lowercase the user-provided answer before comparing them.

It is also beneficial to give the user some indication of the format that they should use to enter answers. This could be done through input validation, or simply by recommending that the user enters their details in a specific format. For example, when asking for a date, indicating that the format should be "DD/MM/YYYY" will mean that the user doesn't have to try and guess what format they entered when registering.

# Old Contents

## Steps

### Step 1) Decide on Identity Data vs Canned Questions vs. User-Created Questions

Generally, a single HTML form should be used to collect all of the inputs to be used for later password resets.

If your organization has a business relationship with users, you probably have collected some sort of additional information from your users when they registered with your web site. Such information includes, but is not limited to:

- email address
- last name
- date of birth
- account number
- customer number
- last 4 of social security number
- zip code for address on file
- street number for address on file

For enhanced security, you may wish to consider asking the user for their email address first and then send an email that takes them to a private page that requests the other 2 (or more) identity factors. That way the email itself isn't that useful because they still have to answer a bunch of 'secret' questions after they get to the landing page.

On the other hand, if you host a web site that targets the general public, such as social networking sites, free email sites, news sites, photo sharing sites, etc., then you likely to not have this identity information and will need to use some sort of the ubiquitous "security questions". However, also be sure that you collect some means to send the password reset information to some out-of-band side-channel, such as a (different) email address, an SMS texting number, etc.

Believe it or not, there is a certain merit to allow your users to select from a set of several "canned" questions. We generally ask users to fill out the security questions as part of completing their initial user profile and often that is the very time that the user is in a hurry; they just wish to register and get about using your site. If we ask users to create their own question(s) instead, they then generally do so under some amount of duress, and thus may be more likely to come up with extremely poor questions.

However, there is also some strong rationale to requiring users to create their own question(s), or at least one such question. The prevailing legal opinion seems to be if we provide some sort of reasonable guidance to users in creating their own questions and then insist on them doing so, at least some of the potential liabilities are transferred from our organizations to the users. In such cases, if user accounts get hacked because of their weak security questions (e.g., "What is my favorite ice cream flavor?", etc.) then the thought is that they only have themselves to blame and thus our organizations are less likely to get sued.

Since OWASP recommends in the [Forgot Password Cheat Sheet](Forgot_Password_Cheat_Sheet.md) that multiple security questions should be posed to the user and successfully answered before allowing a password reset, a good practice might be to require the user to select 1 or 2 questions from a set of canned questions as well as to create (a different) one of their own and then require they answer one of their selected canned questions as well as their own question.

### Step 2) Review Any Canned Questions with Your Legal Department or Privacy Officer

While most developers would generally first review any potential questions with whatever relevant business unit, it may not occur to them to review the questions with their legal department or chief privacy officer. However, this is advisable because their may be applicable laws or regulatory / compliance issues to which the questions must adhere. For example, in the telecommunications industry, the FCC's Customer Proprietary Network Information (CPNI) regulations prohibit asking customers security questions that involve "personal information", so questions such as "In what city were you born?" are generally not allowed.

### Step 3) Insist on a Minimal Length for the Answers

Even if you pose decent security questions, because users generally dislike putting a whole lot of forethought into answering the questions, they often will just answer with something short. Answering with a short expletive is not uncommon, nor is answering with something like "xxx" or "1234". If you tell the user that they *should* answer with a phrase or sentence and tell them that there is some minimal length to an acceptable answer (say 10 or 12 characters), you generally will get answers that are somewhat more resistant to guessing.

### Step 4) Consider How To Securely Store the Questions and Answers

There are two aspects to this...storing the questions and storing the answers. Obviously, the questions must be presented to the user, so the options there are store them as plaintext or as reversible ciphertext. The answers technically do not need to be ever viewed by any human so they could be stored using a secure cryptographic hash (although in principle, I am aware of some help desks that utilize the both the questions and answers for password reset and they insist on being able to *read* the answers rather than having to type them in; YMMV). Either way, we would always recommend at least encrypting the answers rather than storing them as plaintext. This is especially true for answers to the "create your own question" type as users will sometimes pose a question that potentially has a sensitive answer (e.g., "What is my bank account \# that I share with my wife?").

So the main question is whether or not you should store the questions as plaintext or reversible ciphertext. Admittedly, we are a bit biased, but for the "create your own question" types at least, we recommend that such questions be encrypted. This is because if they are encrypted, it makes it much less likely that your company will be sued if you have some bored, rogue DBAs pursuing the DB where the security questions and answers are stored in an attempt to amuse themselves and stumble upon something sensitive or perhaps embarrassing.

In addition, if you explain to your customers that you are encrypting their questions and hashing their answers, they might feel safer about asking some questions that while potentially embarrassing, might be a bit more secure. (Use your imagination. Do we need to spell it out for you? Really???)

### Step 5) Periodically Have Your Users Review their Questions

Many companies often ask their users to update their user profiles to make sure contact information such as email addresses, street address, etc. is still up-to-date. Use that opportunity to have your users review their security questions. (Hopefully, at that time, they will be in a bit less of a rush, and may use the opportunity to select better questions.) If you had chosen to encrypt rather than hash their answers, you can also display their corresponding security answers at that time.

If you keep statistics on how many times the respective questions has been posed to someone as part of a Forgot Password flow (recommended), it would be advisable to also display that information. (For instance, if against your advice, they created a question such as "What is my favorite hobby?" and see that it had been presented 113 times and they think they might have only reset their password 5 times, it would probably be advisable to change that security question and probably their password as well.)

### Step 6) Authenticate Requests to Change Questions

Many web sites properly authenticate change password requests simply by requesting the current password along with the desired new password. If the user cannot provide the correct current password, the request to change the password is ignored. The same authentication control should be in place when changing security questions. The user should be required to provide the correct password along with their new security questions & answers. If the user cannot provide the correct password, then the request to change the security questions should be ignored. This control prevents both Cross-Site Request Forgery attacks, as well as changes made by attackers who have taken control over a users workstation or authenticated application session.

# Using Security Questions

Requiring users to answer security questions is most frequently done under two quite different scenarios:

- As a means for users to reset forgotten passwords. (See [Forgot Password Cheat Sheet](Forgot_Password_Cheat_Sheet.md).)
- As an additional means of corroborating evidence used for authentication.

If at anytime you intend for your users to answer security questions for both of these scenarios, it is *strongly* recommended that you use two different sets of questions / answers.

It should noted that using a security question / answer in addition to using passwords does ***not*** give you multi-factor authentication because both of these fall under the category of "what you know". Hence they are two of the *same* factor, which is not multi-factor. Furthermore, it should be noted that while passwords are a very weak form of authentication, answering security questions are generally is a much weaker form. This is because when we have users create passwords, we generally test the candidate password against some password complexity rules (e.g., minimal length &gt; 10 characters; must have at least one alphabetic, one numeric, and one special character; etc.); we usually do no such thing for security answers (except for perhaps some minimal length requirement). Thus good passwords generally will have much more entropy than answers to security questions, often by several orders of magnitude.

## Security Questions Used To Reset Forgotten Passwords

The [Forgot Password Cheat Sheet](Forgot_Password_Cheat_Sheet.md) already details pretty much everything that you need to know as a developer when *collecting* answers to security questions. However, it provides no guidance about how to assist the user in selecting security questions (if chosen from a list of candidate questions) or writing their own security questions / answers. Indeed, the [Forgot Password Cheat Sheet](Forgot_Password_Cheat_Sheet.md) makes the assumption that one can actually use additional *identity* data as the security questions / answers. However, often this is not the case as the user has never (or won't) volunteer it or is it prohibited for compliance reasons with certain regulations (e.g., as in the case of telecommunications companies and [CPNI](https://en.wikipedia.org/wiki/Customer_proprietary_network_information) data).

Therefore, at least some development teams will be faced with collecting more generic security questions and answers from their users. If you must do this as a developer, it is good practice to:

- briefly describe the importance of selecting a good security question / answer.
- provide some guidance, along with some examples, of what constitutes bad vs. fair security questions.

You may wish to refer your users to the [Good Security Questions](http://goodsecurityquestions.com/) web site for the latter.

Furthermore, since adversaries will try the "forgot password" reset flow to reset a user's password (especially if they have compromised the side-channel, such as user's email account or their mobile device where they receive SMS text messages), is a good practice to minimize unintended and unauthorized information disclosure of the security questions. This may mean that you require the user to answer one security question before displaying any subsequent questions to be answered. In this manner, it does not allow an adversary an opportunity to research all the questions at once. Note however that this is contrary to the advice given on the [Forgot Password Cheat Sheet](Forgot_Password_Cheat_Sheet.md) and it may also be perceived as not being user-friendly by your sponsoring business unit, so again YMMV.

Lastly, you should consider whether or not you should treat the security questions that a user will type in as a "password" type or simply as regular "text" input. The former can prevent shoulder-surfing attacks, but also cause more typos, so there is a trade-off. Perhaps the best advice is to give the user a choice; hide the text by treating it as "password" input type by default, but all the user to check a box that would display their security answers as clear text when checked.

## Security Questions As An Additional Means Of Authenticating

First, it bears repeating again...if passwords are considered weak authentication, then using security questions are even less robust. Furthermore, they are no substitute for true multi-factor authentication, or stronger forms of authentication such as authentication using one-time passwords or involving side-channel communications. In a word, very little is gained by using security questions in this context. But, if you must...keep these things in mind:

- Display the security question(s) on a separate page only *after* your users have successfully authenticated with their usernames / passwords (rather than only after they have entered their username). In this manner, you at least do not allow an adversary to view and research the security questions unless they also know the user's current password.
- If you also use security questions to reset a user's password, then you should use a *different* set of security questions for an additional means of authenticating.
- Security questions used for actual authentication purposes should regularly expire much like passwords. Periodically make the user choose new security questions and answers.
- If you use answers to security questions as a *subsequent* authentication mechanism (say to enter a more sensitive area of your web site), make sure that you keep the session idle time out very low...say less than 5 minutes or so, or that you also require the user to first re-authenticate with their password and then immediately after answer the security question(s).

# Related Articles

- [Forgot Password Cheat Sheet](Forgot_Password_Cheat_Sheet.md)
- [Good Security Questions web site](http://goodsecurityquestions.com/)
