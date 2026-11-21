# Week 3 Report

Pentester: Muhammad Abdul Hanan
Program/Batch: B084M - Networkwalks
Date: 21 November 2026
Modules completed: W3-PM1 (Password Cracking with JTR), W3-PM2 (Password Cracking with NW Tools)
Target: My Locked PDF1.pdf and My Locked PDF1 (for NW Tools Lab WK3-PM2).pdf, lab files from the internship
Permission: Yes, internship lab files only.

## 1. Liability Disclaimer

I did these activities only on files I own or where I had written permission. All material is for education and research only.

## 2. Introduction

This report covers cracking the password of two locked PDF files. PM1 uses John the Ripper. PM2 uses the Networkwalks Hash Calculator and Password Cracker web tools. Both files use the Standard security handler, Revision R4, Version V4, 128 bit key.

## 3. Tools Used

John the Ripper jumbo 1.9.0, pdf2john hash format, Networkwalks Hash Calculator, Networkwalks Password Cracker, default wordlist.

## 4. Activities

### 4.1 PM1 - Password Cracking with JTR

Run on 21 November 2026. Screenshots in screenshots/ 1 to 4.

- File: My Locked PDF1.pdf, 267 KB. Standard handler, R4, V4, 128 bit, permissions -1028.
- I extracted the hash in pdf2john format: $pdf$4*4*128*-1028*1*16*ca7f72f11459cba469f1005a8765ed51*32*f32d8fa1bfbe2648226dffc39f7909ea0021446990b9e4114071a4d9104984c1*32*9322f50c29569712067a775264635e4954ccb1b99e209d664984054ffad30a6a
- John ran with the default wordlist. It loaded 1 password hash, PDF format, revision 4. Cracked in under a second. Password: good-luck.
- john --show confirmed it: ?:good-luck, 1 password hash cracked, 0 left.
- I opened the PDF with the password to check it. good-luck opened it. password1 did not open it. The guide says the password is password1, but that is wrong for this file. I trusted the crack, not the guide.
- Problem faced: the john that comes with Ubuntu has no PDF format. I built John the Ripper jumbo 1.9.0 from source. The build failed on blake2.h with GCC, the struct alignment in that file is wrong for new compilers. I fixed the alignment in blake2.h and the build finished. After that john listed PDF as a format.

### 4.2 PM2 - Password Cracking with NW Tools

Run on 21 November 2026. Screenshots in screenshots/ 5 to 8.

- File: My Locked PDF1 (for NW Tools Lab WK3-PM2).pdf, 65 KB. Standard handler, R4, V4, 128 bit, permissions -1060.
- Hash Calculator read the file and gave the hash: $pdf$4*4*128*-1060*1*16*55d1a5c14175da449753199e44971d32*32*777fd021a7f3c5ae598c0c6495c7f76e00000000000000000000000000000000*32*ceecdac74b19b5a62688d3b3524e1374c955cbb9cc3c45316494d9446ef81af1. Revision R4, Version V4, 128 bit. The hash it gave is the same one I extracted for John.
- Password Cracker tried its built in list of 100 passwords. It found a match at 91 out of 100. Password: password1. The page showed PASSWORD CRACKED SUCCESSFULLY.
- I also cracked the same file with John. Same answer, password1. john --show confirmed it: ?:password1, 1 password hash cracked, 0 left.

## 5. Risk Analysis

Findings are observations from cracking lab files, not confirmed vulnerabilities. No active exploitation was done.

- Both passwords are plain dictionary words, good-luck and password1. John cracked each in under a second. A password like this protects nothing. Risk: High, for any real file locked with a word like this.
- PDF R4 with a 128 bit key is old protection. It depends fully on the password being strong. With a weak password the encryption does not help. Risk: Medium.
- The guide said the PM1 password is password1, but the real password is good-luck. A guide can be wrong. Always test the result yourself, by opening the file. Risk: Low, but it cost time.
- The Networkwalks web tools work without installing anything, and the hash they gave matched my own extraction exactly. Good for a quick check, but a web tool should only be used on files you are allowed to test. Risk: Low.

## 6. Recommendations

Use long random passwords, not dictionary words. Use a password manager so you do not have to remember them. Do not trust a password just because a file is locked, the lock is only as strong as the password. Test your own result before you report it.

## 7. Conclusion

I cracked two locked PDFs two ways. With John the Ripper I cracked the PM1 file, password good-luck, and the PM2 file, password password1. With the Networkwalks web tools I cracked the PM2 file again, same answer. I learned how a PDF password is stored as a hash, how to pull that hash out, and how fast a weak password falls to a wordlist. The main lesson is simple: a short common password is no protection at all.

## 8. Evidence

- 1-pdf-hash.png - extracted hash of the PM1 file in pdf2john format
- 2-john-crack-pm1.png - John cracking the PM1 file, password good-luck
- 3-john-show-pm1.png - john --show, good-luck, 1 password hash cracked
- 4-verify-decrypt.png - opening the PM1 file, good-luck works, password1 does not
- 5-john-crack-pm2.png - John cracking the PM2 file, password password1
- 6-hash-calculator.png - Hash Calculator result for the PM2 file
- 7-password-cracker.png - Password Cracker result, PASSWORD CRACKED SUCCESSFULLY, password1
- 8-cracker-hash-pasted.png - the hash pasted in the Password Cracker, built in list of 100 words
