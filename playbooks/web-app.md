# Web App

# Gatherin information 
- Look up company and leadership
- looks shodan
- dns lookup
- dark web

# If an ip
- nmap scan
- see what ports are open
- banner grabbing
- why is ssh not secure
    - normally don't have password
- ftp & telnet not secure no encryption

# One Web App page
- look for anything insecure 
- burpsuite
- look at the request
- anything in the url

# login page
- are they returning anything on the backend
- exposed buckets
- collect the api endpoints

# Check
- look for policy policy they have

# how to find the user name
- find the names in the recon from the beginning

# Do the password spraying
- look if the user name and pay
- look for errors to do user  enumeration for free
- is the username being validated on the backend

# password is accepted, you are now a user
- ssti's

# have the reverse shell. how do you go from user to root
- find what system you are on

# have root / how do you go from your kali to the linux
- bloodhound or powershell
    - requirement: need active credentials

# How do you get credentials
- Kerb root

# Bloodhound
- want to see account with security access
- AD and Bloodhound won't tell you who has access to what

# Find who has access to what
- 

# Why is MIME cats so loud
- It touches a process calles Lsass

**RCE**
**OWASP Top 10**

---***With Tom N***---

**Cross site scripting**
- api response
- on login page
- does it 
- is there sql injections
    - run a sql map
- Check parameters
    - observe what is happening during the login process
        - what does it do
        - how does it do it
        - what can we do to manipulate it
            - can we put in bogus json
            - can we change the hostname

see a successful login with a username and password
jwt
- make sure theree is no cruddy seed for the jwt

with sparying you need to know
- number of users
- that the users exist
- the lockout mechanism

--
what is the difference between jwt & base64

What is cross-site scripting

2 types of cross-site scripting
- reflected
- scripted

--- 

How do you perform SQL injection
- Usually admin is the first user in table