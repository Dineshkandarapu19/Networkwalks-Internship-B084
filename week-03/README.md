
# Week 03 – PM1: Password Cracking with John the Ripper

## 1. Project Overview

This project was completed as part of the NetworkWalks Cybersecurity Internship (Batch B084).

The objective was to understand and perform password recovery on an assigned password-protected PDF using John the Ripper (JTR) in Kali Linux.

The practical demonstrates how password hashes can be extracted from protected PDF files and tested against candidate passwords using a dictionary attack.

## 2. Objectives

- Understand password hashing and dictionary attacks.
- Verify John the Ripper installation in Kali Linux.
- Extract a PDF password hash using pdf2john.
- Perform a dictionary attack using a wordlist.
- Verify the recovered password.
- Open the protected PDF using the recovered password.
- Document the practical workflow and results.

## 3. Lab Environment

| Component | Details |
|---|---|
| Operating System | Kali Linux |
| Virtualization | Oracle VirtualBox |
| Password Recovery Tool | John the Ripper |
| Hash Extraction Tool | pdf2john |
| Attack Type | Dictionary Attack |
| Target File | My Locked PDF1.pdf |
| Wordlist | rockyou.txt |
| Working Directory | ~/week3-jtr |

## 4. Tools Used

### John the Ripper

John the Ripper is an open-source password security auditing and recovery tool. It supports multiple hash formats and password recovery techniques.

### pdf2john

pdf2john is a utility included with John the Ripper Jumbo that extracts password-verification data from protected PDF files into a format that John can process.

### Wordlist (rockyou.txt)

A wordlist is a collection of candidate passwords used during dictionary attacks.

The rockyou.txt wordlist available in Kali Linux was used in this practical.

### Kali Linux

Kali Linux is a Debian-based Linux distribution containing tools commonly used for cybersecurity testing and security auditing.

## 5. Practical Implementation

### Step 1: Verify John the Ripper Installation

Command:

```bash
john --list=build-info
```

John the Ripper was available in Kali Linux.

### Step 2: Verify PDF Hash Support

Command:

```bash
john --list=formats | grep -i pdf
```

Output confirmed that the PDF hash format was supported.

### Step 3: Prepare Lab Files

The assigned PDF was accessed through the VirtualBox shared folder.

The PDF was copied into the working directory.

Commands:

```bash
mkdir -p ~/week3-jtr
cd ~/week3-jtr
cp "/downloads/My Locked PDF1.pdf" .
ls -lh
```

The following file was available in the working directory:

- My Locked PDF1.pdf

### Step 4: Extract the PDF Hash

Command:

```bash
perl /usr/share/john/pdf2john.pl "My Locked PDF1.pdf" > hash1.txt
```

Explanation:

- `pdf2john.pl` extracts the PDF password hash.
- The quoted filename specifies the target PDF.
- `>` redirects the extracted hash into `hash1.txt`.

The extracted hash was verified using:

```bash
head -c 300 hash1.txt
```

The PDF hash was successfully extracted and saved.

### Step 5: Perform Dictionary Attack

Command:

```bash
john --format=PDF --wordlist=/usr/share/wordlists/rockyou.txt hash1.txt
```

Explanation:

- `john` starts the password recovery process.
- `--format=PDF` specifies the PDF hash format.
- `--wordlist` specifies the candidate password dictionary.
- `hash1.txt` contains the extracted PDF hash.

John successfully loaded one PDF password hash and tested candidate passwords from the wordlist.

### Step 6: Display Recovered Password

Command:

```bash
john --show --format=PDF hash1.txt
```

Result:

```text
My Locked PDF1.pdf:good-luck

1 password hash cracked, 0 left
```

Result: Password successfully recovered.

### Step 7: Verify PDF Access

Command:

```bash
xdg-open "My Locked PDF1.pdf"
```

The recovered password was entered to open the protected PDF.

The PDF opened successfully, confirming that the recovered password was correct.

## 6. Final Results

| Task | Result |
|---|---|
| John the Ripper availability | Successful |
| PDF format support verification | Successful |
| PDF hash extraction | Successful |
| Dictionary attack | Successful |
| Password recovery | Successful |
| PDF access verification | Successful |

**Recovered Password:** `good-luck`

**Hashes Cracked:** 1/1

**Remaining:** 0

## 7. Screenshots and Evidence

The following screenshots document the practical:

 John the Ripper installation verification.
   <img width="1920" height="982" alt="john-version" src="https://github.com/user-attachments/assets/34a4c109-6276-4c6e-bd43-306df8d15d81" />

 PDF file inside the working directory.
 PDF hash extraction using pdf2john.
 <img width="1920" height="982" alt="PDF hash extraction using pdf2john" src="https://github.com/user-attachments/assets/1cc7396a-8f2e-406f-a8c0-d80f0c366243" />

 Extracted hash saved in hash1.txt.
 <img width="1920" height="982" alt="pdf-hash-extraction" src="https://github.com/user-attachments/assets/00288c47-26f4-46a8-bea7-7d4962ed9842" />

 John the Ripper dictionary attack.
 <img width="1920" height="982" alt="password-obtained" src="https://github.com/user-attachments/assets/76b13a60-5bf8-43aa-aa9f-43da7afaf953" />

 Terminal showing the recovered password.
 Successful opening of the protected PDF.
 <img width="1920" height="982" alt="pdf-flag-captured" src="https://github.com/user-attachments/assets/30239092-2c07-41b6-9e2e-acc67ee71351" />


## 8. Key Learnings

Through this practical, I learned:

- How password-protected PDFs use password-verification data.
- How to extract PDF hashes using pdf2john.
- How dictionary attacks work.
- How John the Ripper processes candidate passwords.
- How to use wordlists for password recovery.
- How to specify the PDF hash format.
- How to verify recovered passwords using John the Ripper.
- How to validate password recovery by opening the protected PDF.

An important takeaway was understanding that a password hash is not the original password. Password recovery tools test candidate passwords against the extracted hash.

## 9. Conclusion

This practical provided hands-on experience with password recovery using John the Ripper in Kali Linux.

I successfully accessed the assigned PDF, extracted its password hash using pdf2john, performed a dictionary attack using the rockyou.txt wordlist, recovered the correct password, and verified access to the protected document.

The exercise improved my understanding of password security, hash extraction, dictionary attacks, and Linux-based cybersecurity tools.

---

**Internship:** NetworkWalks Cybersecurity Internship  
**Batch:** B084  
**Week:** 03  
**Project Module:** PM1 – Password Cracking with John the Ripper  
**Status:** Completed

