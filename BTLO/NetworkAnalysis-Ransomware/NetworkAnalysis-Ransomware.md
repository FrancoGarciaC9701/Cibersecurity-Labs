# BTLO - Lab: Network Analysis - Ransomware

https://blueteamlabs.online/home/challenge/network-analysis-ransomware-3dd520c7ec

# 📝 Scenario
ABC Industries worked day and night for a month to prepare a tender document for a prestigious project that would secure the company’s financial future. The company was hit by ransomware, believed to be conducted by a competitor, and the final version of the tender document was encrypted. Right now they are in need of an expert who can decrypt this critical document. All we have is the network traffic, the ransom note, and the encrypted ender document. Do your thing Defender!​

# What am I going to wear?
. VMWare with Linux - Wireshark - TShark - VirusTotal - RansomwareFileDecryption

# 🔎 Steps
1. Dowload the lab file
2. Unzip the file and the other file if required
3. In this case, we will analyze traffic with Wireshark
4. Answer the questions one by one

# Questions
a. What is the operating system of the host from which the network traffic was captured? 

b. What is the full URL from which the ransomware executable was downloaded? 

c. Name the ransomware executable file? 

d. What is the MD5 hash of the ransomware? 

e. What is the name of the ransomware? 

f. What is the encryption algorithm used by the ransomware, according to the ransom note? 

g. What is the domain beginning with ‘d’ that is related to ransomware traffic? 

h. Decrypt the Tender document and submit the flag

# ❓ Question (A) What is the operating system of the host from which the network traffic was captured? 

We go to the statistics section > Capture File Properties, under capture in OS

![OS](https://github.com/FrancoGarciaC9701/Cibersecurity-Labs/blob/8423f68af8eb6d3ac1e08ae6eab6968eb5b6ba92/BTLO/NetworkAnalysis-Ransomware/Images/NAR-Statistics.png)

✅ The Answer is: 32-bit Windows 7 Service Pack 1, build 7601

# ❓ Question (B) What is the full URL from which the ransomware executable was downloaded? 

We go to the Wireshark search engine and filter by http.request because with this query we are asking to see the complete URL from where the ransomware was downloaded.

![http](https://github.com/FrancoGarciaC9701/Cibersecurity-Labs/blob/1e2a72ade786a2d7ac7a91d44c0e8eb3f43ad5e4/BTLO/NetworkAnalysis-Ransomware/Images/NAR-http.png)
![fullrequest](https://github.com/FrancoGarciaC9701/Cibersecurity-Labs/blob/1e2a72ade786a2d7ac7a91d44c0e8eb3f43ad5e4/BTLO/NetworkAnalysis-Ransomware/Images/NAR-fullrequest.png)

Within the file that the query gave us, in the Hypertext Transfer Protocol section it gives us the full request in violet

✅ The Answer is: http://10.0.2.15:8000/safecrypt.exe

# ❓ Question (C) Name the ransomware executable file?

At the end of the URL we can see the name of the executable ending in .exe

✅ The Answer is: safecrypt.exe

# ❓ Question (D) What is the MD5 hash of the ransomware? 

Since there is no query in Wireshark that gives us the md5 hash, we will have to extract the file with Tshark. First, let's look at the protocol used in Statistics > Protocol Hierarchy. In any case, we can see it in what the "http.request" query gives us.

![SPH](https://github.com/FrancoGarciaC9701/Cibersecurity-Labs/blob/c5727ee900780cabc41e4bb9a0275974a62c5d7e/BTLO/NetworkAnalysis-Ransomware/Images/NAR-extraction1.png)

We see that it is http then in Tshark we use the following command to create a folder and extract the executable from the .pcap file (DO NOT RUN IT THE .EXE FILE):

tshark -r  ransom_traffic.pcapng --export-objects http,./archivos_extraidos

Once we have the executable extracted, we enter the folder where we saved it and use md5sum to extract the hash:

![Md5Extract](https://github.com/FrancoGarciaC9701/Cibersecurity-Labs/blob/06690cea46084ac993a6a68da4aa7d3a17ed1786/BTLO/NetworkAnalysis-Ransomware/Images/NAR-md5extract.png.png)

✅ The Answer is: 4a1d88603b1007825a9c6b36d1e5de44

# ❓ Question (E) What is the name of the ransomware? 

After using the hash we obtained in the previous exercise, we are going to take it to Virustotal to analyze it

![RName](https://github.com/FrancoGarciaC9701/Cibersecurity-Labs/blob/526fff6d5771b8c4e966f64545beeeee26dcab53/BTLO/NetworkAnalysis-Ransomware/Images/NAR-ransomwarename.png)

We can see in family labels that it is already associated with other investigations and in the antivirus search engines we see a name that is repeated in similar ways. "Teslacrypt" "Tescrypt"
We tried those two and found it to be Teslacrypt

✅ The Answer is: Teslacrypt

# ❓ Question (F) What is the encryption algorithm used by the ransomware, according to the ransom note? 

At the beginning of the message they sent us, we can see that they informed us that they used RSA-4096 to encrypt the files.

![Encrypt](https://github.com/FrancoGarciaC9701/Cibersecurity-Labs/blob/2c1a2367bec7bf699e03811bb403990fe1d03d65/BTLO/NetworkAnalysis-Ransomware/Images/help_recover_instructions.png)

✅ The Answer is: RSA-4096

# ❓ Question (G) What is the domain beginning with ‘d’ that is related to ransomware traffic?

We go back to Wireshark, as we need to look for a domain related to the ransomware traffic that starts with "d" and after comparing the few domains we found with "d" with the domains related to the hash in virustotal we can see that the answer is "dunyamuzelerimuzesi.com"

![DNS](https://github.com/FrancoGarciaC9701/Cibersecurity-Labs/blob/930842e7ff6c5b65bcdae691c0fd0a970fe7022c/BTLO/NetworkAnalysis-Ransomware/Images/NAR-DNS.png)
![DNS2](https://github.com/FrancoGarciaC9701/Cibersecurity-Labs/blob/5505afcb554691c81a2ce19ee7629a50449c868c/BTLO/NetworkAnalysis-Ransomware/Images/NAR-DNSVT.png)

✅ The Answer is: dunyamuzelerimuzesi.com

# ❓ Question (H) Decrypt the Tender document and submit the flag

For this step we are going to use Ransomware File Decryptor, it is compatible only with Windows, we download it from its official website https://success.trendmicro.com/en-US/solution/KA-0006362, unzip the file, start the application, when we have to choose the file type we choose TeslaCrypt V3/V4 and then the file to analyze which is tender.pdf.micro


![RMWTM](https://github.com/FrancoGarciaC9701/Cibersecurity-Labs/blob/b5dab043c72af80d6e8632412b5f900b59efee61/BTLO/NetworkAnalysis-Ransomware/Images/Screenshot%202025-08-26%20182739.png)
![FLAG](https://github.com/FrancoGarciaC9701/Cibersecurity-Labs/blob/b5dab043c72af80d6e8632412b5f900b59efee61/BTLO/NetworkAnalysis-Ransomware/Images/Screenshot%202025-08-26%20182637.png)

✅ The Answer is: BTLO-T3nd3r-Fl@g

Thank you for reading, any questions, corrections or suggestions are welcome. My contact channels are
francogarcia9701@gmail.com
https://www.linkedin.com/in/franco-garcia9701/
Thank you for reading, any questions, corrections or suggestions are welcome. My contact channels are
