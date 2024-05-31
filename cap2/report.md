## Bug Bounty
 ### Introduction

Cyber risks have become more rampant, therefore making it evident that there is the need for better measures in the protection of websites. In an effort to safeguard their information, organizations have adopted the use of bug bounty programs as a way of preventing potential threats. This paper outlines the steps that were taken during a bug bounty program where the focus was to identify vulnerabilities in a given website

It was our intention to perform a security audit of the given website, utilizing a range of testing approaches in order to identify any potential openings that could be exploited by attackers. The assessment focused on general vulnerabilities of web applications which can be listed as SQL injection, Cross Site Scripting (XSS), Cross Site Request Forgery (CSRF), and server misconfiguration.

We also intended to not only map out the system’s security flaws but also propose measures to address the issues that have been raised. This report also includes details about the approaches that we have used during the testing, the vulnerabilities that we have discovered, their possible consequences and recommendations for their solutions. This study highlights the importance of practising security testing as a continuous process to secure web applications .

### 1. Hack this site

**Challenges from Basic challenges**

- LEVEL 1

In this first level also known as “the idiot test ” where we were assigned to find the password to complete the level.

![Alt text](<hack this site/1/Screenshot 2567-05-28 at 10.07.34 PM.png>)

So to complete this level we need to inspect the page where we will be directed to the HTML code for this page where the password was imbedded as comment.

![Alt text](<hack this site/1/Screenshot 2567-05-28 at 10.06.51 PM.png>)

So the password was 28e47fb8as we can see that it was above the a password field.

- LEVEL 2

In this level we were asked to find a password for Sam who is a Network securities. So Sam set up a password protection script. He made it load the real password from an unencrypted text file and compare it to the password the user enters. However, he neglected to upload the password file. So to clear this level can directly hit the submit button since he neglected to upload the password file

![Alt text](<hack this site/2/Screenshot 2567-05-28 at 10.08.04 PM.png>)

- LEVEL 3

In this level we were asked to find the password where but with a different condition where we can see in the problem statement that Sam this uploaded the file but came across a different problem.

![Alt text](<hack this site/3/Screenshot 2567-05-28 at 10.12.01 PM.png>)

Same as the earlier problem I inspected the webpage and navigated myself to the password field and where I found that in the input field the values “password.php” was hidden from the page.

![Alt text](<hack this site/3/Screenshot 2567-05-28 at 10.12.16 PM.png>)

So I tried to navigate to that page in the url section and tried to put the endpoint as “/password.php”

![Alt text](<hack this site/3/Screenshot 2567-05-28 at 10.12.51 PM.png>)

After entering the endpoint I was directed to a page where I was able to find the password for this problem.

![Alt text](<hack this site/3/Screenshot 2567-05-28 at 10.13.03 PM.png>)

- LEVEL 4

This time Sam hardcored and bad for him being a forgetful person he wrote a script to send a password to his mail.

![Alt text](<hack this site/4/Screenshot 2567-05-28 at 10.15.26 PM.png>)

So to get the password I again inspected this page and navigated to the mail field where I could see this Email.

![Alt text](<hack this site/4/Screenshot 2567-05-28 at 10.16.26 PM.png>)

I changed his password with mine in that field so that the mail could come to my mail instead of his.

![Alt text](<hack this site/4/Screenshot 2567-05-28 at 10.17.03 PM.png>)

After this I requested for the password and different page indicating that the mail was sent to my mail

![Alt text](<hack this site/4/Screenshot 2567-05-28 at 10.17.18 PM.png>)

I checked my mail and boom the password was sent to my mail.
![Alt text](<hack this site/4/Screenshot 2567-05-28 at 10.17.53 PM.png>)

- LEVEL 5

In this level again we were given same problem as that with Level 4 and I did the same for all.

![Alt text](<hack this site/5/Screenshot 2567-05-31 at 2.30.46 AM.png>)

Replaced my mail with Sam’s

![Alt text](<hack this site/5/Screenshot 2567-05-31 at 2.31.34 AM.png>)
![Alt text](<hack this site/5/Screenshot 2567-05-31 at 2.32.00 AM.png>)

And yet again the password was sent to my mail.

![Alt text](<hack this site/5/Screenshot 2567-05-31 at 2.34.30 AM.png>)

- LEVEL 6

Here the password was encrypted and the task to decrypted it

![Alt text](<hack this site/6/Screenshot 2567-05-30 at 9.21.05 PM.png>)

So to decrypt the password that was given we had to know the pattern in which this password was getting encrypted so I tried to figure it out with some examples Where I tried encrypting “1234” and an output shown below.

![Alt text](<hack this site/6/Screenshot 2567-05-30 at 9.21.19 PM.png>)

With this I could see that the password is a pattern where the number is getting incremented to the the number of its position like the first number being 1 gets added to this position number which is 0 and 2 is getting incremented with its position number which is 1 and the output is 3 and the same for all. For the special characters I used an ASCII table to know the pattern for it.

![Alt text](<hack this site/6/Screenshot 2567-05-30 at 9.17.54 PM.png>)
So with this the password was 626f3a45

---


### 2. URL 2. 10.3.21.141:8008
#### Vulnerability 1 : XSS: Cross-site Scripting

Cross Site Scripting (XSS) is a security vulnerability often discovered in web applications. It happens when a hacker manages to insert malicious scripts into content that gets sent to a user's browser. The main goal of XSS is to run scripts, within the users session on the website, which could result in actions taking place. This occurs when malicious input submitted by an attacker is stored on the server, such as in a database, comment field, or forum post. When a user retrieves the stored data, the malicious script is executed in their browser.

**consequences**

A web application that has an XSS (Cross-Site Scripting) vulnerability can have many serious outcomes, which affect the users as well as the owning organization itself. Here are a number of key consequences
- User Information: Attackers can steal personal user data, such as users’ names, passwords, email addresses and other personal information.
- Session Cookies: They can take their session cookie who will then intrude into user’s sessions thus pretending to be those users.
- User Accounts: By stealing session cookies or login credentials, attackers can gain unauthorized access to user accounts, potentially leading to identity theft and unauthorized actions.

**Steps to reproduce**

Once I was logged into the website there was a option to add a new snippet where a user can add their snippets.

![Alt text](<Gruyere/XSS/Screenshot 2567-05-31 at 1.03.14 PM.png>)

So in this section we can add snippets in the form of html where we can also add Javascript for some functionality to happen when a user interacts with it. So basic functionality of javascript is the “alert” where a user will get an alert message.

![Alt text](<Gruyere/XSS/Screenshot 2567-05-31 at 1.01.19 PM.png>)

Upon adding this snippet when the user hover over this they will come across this type of message. And likewise we can add harmful and malicious scripts like this. And indicating that this site has an XSS vulnerability.

![Alt text](<Gruyere/XSS/Screenshot 2567-05-31 at 1.19.08 PM.png>)

So in the image below that we can see that we have a upload section where the user can add malicious file for XSS


![Alt text](<Gruyere/XSS/Screenshot 2567-05-30 at 12.40.00 PM.png>)

In this i have added index.html file to conduct a XSS so when the user login in and somehow manageto click the link they would be directed to a another html page.

![Alt text](<Gruyere/XSS/Screenshot 2567-05-30 at 12.40.21 PM.png>)

After adding the index.html file i was given a url where the html file would be stored. but in place of the given IP address we have subtitude by 10.3.21.141

![Alt text](<Gruyere/XSS/Screenshot 2567-05-30 at 12.40.44 PM.png>)

So when we go to that link we will be seeing the the file being executed. 

![Alt text](<Gruyere/XSS/Screenshot 2567-05-30 at 12.41.00 PM.png>)

**Vulnerability 2 Privilege Escalation**

Privilege Escalation also known as Elevation of Privilege usually referred to as privilege escalation is a class of security vulnerability wherein an attacker gains illicit entry into higher privileges or permissions than what was assigned initially. The attacker can then misuse this to carry out inappropriate activities such as accessing data that is not supposed to access.

**How this vulnerability works**

The most common form of attack is elevation of privilege, which is initiated when an attacker follows a sequence of activities such as reconnaissance, where the attacker acquires information regarding the target system, including its weaknesses or faults. Once enough information has been gathered, the attacker enters the first phase of an attack, typically by gaining the initial foot-hold that is usually accomplished by either phishing email, finding a vulnerability in the target’s software, or using a stolen username and password. In the second phase, the attacker proceeds to discovery and enumeration where the system is identified and relevant accounts, services, and possibilities for escalation of privileges are searched for. The next step is to take advantage of these vulnerabilities, which may involve running a scan to attempt to get code to execute or using a Nessus scan to check for open shares, unpatched software, default passwords, and the sharing of directories that were not supposed to be shared; using phishing attacks to obtain root, or higher, privileges. Seizing on these vulnerabilities empowers the attacker to gain higher permissions: to read and/or write private information, change program settings or configuration, print or delete something without having permissions, and even to infect the PC with a virus and thus, take full control over the system. Measures such as patching, keeping user privileges low, and authentication should also be in place to avoid experiencing such attacks while monitoring for any activities that look suspicious.

**What are the consequences**

As mentioned, the impact of an elevation of privilege attack can be devastating on the targeted entity or system. When an attacker achieves root/administrator level they can read, change or delete the information of an organization such as personal data, financial data or other business data thus breaching company’s data and possibly incurring the law’s wrath for neglecting to protect the data. Furthermore, when an attacker gains privileges to a system, he or she can change configurations, delete or manipulate files and data, and introduce malware or ransomware programs that interrupt business operations and result in costly consequences. They can as well develop other means which they use to compromise the system for future accesses once compromised, meaning the system can hardly be fully protected even if the initial threat is identified. It is equally important to note that the reputation of the organization gets compromised with customer trust and definite business venturing. Also, there can be legal consequences where the entity is faced with regulatory fines for the violation of data protection laws. All in all, the increased awareness of such an attack highlights the need to enhance security features to discourage privilege escalation.

**Steps to reproduce**

Right after creating the account i was just logged in as a user but this website being vulnerable i can convert myself to an administrator or a admin.

![Alt text](<Gruyere/privilege escalation/Screenshot 2567-05-31 at 3.09.34 PM.png>)

When i go to my profile section I was only able to edit my profile

![Alt text](<Gruyere/XSS/Screenshot 2567-05-30 at 6.15.33 PM.png>)

To get the admin privilege or access in url we just need to put the update and is_admin to true in which our url will look something like this: **"10.3.21.141:8008/471541268652354669237873339020654786900 /saveprofile?action=update&is_admin=True"**.

![Alt text](<Gruyere/privilege escalation/Screenshot 2567-05-31 at 3.25.31 PM.png>)

After going to that page we will not see much difference and we will directed to the home page itself. But after signing out and sign in again is where we will see that we have got the admin access.

![Alt text](<Gruyere/privilege escalation/Screenshot 2567-05-31 at 3.36.19 PM.png>)

As we can see that I'm now the admin and I can edit any user profile and even change their password and usernames.

![Alt text](<Gruyere/privilege escalation/Screenshot 2567-05-31 at 3.36.27 PM.png>)

#### Vulnerability 2: Path Traversal

Path traversal commonly referred to as directory traversal is a security weakness that lets an attacker transcend into directories as well as files that aren’t in the authorized directory. The possibility exists that the end-in-file-name character manips can say “dot-dot-slash (. . /)” to find his way outside the target directory and into other files and directories that should not be accessible to attackers; this includes others such as system configuration files, users’ inputs and other critical system files.

**Consequences**

The impact of path traversal attack can be severe since it grants the attack permission to download any files or directories apart from any that are within the confined application. This gives unauthorized persons an opportunity to corrupt, manipulate, or modify important data including Passwords, Configuration files and other Personal data, leading to major loss of data and privacy. Also, this access can be used by the attackers for stealing important information, using intellectual property losses With it, and financial losses. Moreover, it also provides the attacker a complete control on the critical system files and the ability to change System configurations, an opportunity to privilege escalation or even to install other malicious software, which in turn make the entire system vulnerable. They not only lead to leakage of important information but also bring about negative impacts such as reputation loss, decreased customer confidence and legal actions against the organization for neglecting the task of safeguarding the data. Altogether, the path traversal vulnerabilities could be considered as critical since they expose systems and information to risk of unauthorized access and tampering.

**Steps to reproduce**

This attack is solely based to demonstrate how path traversal is a way to exploit the vulnerability. So in path traversal to find the hidden file we make use of the ../ where our browser will look like: http://10.3.21.141:8008/4715412686523546692378733390206547 86900/../secret.txt

but browsers like chrome and firefox don't allow this type of commands in the url To bypass we can make use of “ %2f” which is represents “../”. http://10.3.21.141:8008/4715412686523546692378733390206547 86900/..%2fsecret.txt

![Alt text](<Gruyere/path traversal/Screenshot 2567-05-31 at 4.11.53 PM.png>)
![Alt text](<Gruyere/path traversal/Screenshot 2567-05-31 at 4.12.09 PM.png>)

#### URL 1: 10.3.21.141:8000
**Vulnerability 1: XSS Cross-site scripting**

Same as the previous website, this one also has an XSS vulnerability. Cross Site Scripting (XSS) is a security vulnerability often discovered in web applications. It happens when a hacker manages to insert malicious scripts into content that gets sent to a user's browser. The main goal of XSS is to run scripts, within the users session on the website, which could result in actions taking place.
This occurs when malicious input submitted by an attacker is stored on the server, such as in a database, comment field, or forum post. When a user retrieves the stored data, the malicious script is executed in their browser.

**consequences**

A web application that has an XSS (Cross-Site Scripting) vulnerability can have many serious outcomes, which affect the users as well as the owning organization itself. Here are a number of key consequences
- User Information: Attackers can steal personal user data, such as users’ names, passwords, email addresses and other personal information.
- Session Cookies: They can take their session cookie who will then intrude into user’s sessions thus pretending to be those users.
- User Accounts: By stealing session cookies or login credentials, attackers can gain unauthorized access to user accounts, potentially leading to identity theft and unauthorized actions.

**Steps to reproduce**

In this site as well we encountered an XSS vulnerability where we can enter malicious html or javascript files. In this as you can see that i'm again adding a script.

![Alt text](<pixi/Screenshot 2567-05-30 at 8.05.10 PM.png>)

So whenever the user tries to get into this page they will see this message pop up

![Alt text](<pixi/Screenshot 2567-05-30 at 8.03.21 PM.png>)

#### Remediation Summary

As a consequence of this assessment, there are several measures that may need to be taken to enhance the security of this website before going live on the internet. It may therefore be worthy to note that remediation efforts are as follows;

1. Cross site scripting
- Input Validation: The inputs from the user should undergo some checks to ensure that they are in the proper format of the system. Eliminate all inputs with at least one value that could be considered a security threat.

- Output Encoding: Sanitize the outputs of Encode to avoid running scripts included in the HTML tags in the browser.

- Content Security Policy (CSP): To mitigate these security risks, it is recommended to enable Content Security Policy (CSP) to limit the origin from where scripts can be loaded and executed.

- Sanitization Libraries: Input sanitizing libraries to be used are the OWASP Java Encoder or the DOMPurify for JavaScript.

2. Privilege escalation
- Least Privilege Principle: Minimize the use of privilege in users and processes to just enough to enable them perform their function.

- Access Controls: Regularly review user and process privilege levels, and ensure only authorized users and processes have access to the associated resources.

- Authentication Mechanisms: Mitigate weak authentication controls, and enhance Password and Authentication controls through the implementation of Multi Factor Authentication for sensitive accounts.

- Regular Audits: Auditing the user privileges and the frequency with which the users use the privileged accounts will help in solving the problem of unauthorized privilege escalation.

3. Path traversal
- Input Validation: This is to check if the various inputs that the application has concerning the file system contain path traversal strings like . .. /.
- Canonicalization: Migration rules allow comparing the file locations based on the canonical paths and keeping all the files within the directory.
- Access Controls: To avoid such incidents, it is advisable that specific measures such as access control must be put in place to prohibit unauthorised file access.
- Error Handling: OS developers should refrain from revealing a file system’s structure to users in error messages.
