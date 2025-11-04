# 🦆 v1t CTF Write-Up

---

## **DUCK**

### **1. Rules**
The flag was hidden directly in the challenge rules.

---

### **2. Lucky Ducky**
Visited my profile on the challenge website, clicked on my team name below my username, and a pop-up appeared revealing the *Lucky Flag*.

---

## **CRYPTO**

### **1. Misconfigured RSA**
The RSA setup used a **prime modulus** `n`, which is a misconfiguration.

**Steps to decrypt:**
1. Compute \( \phi(n) = n - 1 \)
2. Find the private exponent  
   \( d = e^{-1} \mod \phi(n) \)  
   (use the extended Euclidean algorithm or `pow(e, -1, phi)` in Python)
3. Decrypt the ciphertext:  
   \( m = c^d \mod n \)
4. Convert `m` to bytes:  
   ```python
   m.to_bytes((m.bit_length() + 7) // 8, 'big')
   ```
5. Decode as ASCII to retrieve the flag.

*(Used GPT for assistance here.)*

---

## **OSINT**

### **1. Among USniversity**
Reverse image search revealed it as the *University of Information Technology*, so the flag was:

```
v1t{UIT}
```

---

### **2. Forgotten Inventory**
The riddle hinted at WikiLeaks’ **2007 "Iraq OIF Property List"** CSV file.  

- Found the dataset and clicked on *file details*.  
- There, I located an email ID within the metadata.  

**Flag:**
```
v1t{david.j.hoskins@us.army.mil}
```

*(Got the WikiLeaks hint from GPT.)*

---

### **3. Duck Company**
Reverse-searched the given image and found the original company’s website:
```
dcuk.com
```

---

## **WEB**

### **1. Login Panel**
- Obtained the login panel’s HTML file from the challenge.  
- Found two **hardcoded SHA-256 hashes** for the username and password.  
- Cracked the password hash online → `p4ssw0rd`.  
- Guessed username `v1t` (based on flag format).  
- Verified its hash match and logged in.

**Flag:**
```
v1t{p4ssw0rd}
```

*(Got some help from GPT here too.)*

---

### **2. Stylish Flag**
- Downloaded `index.html` and its CSS file from GitHub.  
- Opened locally in Firefox.  
- Removed the `"hidden"` attribute near the flag element.  
- The flag appeared upside down — unchecked the CSS `transform` property to read it properly.

---

### **3. Tiny Flag**
- Derived GitHub link: [github.com/tommytheduck](https://github.com/tommytheduck)  
- Found the **Tiny Flag** repository.  
- Zoomed into `favicon.ico` — flag hidden inside the icon.

---

### **4. Mark the Lyrics**
Downloaded the webpage HTML from GitHub and found fragments of the flag hidden in `<mark>` tags throughout the lyrics.

| Fragment | Source |
|-----------|---------|
| **V** | `{<mark>V</mark>erse <mark>1</mark>: Sơn Tùng M-<mark>T</mark>P}` |
| **1** | same as above |
| **T** | same as above |
| **{** | `<mark>{</mark>Pre-Chorus: Sơn Tùng M-TP}` |
| **MCK** | `{Chorus: RPT <mark>MCK</mark>, Sơn Tùng M-TP}` |
| **-pap-** | `pap<mark>-pap-</mark>pap-pap` |
| **cool** | `Nháy mắt <mark>cool</mark> cool, sợ đéo gì phốt ghẻ` |
| **-ooh-** | `ooh<mark>-ooh-</mark>ooh-ooh` |
| **yeah** | `Yeah, <mark>yeah</mark>, yeah` |
| **}** | `{Outro: Sơn Tùng M-TP, RPT MCK, RPT TC<mark>}</mark>` |

**Final Flag:**
```
v1t{MCK-pap-cool-ooh-yeah}
```