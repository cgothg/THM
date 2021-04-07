# Notes for the room Burp Suite (https://tryhackme.com/room/rpburpsuite). Part of the "Complete Beginner Path"

## Installation 

Will not go through the installation process since Kali Linux ships with Burp Suite. The setup of Burp Suite is descriped nicely in the room.

## Questions and answers:

### Task 6:

By default, the Burp Suite proxy listens on only one interface. What is it? Use the format of IP:PORT

```
127.0.0.1:8080
```

Return to your web browser and navigate to the web application hosted on the VM we deployed just a bit ago. Note that the page appears to be continuously loading. Change back to Burp Suite, we now have a request that's waiting in our intercept tab. Take a look at the actions, which shortcut allows us to forward the request to Repeater?

```
ctrl-r
```

How about if we wanted to forward our request to Intruder?

```
ctrl-i
```

Burp Suite saves the history of requests sent through the proxy along with their varying details. This can be especially useful when we need to have proof of our actions throughout a penetration test or we want to modify and resend a request we sent a while back. What is the name of the first section wherein general web requests (GET/POST) are saved?

```
HTTP History
```

Defined in RFC 6455 as a low-latency communication protocol that doesn't require HTTP encapsulation, what is the name of the second section of our saved history in Burp Suite? These are commonly used in collaborate application which require real-time updates (Google Docs is an excellent example here).

```
WebSockets history
```

Before we move onto exploring our target definition, let's take a look at some of the advanced customization we can utilize in the Burp proxy. Move over to the Options section of the Proxy tab and scroll down to Intercept Client Requests. Here we can apply further fine-grained rules to define which requests we would like to intercept. Perhaps the most useful out of the default rules is our only AND rule. What is it's match type?


```
URL
```

How about it's 'Relationship'? In this situation, enabling this match rule can be incredibly useful following target definition as we can effectively leave intercept on permanently (unless we need to navigate without intercept) as it won't disturb sites which are outside of our scope - something which is particularly nice if we need to Google something in the same browser.

```
Is in target scope
```

### Task 7:


Browse around the rest of the application to build out our page structure in the target tab. Once you've visited most of the pages of the site return to Burp Suite and expand the various levels of the application directory. What do we call this representation of the collective web application?

```
Site map
```

What is the term for browsing the application as a normal user prior to examining it further?

```
Happy Path
```

The issue definitions found here are how Burp Suite defines issues within reporting. While getting started, these issue definitions can be particularly helpful for understanding and categorizing various findings we might have. Which poisoning issue arises when an application behind a cache process input that is not included in the cache key?

```
Web cache poisoning
```

### Task 8:

Try logging in with invalid credentials. What error is generated when login fails?

```
Invalid email or password.
```

Now that we've sent the request to Repeater, let's try adjusting the request such that we are sending a single quote (') as both the email and password. What error is generated from this request?

```
SQLITE_ERROR
```

What field do we have to modify in order to submit a zero-star review?

```
Rating
```

### Task 9:

Which attack type allows us to select multiple payload sets (one per position) and iterate through them simultaneously?

```
Pitchfork
```
How about the attack type which allows us to use one payload set in every single position we've selected simultaneously?

```
Battering Ram
```

Which attack type allows us to select multiple payload sets (one per position) and iterate through all possible combinations?

```
Cluster Bomb
```

Perhaps the most commonly used, which attack type allows us to cycle through our payload set, putting the next available payload in each position in turn?

```
Sniper
```

Finally, click 'Start attack'. What is the first payload that returns a 200 status code, showing that we have successfully bypassed authentication?

```
a' or 1=1--
```

### Task 10

Parse through the results. What is the effective estimated entropy measured in?

```
bits
```

In order to find the usable bits of entropy we often have to make some adjustments to have a normalized dataset. What item is converted in this process?

```
token
```
