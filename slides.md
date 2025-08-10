---
theme: frankfurt
title: Welcome to Slidev
date: 2025/6/31
class: text-center
drawings:
  persist: true
mdc: true
author: Tianyi Wang
fonts:
  sans: '"Times New Roman","Microsoft YaHei",sans-serif'
  mono: 'Fira Code'
css: unocss
---

# Key Management and the Public-Key Revolution

<div class="pt-4 text-2xl">
  Tianyi Wang<br>
  Fujian Normal University<br>
  August 7 2025
</div>

---
section: Motivation
---

# The Prerequisite of Private-Key Cryptography

- Private-key cryptography is used to ensure secrecy and integrity for two communicating parties.

- Its security is entirely dependent on the foundational assumption that both parties **already possess a shared, secret key**.

- This introduces a fundamental logistical problem: How can the parties securely share this secret key in the first place? 

- Sending the key over an insecure communication channel is not a solution, as an eavesdropper would simply intercept it.

<img src=".\img\鸡蛋.png" alt="Logo" width="500" style="position: absolute; bottom: 30px; left: 50%; transform: translateX(-50%); z-index: 1;" />

---

# Limitations of Traditional Key Distribution

- Traditional solutions rely on establishing a temporary secure channel, like a physical meeting or a trusted courier service.

- While functional, these approaches do not scale for large, modern organizations where any pair of employees might need to communicate securely.

- In a network of N employees, each individual would need to securely store and manage N-1 unique keys, creating a logistical nightmare.

- These methods are completely non-viable for "open systems" like the internet, which involve transient interactions between strangers.

<img src=".\img\面对面.png" alt="Logo" width="240" style="position: absolute; bottom: 30px; left: 35%; transform: translateX(-50%); z-index: 1;" />

<img src=".\img\钥匙.png" alt="Logo" width="240" style="position: absolute; bottom: 30px; left: 65%; transform: translateX(-50%); z-index: 1;" />

---
section: One solution - KDC
---

# The Role of a Key-Distribution Center (KDC)

- A KDC is a single, trusted entity that is responsible for establishing pairwise keys for all users within an organization.

- Each user only needs to store and protect one long-term secret key—the one shared with the KDC.

- When a user (Alice) wants to talk to another (Bob), she requests a key from the KDC.

- The KDC generates a new, random "session key" for that specific conversation, which is discarded afterward.

<img src=".\img\KDC.png" alt="Logo" width="500" style="position: absolute; bottom: 30px; left: 50%; transform: translateX(-50%); z-index: 1;" />

---

# KDC Protocol Flow and Drawbacks

- In a typical protocol like Needham-Schroeder, the KDC sends the session key encrypted for Bob to Alice.

- This encrypted portion is called a "ticket," which Alice then forwards to Bob to initiate communication.

- Drawback 1: **Single Point of Failure**. If the KDC goes offline, no one can establish new secure sessions.

- Drawback 2: **High-Value Target**. A compromise of the KDC would allow an attacker to decrypt all network traffic, breaking the entire system.

<img src=".\img\Needham-Schroeder.png" alt="Logo" width="500" style="position: absolute; bottom: 30px; left: 50%; transform: translateX(-50%); z-index: 1;" />


---
section: Breakthrough - DH Protocol
---

# A New Paradigm for Key Exchange

- In their 1976 paper, Diffie and Hellman proposed a method to achieve private communication without any pre-existing private channel.

- The core idea is to leverage mathematical operations that are asymmetric: easy to perform in one direction but extremely difficult to reverse.

- An example is multiplying two large prime numbers (easy), versus finding the original prime factors from their product (difficult).

- This concept was revolutionary, suggesting two people could create a shared secret by communicating only over a public channel.

---

# Security and Vulnerability of Diffie-Hellman

- Security against a passive eavesdropper relies on the hardness of the **Decisional Diffie-Hellman (DDH) problem**.

- The DDH assumption states that it is computationally infeasible to distinguish the computed key $g^{xy}$ from a truly random element in the group G.

- However, the basic protocol is **completely insecur**e against an active **man-in-the-middle attack**.

- An adversary can intercept the communication, establish a separate key with Alice and another with Bob, and relay messages between them, undetectably.

---
section: The Public-Key Revolution
---

# Public-Key Cryptography: The Revolution

- Public-key (or asymmetric) cryptography, also introduced by Diffie and Hellman, uses a pair of keys for each user: one public, one private.

- The public key is designed to be widely distributed, while the private key must be kept secret by its owner.

- This asymmetry enables two powerful new cryptographic primitives: Public-Key Encryption and Digital Signatures.

- This was the catalyst that moved cryptography from a niche government tool to a widespread commercial technology.

---

# Application 1: Public-Key Encryption

- To send a secret message, a sender uses the **receiver's public key** to encrypt it.

- Once encrypted, only the receiver, using their corresponding **private key**, can decrypt and read the message.

- The security holds even if an adversary knows the public key used for encryption, which is a remarkable property.

- This effectively solves the key distribution problem for confidential communication.

---

# Application 2: Digital Signatures

- To prove authenticity, a sender uses their **own private key** to generate a unique signature for a document.

- Anyone in the world can then use the sender's **public key** to verify that the signature is valid.

- This provides message integrity and authenticity, proving who sent the message and that it has not been altered.

- Crucially, it enables **non-repudiation**: the sender cannot later deny having signed the document, a property vital for contracts and e-commerce.

---

# Why Do We Still Need Private-Key Cryptography?

- While public-key cryptography is more powerful, private-key cryptography is orders of magnitude more efficient and faster.

- For applications involving large amounts of data, such as full disk encryption or streaming video, private-key crypto is the only practical choice.

- Modern systems use a **hybrid approach**: public-key cryptography is used to securely establish a shared, temporary private key.

- This private key (or session key) is then used for the actual high-speed encryption of bulk data.

---
layout: center
class: text-center
---

<div class="h-6"></div>

# Thank You / Q&A

<div class="mt-6"></div>

<table class="bg-blue-50 rounded-lg shadow-sm border border-blue-100 mx-auto" style="width: 400px; max-width: 75%;">
  <tbody>
    <tr>
      <td class="px-6 py-3">
        <b>GitHub:</b> <a href="https://github.com/coperlm" class="text-blue-600">https://github.com/coperlm</a>
      </td>
    </tr>
    <tr>
      <td class="border-t border-blue-100 px-6 py-3">
        <b>Email:</b> <a href="mailto:TyWang2005@outlook.com" class="text-blue-600">TyWang2005@outlook.com</a>
      </td>
    </tr>
  </tbody>
</table>