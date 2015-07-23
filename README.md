<h1>Rust Ssmtp</h1>
Rust sending emails via ssmtp

This is the beginning stages of this repo and I am a Rust newbie. Please provide suggestions or corrections. Currently there is no working method (that I am aware of) to send emails with Rust. So I made rust-ssmtp.


The requirements for Rust Ssmtp:
<ol>
  <li>Linux/OSX</li>
  <li>ssmtp</li>
</ol>


\* Note: These instructions assume a Ubuntu machine and the use of a gmail account. You can yous any smtp ready email account.


<h2>Step One</h2>
<h3>Install ssmtp and configure</h3>

Run Commands:
```
apt-get -y install ssmtp
nano /etc/ssmtp/ssmtp.conf
```

Edit/Add the Follwing Lines:
```
root=your.account@gmail.com
mailhub=smtp.gmail.com:587
FromLineOverride=YES
UseSTARTTLS=YES
AuthUser=your.account
AuthPass=password
AuthMethod=LOGIN
```


\* Note: Special charecters such as symbols will not work. Also dispable two step authentication.

Test Commands:
 ```
ssmtp your.account@gmail.com
Subject: Hello
I am the body. World!
```


<h2>Step Two</h2>
<h3>Create Main.rs File</h3>

```
extern crate ssmtp;
use ssmtp::email;

fn main() {

    // Configure email body and header
    email::create(
        // From Address
        "from.email@example.com",
        // To Address
        "to.email@example.com",
        // Subject
        "Subject - Hello World!",
        // Body
        "<html><body><h1>I am the body. Hello Wolrd!<br/><br/>And I accept html.</h1></body></html>"
    );

    // Define the actual email address to receive the email
    email::send("your.email@gmail.com");
}
```
