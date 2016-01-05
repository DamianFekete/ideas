[Source: https://www.eecs.umich.edu/courses/eecs588/readings.html](https://www.eecs.umich.edu/courses/eecs588/readings.html "Permalink to EECS 588 - Reading List")

# EECS 588 - Reading List

# [Computer & Network Security][1]

## EECS 588 – Winter 2015

[Overview][1][Schedule][2][Readings][3][Attack Presentations][4][Course Project][5]

## Readings

### Paper Response Guidelines

Write a ~400 word critical response to **each** required paper.
* In the first paragraph:
    1. State the problem that the paper tries to solve; and
    2. Summarize the main contributions.
* In one or more additional paragraphs:
    1. Evaluate the paper's strengths _and_ weaknesses;
    2. Discuss something you would have done differently if you had written the paper; and
    3. Suggest one or more interesting open problems on related topics.

Your most important task is to demonstrate that you've **read the paper** and **thought carefully** about the topic.

Paper responses are due before the start of class via the [**online submission system**][6]. Before you upload your work, the system will ask you to assess earlier responses written by your peers. We'll combine peer feedback and our own evaluation when determining your grade.

### Reading List

This list is subject to change. Updates will be posted by the end of the day on the Friday before each lecture.

[Unfortunately][7], some articles require paid subscriptions to journals and digital libraries. You can access these for free when connecting on campus. For off-campus access, try the [U-M VPN][8] or the [MLibrary Proxy Server Bookmarklet][9].

## Welcome / Essential Crypto

###  Tuesday, January 13

* [Introduction][10]. (Slides from lecture.)
* [The Security Mindset][11]. Bruce Schneier. 2008\.
* [Security Engineering][12]. Ross Anderson. Wiley, 2001.
* [Handbook of Applied Cryptography][13]. Menezes, van Oorschot, and Vanstone. CRC Press, 1996.

###  Thursday, January 15

* [Essential Cryptography][14]. (Slides from lecture.)
* [TLS and SSL][15]. D. Koren, et al. Secure Networking Protocols Portal, 2009.
* [TLS v1.2][16]. Dierks and Rescorla. RFC 5246, 2008.
* [The First Few Milliseconds of an HTTPS Connection][17]. Jeff Moser. 2009\.
* [StartSSL][18]. (CA providing free certs.)
* [Let's Encrypt][19]. (the CA Alex is building).

## How Crypto Fails

###  Tuesday, January 20

* [MD5 To Be Considered Harmful Someday][20]. Dan Kaminsky. 2004\.
* [MD5 Considered Harmful Today][21]. Sotirov, Stevens, Appelbaum, Lenstra, Molnar, Osvik, and Weger. CCC 2008\.
* [How to Break MD5 and Other Hash Functions][22]. Wang and Yu. Eurocrypt 2005.
* [Short Chosen-Prefix Collisions for MD5 and the Creation of a Rogue CA Certificate][23]. Stevens, Sotirov, Appelbaum, Lenstra, Molnar, Osvik, and Weger. Crypto 2009.
* [Chosen-prefix collisions for MD5 and applications][24]. Stevens, Lenstra, and de Weger. Int. J. Applied Cryptography, 2(4), 2012.
* [Analysis of the HTTPS Ecosystem][25]. Durumeric, Kasten, Bailey, and Halderman. IMC 2013.
* [Cryptanalysis of the Windows Random Number Generator][26]. Dorrendorf, Gutterman, and Pinkas. CCS 2007\.

###  Thursday, January 22

* [Lessons Learned in Implementing and Deploying Crypto Software][27]. Peter Gutmann. Usenix Security 2002.
* [Mining Your Ps and Qs: Detection of Widespread Weak Keys in Network Devices][28]. Heninger, Durumeric, Wustrow, and Halderman. Usenix Security 2012.
* [Why Cryptosystems Fail][29]. Ross Anderson. Commun. ACM, 37(11), Nov. 1994\.
* [Why Information Security is Hard: An Economic Perspective][30]. Ross Anderson. ACSAC 2001\.
* [The Most Dangerous Code in the World: Validating SSL Certificates in Non-Browser Software][31]. Georgiev, Iyengar, Jana, Anubhai, Boneh, and Shmatikov. CCS 2012.
* [ZMap: Fast Internet-Wide Scanning and its Security Applications][32]. Durumeric, Wustrow, and Halderman. Usenix Security 2013.
* [Scans.io][33]. (Internet scan data repository.)

## Binary Exploitation

###  Tuesday, January 27 — Basic Exploitation

* [Smashing the Stack for Fun and Profit][34]. Aleph One. Phrack 49(14), Nov. 1996\.
* [StackGuard: Automatic Adaptive Detection and Prevention of Buffer-Overflow Attacks][35]. Cowan, Pu, Maier, Hinton, Walpole, Bakke, Beattie, Grier, Wagle, and Zhang. Usenix Security 1998.
* [Beyond Stack Smashing: Recent Advances in Exploiting Buffer Overruns][36]. Pincus and Baker. IEEE Security and Privacy, July–Aug. 2004.
* [On the Effectiveness of ASLR][37]. Shacham, Page, Pfaff, Goh, Modadugu, and Boneh. CCS 2004\.
* [English Shellcode][38]. Mason, Small, Monrose, and MacManus. CCS 2009\.
* [AEG: Automatic Exploit Generation][39]. Avgerinos, Cha, Hao, and Brumley. NDSS 2011.

###  Thursday, January 29 — Modern Attacks

* [The Geometry of Innocent Flesh on the Bone: Return-into-libc without Function Calls (on the x86)][40]. Hovav Shacham. CCS 2007\.
* [Eternal War in Memory][41]. Szekeres, Payer, Wei, and Song. Oakland 2013.
* [VUPEN Vulnerability Research Blog][42]. (Details of advanced modern exploitation.)
* [Markets for Zero-Day Exploits: Ethics and Implications][43]. Egelman, Herley, and van Oorschot. NSPW 2013\.
* [An Empirical Study of Vulnerability Rewards Programs][44]. Finifter, Akhawe, and Wagner. Usenix Security 2013.
* [Nozzle: A Defense Against Heap-spraying Code Injection Attacks][45]. Ratanaworabhan, Livshits, and Zorn. Usenix Security 2009.

## Malicious Software

###  Tuesday, February 3 — Malware

* [Reflections on Trusting Trust][46]. Ken Thompson. Communications of the ACM, 27(8), Aug. 1984.
* [CloudAV: N-Version Antivirus in the Network Cloud][47]. Oberheide, Cooke, and Jahanian. Usenix Security 2008.
* [Towards Automatic Generation of Vulnerability-Based Signatures][48]. Brumley, Newsome, Song, Wang, and Jha. Oakland 2006\.
* [Control Flow Integrity for COTS Binaries][49]. Zhang and Sekar. Usenix Security 2013.
* [Inside the Slammer Worm][50]. Moore, Paxson, Savage, Shannon, Staniford, and Weaver. IEEE Security and Privacy, July/August 2003.
* [The Morris Worm: A Fifteen-Year Perspective][51]. Orman. IEEE Security and Privacy, Sept./Oct. 2003.

###  Thursday, February 5 — Isolation

* [Capsicum: Practical Capabilities for UNIX][52]. Watson, Anderson, Laurie, and Kennaway. Usenix Security 2010.
* [Native Client: A Sandbox for Portable, Untrusted x86 Native Code][53]. Yee, Sehr, Dardyk, Chen, Muth, Ormandy, Okasaka, Narula, and Fullagar. Oakland 2009\.
* [Leveraging Legacy Code to Deploy Desktop Applications on the Web][54]. Douceur, Elson, Howell, and Lorch. OSDI 2008\.
* [Safe Kernel Extensions Without Run-Time Checking][55]. Necula and Lee. OSDI 1996\.
* [The Security Architecture of the Chromium Browser][56]. Barth, Jackson, Reis, and The Google Chrome Team. 2008\.
* [The Ten-Page Introduction to Trusted Computing][57]. Martin. 2008\.

## Web Security

###  Tuesday, February 10 — Web Attacks

* [Blueprint: Robust Prevention of Cross-site Scripting Attacks for Existing Browsers][58]. Louw and Venkatakrishnan. Oakland 2009\.
* [Robust Defenses for Cross-Site Request Forgery][59]. Barth, Jackson, and Mitchell. CSS 2008\.
* [deDacota: Toward Preventing Server-Side XSS via Automatic Code and Data Separation][60]. Doupé, Cui, Jakubowski, Peinado, Kruegel, and Vigna. CCS 2013\.
* [Protection and Communication Abstractions for Web Browsers in MashupOS][61]. Wang, Fan, Howell, and Jackson. SOSP 2007\.
* [Enemy of the State: A State-Aware Black-Box Web Vulnerability Scanner][62]. Doupe, Cavedon, Kruegel, and Vigna. Usenix Security 2012.
* [OWASP Cheat Sheet Series][63]. Open Web Application Security Project.

###  Thursday, February 12 — Web Isolation

* [Securing Browser Frame Communication][64]. Barth, Jackson, and Mitchell. Usenix Security 2008.
* [Reining in the Web with Content Security Policy][65]. Stamm, Sterne, and Markham. WWW 2010.
* [Beware of Finer-Grained Origins][66]. Jackson and Barth. Web 2.0 Security and Privacy 2008.
* [Protecting Browsers from DNS Rebinding Attacks][67]. Jackson, Barth, Bortz, Shao, And Boneh. CCS 2007\.
* [Cross-Origin JavaScript Capability Leaks: Detection, Exploitation, and Defense][68]. Barth, Weinberger, and Song. Usenix Security 2009.
* [Eradicating DNS Rebinding with the Extended Same-Origin Policy][69]. Johns, Lekies, and Stock. Usenix Security 2013.

## Human Factors

###  Tuesday, February 17 — Authentication

* [reCAPTCHA: Human-Based Character Recognition via Web Security Measures][70]. von Ahn, Maurer, McMillen, Abraham, and Blum. Science, September 2008.
* [The Tangled Web of Password Reuse][71]. Das, Bonneau, Caesar, Borisov, and Wang. NDSS 2014\.
* [Games with a Purpose][72]. Luis von Ahn. CACM, August 2008.
* [Sketcha: A Captcha Based on Line Drawings of 3D Models][73]. Ross, Halderman, and Finkelstein. WWW 2010\.
* [The Robustness of Hollow CAPTCHAs][74]. Gao, Wang, Qi, Wang, Liu, and Yan. CCS 2013\.
* [How Good are Humans at Solving CAPTCHAs?][75] Bursztein, Bethard, Fabry, Mitchell, and Jurafsky. Oakland 2010.
* [The Science of Guessing: Analyzing an Anonymized Corpus of 70 Million Passwords][76]. Joseph Bonneau. Oakland 2012\.
* [A Usability Study and Critique of Two Password Managers][77]. Chiasson, van Oorschot, and Biddle. Usenix Security 2006.
* [Honeywords: Making Password-Cracking Detectable][78]. Juels and Rivest. CCS 2013\.
* [Designing Crypto Primitives Secure Against Rubber Hose Attacks][79]. Bojinov, Sanchez, Reber, Boneh, and Lincoln. Usenix Security 2012.

###  Thursday, February 19 — Usable Security

* [Why Johnny Can’t Encrypt: A Usability Evaluation of PGP 5.0][80]. Whitten and Tygar. Usenix Security 1999.
* [The Psychology of Security for the Home Computer User][81]. Howe, Ray, Roberts, Urbanska, and Byrne. Oakland 2012.
* [So Long, And No Thanks for the Externalities: The Rational Rejection of Security Advice by Users][82]. Cormac Herley. NSPW 2009\.
* [Secrecy, Flagging, and Paranoia: Adoption Criteria in Encrypted Email][83]. Gaw, Felten, and Fernandez-Kelly. CHI 2006\.
* [In Search of Usable Security: Five Lessons from the Field][84]. Balfanz, Durfee, Grinter, and Smetters. IEEE Security and Privacy, September/October 2004.
* [Folk Models of Home Computer Security][85]. Rick Wash. SOUPS 2010\.
* [Your Attention Please: Designing Security-Decision UIs][86]. Bravo-Lillo, Cranor, Downs, Komanduri, Reeder, Schechter, and Sleeper. SOUPS 2013\.
* [Alice in Warningland: A Large-Scale Field Study of Browser Security Warning Effectiveness][87]. Akhawe and Felt. Usenix Security 2013.
* [Why (Special Agent) Johnny (Still) Can't Encrypt][88]. Clark, Goodspeed, Metzger, Wasserman, Xu, and Blaze. Usenix Security 2011.

## Mobile Security

###  Tuesday, February 24 — Mobile Security

* [Dissecting Android Malware: Characterization and Evolution][89]. Zhou and Jiang. Oakland 2012.
* [You Can Run, but You Can’t Hide: Exposing Network Location for Targeted DoS Attacks in Cellular Networks][90]. Qian, Wang, Xu, Mao, Zhang, and Wang. NDSS 2012\.
* [Smart-Phone Attacks and Defenses][91]. Guo, Wang, and Zhu. HotNets 2004\.
* [Android Permissions: User Attention, Comprehension, and Behavior][92]. Felt, Ha, Egelman, Haney, Chin, and Wagner. SOUPS 2012\.
* [Android Permissions Demystified][93]. Felt, Chin, Hanna, Song, and Wagner. CCS 2011\.
* [User-Driven Access Control: Rethinking Permission Granting in Modern Operating Systems][88]. Roesner, Kohno, Moshchuk, Parno, Wang, and Cowan. Oakland 2012.
* [Predictability of Android OpenSSL's Pseudorandom Number Generator][94]. Kim, Han, and Lee. CCS 2013\.

###  Thursday, February 26 — Pre-proposal presentations No written response required for today.

## Network Security

###  Tuesday, March 10 — Network Attacks

* [A Look Back at “Security Problems in the TCP/IP Protocol Suite.”][95] Steve Bellovin. ACSAC 2004\.
* [The Crossfire Attack][96]. Kang, Lee, and Gligor. Oakland 2013.
* [Blind TCP/IP Hijacking is Still Alive][97]. lkm. Phrack 64, 2007.
* [A Survey of BGP Security Issues and Solutions][98]. Butler, Farley, McDaniel, and Rexford. 2008\.
* [Black Ops 2008: It’s the End of the Cache as We Know It][99]. Dan Kaminsky. Toorcon 2008\.
* [Increased DNS Forgery Resistance Through 0x20-Bit Encoding][100]. Dagon, Antonakakis, Vixie, Jinmei, and Lee. CCS 2008\.
* [Bro: A System for Detecting Network Intruders in Real-Time][101]. Vern Paxson. Computer Networks 31(23-24), 1999.
* [The Security Flag in the IPv4 Header][102]. Steve Bellovin. RFC 3514.

###  Thursday, March 12 — Online Crime

* [Spamalytics: An Empirical Analysis of Spam Marketing Conversion][103]. Kanich, Kreibich, Levchenko, Enright, Voelker, Paxson, and Savage. CCS 2008\.
* [Your Botnet is My Botnet: Analysis of a Botnet Takeover][104]. Stone-Gross, Cova, Cavallaro, Gilbert, Szydlowski, Kemmerer, Kruegel, and Vigna. CCS 2009\.
* [Modeling and Evaluating the Resilience of Peer-to-Peer Botnets][105]. Rossow, Andriesse, Werner, Stone-Gross, Plohmann, Dietrich, and Bos. Oakland 2013.
* [A Multifaceted Approach to Understanding the Botnet Phenomenon][106]. Rajab, Zarfoss, Monrose, and Terzis. ISC 2006\.
* [What’s Clicking What? Techniques and Innovations of Today’s Clickbots][107]. Miller, Pearce, Grier, Kreibich, and Paxson. DIMVA 2011\.
* [Clickjacking: Attacks and Defenses][108]. Huang, Moshchuk, Wang, Schechter, and Jackson. Usenix Security 2012.
* [@spam: The Underground on 140 Characters or Less][109]. Grier, Thomas, Paxson, and Zhang. CCS 2010.
* [On the Mismanagement and Maliciousness of Networks][110]. Zhang, Durumeric, Bailey, Liu, and Karir. NDSS 2014.

## Advanced Threats

###  Tuesday, March 17 — Cyberwarfare

* [W32.Stuxnet Dossier][111]. Falliere, Murchu, and Chien. Symantec technical report, 2011.
* [APT1 Report][112]. Mandiant technical report, 2013.
* [Cyberwar and Peace][113]. Thomas Rid. Foreign Affairs, Nov./Dec. 2013.
* [NSA's ANT Division Catalog of Exploits][114]. Published by _Der Spiegel_, Dec. 2013.
* [To Kill a Centrifuge][115]. Ralph Langner. Nov. 2013.
* [iSeeYou: Disabling the MacBook Webcam Indicator LED][116]. Brocker and Checkoway. Dec. 2013.
* [Reversing and Exploiting an Apple Firmware Update][117]. K. Chen. BlackHat USA 2009.
* [SkyNET: A Mobile Attack Drone and Stealth Botmaster][118]. Reed, Geis, and Dietrich. WOOT 2011\.
* [Designing and Implementing Malicious Hardware][119]. King, Tucek, Cozzie, Grier, Jiang, and Zhou. LEET 2008\.
* [Stealthy Dopant-Level Hardware Trojans][120]. Becker, Regazzoni, Paar, and Burleson. CHES 2013.

###  Thursday, March 19 — Mass Surveillance

* [Decoding the Summer of Snowden][121]. Julian Sanchez. Cato Policy Report, 2013.
* [Liberty and Security in a Changing World][122]. President's review group on intelligence and communications technologies. Dec. 2013.
* [Report on the Telephone Records Program Conducted under Section 215][123]. Privacy and Civil Liberties Oversight Board. Jan. 2014.
* [NSA Collecting Phone Records of Millions of Verizon Customers Daily][124]. Glenn Greenwald. The Guardian, Jun. 2013.
* [NSA Infiltrates Links to Yahoo, Google Data Centers Worldwide, Snowden Documents Say][125]. Gellman and Soltani. Washington Post, Oct. 2013.
* [NSA Collects Millions of Text Messages Daily in ‘Untargeted’ Global Sweep][126]. James Ball. The Guardian, Jan. 2014.
* [Global Surveillance Disclosures][127]. Wikipedia.
* [Catalog of the Snowden revelations][128]. Lawfare.

## Securing Critical Systems

###  Tuesday, March 24 — Health and Safety

* [Experimental Security Analysis of a Modern Automobile][129]. Koscher, Czeskis, Roesner, Patel, Kohno, Checkoway, McCoy, Kantor, Anderson, Shacham, and Savage. Oakland 2010\.
* [Security and Privacy for Implantable Medical Devices][130]. Halperin, Heydt-Benjamin, Fu, Kohno, and Maisel. IEEE Pervasive Computing 7(1), 2008.
* [Comprehensive Experimental Analyses of Automotive Attack Surfaces][131]. Checkoway, McCoy, Kantor, Anderson, Shacham, Savage, Koscher, Czeskis, Roesner, and Kohno. Usenix Security 2011.
* [Pacemakers and Implantable Cardiac Defibrillators: Software Radio Attacks and Zero-Power Defenses][132]. Halperin, Heydt-Benjamin, Ransford, Clark, Defend, Morgan, Fu, Kohno, and Maisel. Oakland 2008.
* [Illuminating the Security Issues Surrounding Lights-Out Server Management][133]. Bonkoski, Bielawski, and Halderman. WOOT 2013.
* [Building the IBM 4758 Secure Coprocessor][134]. Dyer, Lnidermann, Perez, Sailer, van Doorn, Smith, and Weingart. IEEE Computer, Oct. 2001.

###  Thursday, March 26 — Securing TLS

* [SSL and HTTPS: Revisiting Past Challenges and Evaluating Certificate Trust Model Enhancements][135]. Clark and van Oorschot. Oakland 2013.
* [The Most Dangerous Code in the World: Validating SSL Certificates in Non-Browser Software][136]. Georgiev, Iyengar, Jana, Anubhai, Boneh, and Shamatikov. CCS 2012\.
* [ForceHTTPS Cookies: A Defense Against Eavesdropping and Pharming][137]. Jackson and Barth. WWW 2008\.
* [Null Prefix Attacks Against SSL/TLS Certificates][138]. Moxie Marlinspike. 2009\.
* [Lucky 13: Breaking the TLS and DTLS Record Protocols][139]. AlFardan and Paterson. Oakland 2013.
* [On the Security of RC4 in TLS][140]. AlFardan, Bernstein, Paterson, Schuldt, and Holloway. Usenix Security 2013.
* [CAge: Taming Certificate Authorities by Inferring Restricted Scopes][141]. Kasten, Wustrow, and Halderman. FC 2013\.
* [Certied Lies: Detecting and Defeating Government Interception Attacks Against SSL][142]. Soghoian and Stamm. FC 2011.
* [Lavabit Legal Proceedings][143]. 2013\.

## Privacy and Confidentiality

###  Tuesday, March 31 — Privacy in the Cloud

* [Third-Party Web Tracking: Policy and Technology][144]. Mayer and Mitchell. Oakland 2012.
* [Social Networking with Frientegrity: Privacy and Integrity with an Untrusted Provider][145]. Feldman, Blankstein, Freedman, and Felten. Usenix Security 2012.
* “[You Might Also Like:” Privacy Risks of Collaborative Filtering][146]. Calandrino, Kilzer, Narayanan, Felten, and Shmatikov. Oakland 2011.
* [Remote Physical Device Fingerprinting][147]. Kohno, Broido, and Claffy. Oakland 2005\.
* [Host Fingerprinting and Tracking on the Web][148]. Yen, Xie, Yu, Yu, and Abadi. NDSS 2012\.
* [Selling Off Privacy at Auction][149]. Olejnik, Tran, and Castelluccia. NDSS 2014\.
* [Adnostic: Privacy Preserving Targeted Advertising][150]. Toubiana, Narayanan, Boneh, Nissenbaum, and Barocas. NDSS 2010\.
* [CryptDB: Protecting Confidentiality with Encrypted Query Processing][151]. Popa, Redfield, Zeldovich, and Balakrishnan. SOSP 2011\.
* [Securing Web Applications by Blindfolding the Server][152]. Popa, Stark, Valdez, Helfer, Zeldovich, Kasshoek, and Balakrishnan. NSDI 2014\.
* [Privacy Policy][153]. Google, Inc.

###  Thursday, April 2 — Deletion and Leakage

* [Lest We Remember: Cold Boot Attacks on Encryption Keys][154]. Halderman, Schoen, Heninger, Clarkson, Paul, Calandrino, Feldman, Appelbaum, and Felten. Usenix Security 2008.
* [Secure Data Deletion][155]. Reardon, Basin, and Capkun. Oakland 2013.
* [History Independence for File Systems][156]. Bajat and Sion. CCS 2013\.
* [BootJacker: Compromising Computers Using Forced Restarts][157]. Chan, Carlyle, David, Farivar, and Campbell. CCS 2008\.
* [Shredding Your Garbage: Reducing Data Lifetime Through Secure Deallocation][158]. Chow, Pfaff, Garfinkel, and Rosenblum. Usenix Security 2005.
* [Increasing Data Privacy with Self-Destructing Data][159]. Geambasu, Kohno, Levy, and Levy. Usenix Security 2009.
* [Defeating Vanish with Low-Cost Sybil Attacks Against Large DHTs][160]. Wolchok, Hofmann, Heninger, Felten, Halderman, Rossbach, Waters, and Witchel. NDSS 2010\.
* [Reconstructing RSA Private Keys from Random Key Bits][161]. Heninger and Shacham. Crypto 2009\.
* [Peeping Tom in the Neighborhood: Keystroke Eavesdropping on Multi-User Systems][162]. Zhang and Wang. Usenix Security 2009.

## Online Freedom

###  Tuesday, April 7

* [Tor: The Second-Generation Onion Router][163]. Dingledine, Mattewson, and Syverson. Usenix Security 2004.
* [Off-the-Record Communication, or, Why Not to Use PGP][164]. Borisov, Goldberg, and Brewer. WPES 2004\.
* [Collateral Freedom: A Snapshot of Chinese Internet Users Circumventing Censorship][165]. Robinson, Yu, and An. OpenITP, 2013.
* [ConceptDoppler: A Weather Tracker for Internet Censorship][166]. Crandall, Zinn, Byrd, Barr, and East. CCS 2007\.
* [Chipping Away at Censorship with User-Generated Content][167]. Burnett, Feamster, and Vempala. Usenix Security 2010.
* [Internet Censorship in China: Where Does the Filtering Occur?][168] Xu, Mao, and Halderman. PAM 2011\.
* [Internet Censorship in Iran: A First Look][169]. Aryan, Aryan, and Halderman. FOCI 2013\.
* [Analysis of the Green Dam Censorware System][170]. Wolchok, Yao, and Halderman. Tech Report, 2009.
* [No Direction Home: The True Cost of Routing Around Decoys][171]. Houmansadr, Wong, and Shmatikov. NDSS 2014\.
* [An Analysis of Private Browsing Modes in Modern Browsers][172]. Aggarwal, Bursztein, Jackson, and Boneh. Usenix Security 2010.

###  Thursday, April 9

* [Bitcoin: A Peer-to-Peer Electronic Cash System][173]. Satoshi Nakamoto. 2008\.
* [Telex: Anticensorship in the Network Infrastructure][174]. Wustrow, Wolchok, Goldberg, and Halderman. Usenix Security 2011.
* [Trawling for Tor Hidden Services][175]. Biryukov, Pustogarov, and Weinmann. Oakland 2013.
* [Criminal Complaint, U.S. v. Ulbricht][176]. Oct. 2013.
* [Zerocoin: Anonymous Distributed E-Cash from Bitcoin][177]. Miers, Garman, Green, and Rubin. Oakland 2013.
* [Shining Light in Dark Places: Understanding the Tor Network][178]. McCoy, Bauer, Grunwald, Kohno, and Sicker. PETS 2008\.
* [Users Get Routed: Traffic Correlation on Tor by Realistic Adversaries][179]. Johnson, Wacek, Jansen, Sherr, and Syverson. CCS 2013.
* [How the NSA Attacks Tor Users with QUANTUM and FOXACID][180]. Bruce Schneier. Oct. 2013.
* [Cover Your ACKs: Pitfalls of Covert Channel Censorship Circumvention][181]. Geddes, Schuchard, and Hopper. CCS 2013\.
* [Protocol Misidentification Made Easy with Format-Transforming Encryption][182]. Dyer, Coull, Ristenpart, and Shrimpton. CSS 2013\.
* [Spot Me If You Can: Uncovering Spoken Phrases in Encrypted VoIP Conversations][183]. Wright, Ballard, Coull, Monrose, and Masson. Oakland 2008\.

## Physical Security

###  Tuesday, April 21 No written response required for today.

* [Cryptology and Physical Security: Rights Amplification in Master-Keyed Mechanical Locks][184]. Matt Blaze. IEEE Security and Privacy, March/April 2003.
* [Keep it Secret, Stupid!][185] Matt Blaze. 2003\.
* [Picking Pin Tumbler Locks][186]. Matt Blaze. 2003\.
* [Safecracking for the Computer Scientist][187]. Matt Blaze. 2004\.
* [Reconsidering Physical Key Secrecy: Teleduplication via Optical Decoding][188]. Laxton, Wang, and Savage. CCS 2008\.
* [Security Analysis of a Widely Deployed Locking System][189]. Weiner, Massar, Tews, Giese, and Wieser. CCS 2013\.

  

[1]: ./
[2]: schedule.html
[3]: readings.html
[4]: attacks.html
[5]: project.html
[6]: https://eecs588.org/login
[7]: https://en.wikipedia.org/wiki/Academic_journal_publishing_reform
[8]: https://www.itcom.itd.umich.edu/vpn/
[9]: https://www.lib.umich.edu/mlibrary-labs/proxy-server-bookmarklet
[10]: ./static/588-w15-intro.pdf
[11]: https://www.schneier.com/blog/archives/2008/03/the_security_mi_1.html
[12]: https://www.cl.cam.ac.uk/~rja14/book.html
[13]: http://cacr.uwaterloo.ca/hac/
[14]: ./static/588-w15-crypto.pdf
[15]: https://archive.is/fo1BG
[16]: https://tools.ietf.org/html/rfc5246
[17]: http://www.moserware.com/2009/06/first-few-milliseconds-of-https.html
[18]: https://www.startssl.com/
[19]: https://letsencrypt.org/
[20]: https://eprint.iacr.org/2004/357
[21]: https://www.win.tue.nl/hashclash/rogue-ca/
[22]: http://www.infosec.sdu.edu.cn/uploadfile/papers/How%20to%20Break%20MD5%20and%20Other%20Hash%20Functions.pdf
[23]: http://deweger.xs4all.nl/papers/[41]StSoApLeMoOsdW-RogueCA-Crypto[2009].pdf
[24]: https://documents.epfl.ch/users/l/le/lenstra/public/papers/lat.pdf
[25]: https://jhalderm.com/pub/papers/https-imc13.pdf
[26]: http://portal.acm.org/citation.cfm?id=1315304
[27]: https://www.usenix.org/event/sec02/full_papers/gutmann/gutmann.pdf
[28]: https://factorable.net/paper.html
[29]: https://www.cl.cam.ac.uk/~rja14/Papers/wcf.pdf
[30]: https://www.cl.cam.ac.uk/~rja14/Papers/econ.pdf
[31]: https://www.cs.utexas.edu/~shmat/shmat_ccs12.pdf
[32]: https://zmap.io/paper.html
[33]: https://scans.io
[34]: ./static/stack_smashing.pdf
[35]: http://static.usenix.org/publications/library/proceedings/sec98/full_papers/cowan/cowan.pdf
[36]: http://ieeexplore.ieee.org.proxy.lib.umich.edu/xpls/abs_all.jsp?arnumber=1324594
[37]: https://portal.acm.org/citation.cfm?id=1030124&dl=ACM&coll=
[38]: http://www.cs.jhu.edu/~sam/ccs243-mason.pdf
[39]: http://security.ece.cmu.edu/aeg/aeg-current.pdf
[40]: http://www-cse.ucsd.edu/~hovav/papers/s07.html
[41]: http://www.cs.berkeley.edu/~dawnsong/papers/Oakland13-SoK-CR.pdf
[42]: http://www.vupen.com/blog/
[43]: http://people.scs.carleton.ca/~paulv/papers/NSPW-2013-author-version.pdf
[44]: https://www.usenix.org/conference/usenixsecurity13/technical-sessions/presentation/finifter
[45]: http://research.microsoft.com/apps/pubs/default.aspx?id=76528
[46]: http://portal.acm.org/citation.cfm?id=358210
[47]: https://www.usenix.org/events/sec08/tech/full_papers/oberheide/oberheide.pdf
[48]: http://bitblaze.cs.berkeley.edu/papers/sig-gen-oakland06.pdf
[49]: https://www.usenix.org/conference/usenixsecurity13/technical-sessions/presentation/Zhang
[50]: http://www.cs.ucsd.edu/~savage/papers/IEEESP03.pdf
[51]: http://ieeexplore.ieee.org/xpl/articleDetails.jsp?arnumber=1236233
[52]: https://www.usenix.org/legacy/events/sec10/tech/full_papers/Watson.pdf
[53]: https://static.googleusercontent.com/external_content/untrusted_dlcp/research.google.com/en/us/pubs/archive/34913.pdf
[54]: https://research.microsoft.com/apps/pubs/?id=72878
[55]: https://www.usenix.org/publications/library/proceedings/osdi96/necula.html
[56]: http://www.adambarth.com/papers/2008/barth-jackson-reis.pdf
[57]: http://www.comlab.ox.ac.uk/files/1873/RR-08-11.PDF
[58]: http://www.cs.uic.edu/~venkat/research/papers/blueprint-oakland09.pdf
[59]: https://crypto.stanford.edu/websec/csrf/csrf.pdf
[60]: http://cs.ucsb.edu/~adoupe/static/dedacota-ccs2013.pdf
[61]: https://research.microsoft.com/~helenw/papers/sosp07MashupOS.pdf
[62]: https://www.usenix.org/system/files/conference/usenixsecurity12/sec12-final225.pdf
[63]: https://www.owasp.org/index.php/Cheat_Sheets
[64]: https://crypto.stanford.edu/websec/frames/post-message.pdf
[65]: http://research.sidstamm.com/papers/csp-www2010.pdf
[66]: https://crypto.stanford.edu/websec/origins/fgo.pdf
[67]: https://crypto.stanford.edu/dns/dns-rebinding.pdf
[68]: http://www.adambarth.com/papers/2009/barth-weinberger-song.pdf
[69]: https://www.usenix.org/conference/usenixsecurity13/technical-sessions/presentation/johns
[70]: http://www.cs.cmu.edu/~biglou/reCAPTCHA_Science.pdf
[71]: https://web.engr.illinois.edu/~das17/paper/NDSS2014.pdf
[72]: http://www.cs.cmu.edu/~biglou/ieee-gwap.pdf
[73]: https://jhalderm.com/pub/papers/sketcha-www10.pdf
[74]: http://dl.acm.org/citation.cfm?id=2516732
[75]: http://theory.stanford.edu/~jcm/papers/captcha-study-oakland10.pdf
[76]: https://www.cl.cam.ac.uk/~jcb82/doc/B12-IEEESP-evaluating_a_huge_password_corpus.pdf
[77]: http://www.scs.carleton.ca/~paulv/papers/usenix06.pdf
[78]: http://people.csail.mit.edu/rivest/pubs/JR13.pdf
[79]: https://www.usenix.org/system/files/conference/usenixsecurity12/sec12-final25.pdf
[80]: http://gaudior.net/alma/johnny.pdf
[81]: http://www.ieee-security.org/TC/SP2012/papers/4681a209.pdf
[82]: https://research.microsoft.com/en-us/um/people/cormac/papers/2009/solongandnothanks.pdf
[83]: https://www.cs.princeton.edu/~sgaw/publications/01Feb-Activists-sgaw-CHI2006.pdf
[84]: http://www.cc.gatech.edu/~beki/j7.pdf
[85]: http://www.rickwash.com/papers/rwash-homesec-soups10-final.pdf
[86]: http://cups.cs.cmu.edu/soups/2013/proceedings/a6_Bravo-Lillo.pdf
[87]: https://www.usenix.org/conference/usenixsecurity13/technical-sessions/presentation/akhawe
[88]: http://www.usenix.org/events/sec11/tech/full_papers/Clark.pdf
[89]: http://www.csc.ncsu.edu/faculty/jiang/pubs/OAKLAND12.pdf
[90]: https://www.eecs.umich.edu/~zhiyunq/pub/ndss12_rnc_fingerprinting.pdf
[91]: https://research.microsoft.com/~helenw/papers/smartphone.pdf
[92]: http://cups.cs.cmu.edu/soups/2012/proceedings/a3_Felt.pdf
[93]: http://www.cs.berkeley.edu/~afelt/android_permissions.pdf
[94]: http://dl.acm.org/citation.cfm?id=2516706
[95]: https://www.cs.columbia.edu/~smb/papers/ipext.pdf
[96]: http://www.ieee-security.org/TC/SP2013/papers/4977a127.pdf
[97]: http://www.phrack.org/issues.html?issue=64&id=13
[98]: https://www.cs.princeton.edu/~jrex/papers/bgp-security08.pdf
[99]: http://s3.amazonaws.com/dmk/DMK_BO2K8.ppt
[100]: http://portal.acm.org/citation.cfm?id=1455770.1455798
[101]: papers/bro-CN99.pdf
[102]: http://www.ietf.org/rfc/rfc3514.txt
[103]: http://www.icir.org/christian/publications/2008-ccs-spamalytics.pdf
[104]: http://seclab.cs.ucsb.edu/media/uploads/papers/torpig.pdf
[105]: http://www.christian-rossow.de/publications/p2pwned-ieee2013.pdf
[106]: http://www.cs.jhu.edu/~fabian/papers/botnets.pdf
[107]: http://www.cs.berkeley.edu/~pearce/papers/clickbots_dimva_2011.pdf
[108]: https://www.usenix.org/system/files/conference/usenixsecurity12/sec12-final39.pdf
[109]: http://www.icir.org/vern/papers/ccs2010-twitter-spam.pdf
[110]: http://web.eecs.umich.edu/~jingzj/paper/jing_ndss14.pdf
[111]: http://securityresponse.symantec.com/en/id/content/en/us/enterprise/media/security_response/whitepapers/w32_stuxnet_dossier.pdf
[112]: http://intelreport.mandiant.com/Mandiant_APT1_Report.pdf
[113]: http://www.foreignaffairs.com/articles/140160/thomas-rid/cyberwar-and-peace
[114]: http://leaksource.wordpress.com/2013/12/30/nsas-ant-division-catalog-of-exploits-for-nearly-every-major-software-hardware-firmware/
[115]: http://www.langner.com/en/wp-content/uploads/2013/11/To-kill-a-centrifuge.pdf
[116]: https://jscholarship.library.jhu.edu/bitstream/handle/1774.2/36569/camera.pdf
[117]: https://www.blackhat.com/presentations/bh-usa-09/CHEN/BHUSA09-Chen-RevAppleFirm-PAPER.pdf
[118]: http://static.usenix.org/events/woot11/tech/final_files/Reed.pdf
[119]: http://www.usenix.org/event/leet08/tech/full_papers/king/king.pdf
[120]: https://people.umass.edu/gbecker/BeckerChes13.pdf
[121]: http://www.cato.org/policy-report/novemberdecember-2013/decoding-summer-snowden
[122]: http://www.whitehouse.gov/sites/default/files/docs/2013-12-12_rg_final_report.pdf
[123]: http://s3.documentcloud.org/documents/1008940/final-report.pdf
[124]: http://www.theguardian.com/world/2013/jun/06/nsa-phone-records-verizon-court-order
[125]: http://www.washingtonpost.com/world/national-security/nsa-infiltrates-links-to-yahoo-google-data-centers-worldwide-snowden-documents-say/2013/10/30/e51d661e-4166-11e3-8b74-d89d714ca4dd_story.html
[126]: http://www.theguardian.com/world/2014/jan/16/nsa-collects-millions-text-messages-daily-untargeted-global-sweep
[127]: https://en.wikipedia.org/wiki/Global_surveillance_disclosures_(2013%E2%80%93present)
[128]: http://www.lawfareblog.com/catalog-of-the-snowden-revelations/
[129]: http://www.autosec.org/pubs/cars-oakland2010.pdf
[130]: https://spqr.eecs.umich.edu/papers/b1kohFINAL2.pdf
[131]: http://www.autosec.org/pubs/cars-usenixsec2011.pdf
[132]: http://www.secure-medicine.org/public/publications/icd-study.pdf
[133]: https://jhalderm.com/pub/papers/ipmi-woot13.pdf
[134]: http://ieeexplore.ieee.org/iel5/2/20660/00955100.pdf?arnumber=955100
[135]: http://www.ieee-security.org/TC/SP2013/papers/4977a511.pdf
[136]: http://www.cs.utexas.edu/~shmat/shmat_ccs12.pdf
[137]: https://crypto.stanford.edu/forcehttps/
[138]: http://www.thoughtcrime.org/papers/null-prefix-attacks.pdf
[139]: http://www.ieee-security.org/TC/SP2013/papers/4977a526.pdf
[140]: https://www.usenix.org/conference/usenixsecurity13/technical-sessions/paper/alFardan
[141]: https://jhalderm.com/pub/papers/cage-fc13.pdf
[142]: http://files.cloudprivacy.net/ssl-mitm.pdf
[143]: https://www.documentcloud.org/documents/801182-redacted-pleadings-exhibits-1-23.html
[144]: https://www.stanford.edu/~jmayer/papers_data/trackingsurvey12.pdf
[145]: https://www.usenix.org/system/files/conference/usenixsecurity12/sec12-final67.pdf
[146]: http://www.ieee-security.org/TC/SP2011/PAPERS/2011/paper015.pdf
[147]: http://www.cs.washington.edu/homes/yoshi/papers/PDF/KoBrCl05PDF-lowres.pdf
[148]: http://research.microsoft.com/pubs/156901/ndss2012.pdf
[149]: http://hal.archives-ouvertes.fr/docs/00/91/52/49/PDF/SellingOffPrivacyAtAuction.pdf
[150]: https://crypto.stanford.edu/adnostic/adnostic-ndss.pdf
[151]: http://web.mit.edu/ralucap/www/CryptDB-sosp11.pdf
[152]: https://css.csail.mit.edu/mylar/mylar.pdf
[153]: https://www.google.com/policies/privacy/
[154]: https://citp.princeton.edu/memory/
[155]: http://www.inf.ethz.ch/personal/basin/pubs/oakland13.pdf
[156]: http://dl.acm.org/citation.cfm?id=2516724
[157]: http://srgsec.cs.uiuc.edu/bootjacker.pdf
[158]: http://static.usenix.org/events/sec05/tech/full_papers/chow/chow.pdf
[159]: http://vanish.cs.washington.edu/pubs/usenixsec09-geambasu.pdf
[160]: https://jhalderm.com/pub/papers/unvanish-ndss10-web.pdf
[161]: http://www.cs.ucsd.edu/~hovav/papers/hs09.html
[162]: https://www.usenix.org/events/sec09/tech/full_papers/zhang.pdf
[163]: https://svn.torproject.org/svn/projects/design-paper/tor-design.pdf
[164]: http://www.cypherpunks.ca/~iang/pubs/otr-wpes.pdf
[165]: https://openitp.org/pdfs/CollateralFreedom.pdf
[166]: http://earlbarr.com/publications/conceptDoppler.pdf
[167]: http://www.gtnoise.net/papers/2010/burnett:usenixsec2010.pdf
[168]: http://pam2011.gatech.edu/papers/pam2011--Xu.pdf
[169]: https://jhalderm.com/pub/papers/iran-foci13.pdf
[170]: https://jhalderm.com/pub/gd/
[171]: http://www.cs.utexas.edu/~shmat/shmat_ndss14decoy.pdf
[172]: https://crypto.stanford.edu/~dabo/pubs/papers/privatebrowsing.pdf
[173]: http://bitcoin.org/bitcoin.pdf
[174]: https://telex.cc/pub/telex-usenixsec11.pdf
[175]: http://www.ieee-security.org/TC/SP2013/papers/4977a080.pdf
[176]: http://cdn3.sbnation.com/assets/3326809/UlbrichtCriminalComplaint.pdf
[177]: http://spar.isi.jhu.edu/~mgreen/ZerocoinOakland.pdf
[178]: https://www.cs.washington.edu/homes/yoshi/papers/Tor/PETS2008_37.pdf
[179]: http://www.ohmygodel.com/publications/usersrouted-ccs13.pdf
[180]: https://www.schneier.com/blog/archives/2013/10/how_the_nsa_att.html
[181]: http://www-users.cs.umn.edu/~hopper/ccs13-cya.pdf
[182]: http://eprint.iacr.org/2012/494.pdf
[183]: http://cs.unc.edu/~fabian/papers/oakland08.pdf
[184]: http://www.crypto.com/papers/mk.pdf
[185]: http://www.crypto.com/papers/kiss.html
[186]: http://www.crypto.com/papers/notes/picking/
[187]: http://www.crypto.com/papers/safelocks.pdf
[188]: http://vision.ucsd.edu/~blaxton/pagePapers/laxton_wang_savage_ccs2008.pdf
[189]: http://dl.acm.org/citation.cfm?id=2516733
 
