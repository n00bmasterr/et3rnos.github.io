---
title: TG:HACK 2020 – s2s messaging Writeup
category: hacking
tags: ctf-writeup
---

> Intercepted ship to ship communication. Can you find the message?

This challenge also gives us a pcapng file.

Pcapng are generated by Wireshark and contain a history of packets sent and received by computers.

So, let’s start Wireshark to analyze the file. We go to Statistics -> Conversations and then we select the TCP tab to list all TCP connections.

![Output](/images/tghship1.png)

We realize there is a particular interesting connection listed: the one where 1017000 bytes were sent and 48000 were received.

Probably it is some kind of file transference.

So, go ahead: select it and click Follow Stream… button in order to inspect the connection more closely.

![Output](/images/tghship2.png)

We notice the data parameter stores a base64 string (because of / and + characters), so we will try to decode it:

```
echo "your_base_64_encoded_string" | base64 -d
```

The output is something illegible, but at the beginning you see that there is a PNG string, so our output is probably a png file.

Knowing this, you just need to decode the string again and save the results into a png file:

```
echo "your_base_64_encoded_string" | base64 -d > image.png
```

Then just open it normally and you will get the flag:

![Output](/images/tghship3.png)

This challenge was solved by my team, [ducks0ci3ty](https://ctftime.org/team/114402).