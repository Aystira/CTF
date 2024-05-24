# Correlation One DoD May 2024 CTF
by Aystira
5/24/2024

On May 18, 2024 Cyber Sentinel in collaboration with the DoD hosted a Capture the Flag (CTF) Competition for aspiring and veteran cybersecurity professionals.
This was my first ever official CTF and I had a great experience overall.  I was only able to answer 4 out of the 21 questions but was overall happy with how I did based on the difficulty.  While the challenge said it was for beginners, I believe that the challenges were definitely not at the beginner level.  This document is my writeup of how I did in the CTF and the documenetation of the steps I took to obtain the flags in the questions that I answered.

## Have you bean here before? - Easy (150p)
This first question was an easy question to test your OSINT skills.  The flag originally was the first 6 symbols in the MAC Address of the guest wifi, but because the OSINT source to obtain the MAC Address was having issues due to the number of requests, the moderators for the CTF updated the challenge to allow for the address of the location to be input as the flag.

<img src="https://github.com/Aystira/CTF/assets/67524880/cec5a0f2-d70b-4cdd-8cfc-a7be879f3552"/>

### Solution
In the picture two things stood out immediately to me.  First was the cup with the name PAUL on it.  A quick google search revealed the cup with PAUL to be a logo for the 'PAUL - French Bakery & Cafe'. Second, a street sign could be seen in the background, and while not the clearest, when zoomed in, I could just make out 13, and knowing that the location was in DC, I could reasonably assume that this bakery was located on or near 13th St.  Back to my google search I found the website for 'PAUL - French Bakery & Cafe' (www.pauldmv.com), and went to the locations tab where I found 2 locations in DC, one on 2000 Pennsylvania Ave NW and the other on 1275 K St NW.  Checking google maps and verifying the location of both addresses vs 13th St, I was able to confirm the location where the picture was taken was from the bakery on 1275 K St NW.

FLAG: C1{1275}

### Takeaway
I struggled a lot with the original flag due to not knowing how to obtain the MAC Address for a device I did not have access to.  I spent a lot of time using nmap to attempt to ping the website and try to obtain a MAC address but was unsuccessful.  I did learn later that a site called https://wigle.net is available as an open source intelligence tool for identifying wifi networks.  Playing around with it on another day, I was able to obtain the MAC Address for 'PAUL - French Bakery & Cafe'.

FLAG: C1{6C:CD:D6}
