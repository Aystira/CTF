# DoD Cyber Sentinel Skills May 2024 CTF
By Aystira\
5/24/2024


On May 18, 2024 Cyber Sentinel in collaboration with the DoD hosted a Capture the Flag (CTF) Competition for aspiring and veteran cybersecurity professionals. This was my first ever official CTF and I had a great experience overall.  I was only able to answer 4 out of the 21 questions but was overall happy with how I did based on the difficulty.  While the challenge said it was for beginners, I believe that the challenges were definitely not at the beginner level.  This document is my writeup of how I did in the CTF and the documenetation of the steps I took to obtain the flags in the questions that I answered.

## Have you bean here before? - Easy (150p)
This first question was an easy question to test your OSINT skills.  The flag originally was the first 6 symbols in the MAC Address of the guest wifi, but because the OSINT source to obtain the MAC Address was having issues due to the number of requests, the moderators for the CTF updated the challenge to allow for the address of the location to be input as the flag.

<img src="https://github.com/Aystira/CTF/assets/67524880/cec5a0f2-d70b-4cdd-8cfc-a7be879f3552"/>

### Solution
In the picture two things stood out immediately to me.  First was the cup with the name PAUL on it.  A quick google search revealed the cup with PAUL to be a logo for the 'PAUL - French Bakery & Cafe'. Second, a street sign could be seen in the background, and while not the clearest, when zoomed in, I could just make out 13, and knowing that the location was in DC, I could reasonably assume that this bakery was located on or near 13th St.  Back to my google search I found the website for 'PAUL - French Bakery & Cafe' (www.pauldmv.com), and went to the locations tab where I found 2 locations in DC, one on 2000 Pennsylvania Ave NW and the other on 1275 K St NW.  Checking google maps and verifying the location of both addresses vs 13th St, I was able to confirm the location where the picture was taken was from the bakery on 1275 K St NW.

FLAG: C1{1275}

### Takeaway
I struggled a lot with the original flag due to not knowing how to obtain the MAC Address for a device I did not have access to.  I spent a lot of time using nmap to attempt to ping the website and try to obtain a MAC address but was unsuccessful.  I did learn later that a site called https://wigle.net is available as an open source intelligence tool for identifying wifi networks.  Playing around with it on another day, I was able to obtain the MAC Address for 'PAUL - French Bakery & Cafe'.

FLAG: C1{6C:CD:D6}

## Exfil - Medium (200p)
This question was an interesting question about analyzing a pcap file.  

### Solution
Seeing that the file provided was a pcap, I opened the file in wireshark.  When I opened the pcap, I immediately went to see what type of packets were in the pcap.  This revealed that all packets in the pcap file were dns packets.  I then looked at the packets and noticed dns queries to the subdomain data.exfiltrated.com. The string before the subdomain also was suspicious as it looked to be encoded text. I filtered the information in the pcap to have only the outgoing query packets and saved the results as a csv.  I then modified the csv in terminal to remove all unnecessary data leaving only the encoded text.  I then copied the encoded text into [CyberChef](https://gchq.github.io/CyberChef/).  I used CyberChef to remove the carriage returns and decode the message revealing a picture with the flag.

FLAG: C1{dns_3xfil7r4t3d!}

### Takeaway
Analyzing the pcap file in this challenge was a good refresher on Wireshark and seeing the DNS exfiltration method was fascinating.  I learned how to modify csv files in the terminal to remove columns, making it much easier to collect only the data I needed from the pcap before putting it into CyberChef.  There were definitely better methods to solve this challenge that I will have to look into.  tshark seems to have been the best option to quickly extract the necessary data. Overall a fun challenge.

## Ephemeral - Easy (150p)
This challenge was completely online with the flag located on a webpage hosted on a specific IP provided.  The challenge specified that the information was not on a regularly used port.

### Solution
Once the organizers specified that this was not on a regular port, this clearly meant that we had to do a full port scan on the IP provided. Nmap was an easy choice, but I did run into a minor pitfall where an nmap scan showed the IP being unavailable but was easily able to get around that.  I modified my command to assume that the IP was available and it revealed that TCP port 51147 was open.  I then went to the site by putting in the IP:51147 which contained the flag.

FLAG: C1{ch3ck_4ll_p0rts!}

### Takeaway
Very simple challenge, and good nmap practice.

## Important Document - Medium (200p)
This challenge contained an html document that was attempting to phish for credentials by masquerading as an excel sheet that required logging in to view.  To me, this challenge was a lot simpler than it seemed. (I actually forgot about this challenge completely.)

### Solution
I first opened the html to see what I was dealing with, not the smartest idea but it was in Kali so I wasn't too worried.  Seeing nothing of relevance, I then opened the file in zsh to see the html code by using the cat command on the file.  The command spit out a long wall of text that included some obfuscated code.  I first looked at the base64 encoded lines and put them into cyberchef.  Unencoding the lines revealed them to be the images for the excel login form.  I then looked at the binary code that had also appeared when I used the cat command. 

![image](https://github.com/Aystira/DoD-Cyber-Sentinels-Skills-Challenge-May-2024-CTF/assets/67524880/84f05581-4f23-4c2e-998a-a105e22a81b0)

I manually added the From Binary operation which revealed a function along with a bunch of other code.  Inside of this code included the url hxxps[://]badguys[.]c1[/]lol (haha) and after it was a small encoded string. I copied the string and put it into Cyberchef, which I then decoded from base64.  Cyberchef then recommended decode from Hex which revealed the flag.

![image](https://github.com/Aystira/DoD-Cyber-Sentinels-Skills-Challenge-May-2024-CTF/assets/67524880/f67133f8-09c5-41cc-881a-aa50dea19eb2)

FLAG: C1{h0p3_y0u_d1dnt_us3_4_r431_p4ssw0rd}

### Takeaway
Document while doing the challenge rather than after.

## Conclusion
Overall I found this CTF to be a very fun experience and I definitely hope to do more of them.  Some things to take away from this is definitely document as I am doing the challenge rather than trying to remember post event.  Also take screenshots.  Like I said earlier, based on the difficulty, I am very happy with answering 4 out of the 21 questions, and actually placing 270th out of over 5000 individuals who signed up.  The next time I do a CTF I hope to be able do better and complete more challenges.
