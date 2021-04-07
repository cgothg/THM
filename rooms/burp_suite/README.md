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

