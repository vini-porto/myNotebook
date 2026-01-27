Imagine if every car company made cars that only worked on their own roads. Chaos! Networks need rules too. These rules are called **networking models**.

Without standards, your iPhone couldn't talk to your Windows laptop. Companies would build walls around their products on purpose.

---
## The OSI Model - Seven Layers of Communication

Think of the OSI model like a post office with seven departments. Each department has one job. When you mail a letter, it goes through all seven departments in order.

### 7 - Application (Software)

- This is you writing the letter. It's where humans interact with computers. Web browsers, email, file transfers - this is where it all starts.
- Where users interact with applications, like email or web browsers
- HTTP, HTTPS, FTP, and DNS are exemples of 7 layer protocols

### 6 - Presentation (Software)

- This layer translates your letter into a language the postal system understands. It handles encryption (secret codes) and compression (making things smaller).
- Responsible for translating data between the application layer and the network format.
- Encryption and decryption

### 5 - Session (Software)

- This layer manages conversations. It's like a phone operator connecting calls and making sure people take turns talking.
- Controls dialogues(sessions) between communications hosts.

**The Top Three Layers** - Network administrators don't usually mess with these. That's the programmer's job.

---

### 4 - Transport

This layer breaks big letters into smaller envelopes. It numbers each piece so they can be put back together correctly. It's like sending a big package in multiple boxes with tracking numbers.

- Segments and reassembles data for communications between end hosts.
- Ensures data arrives correctly and in the right order.

**Two Main Protocols:**

- **TCP** - Reliable but slow. Like registered mail with receipts.
- **UDP** - Fast but unreliable. Like regular mail - sometimes it gets lost.

<aside> 💡

Port Numbers

</aside>

### 3 - Network (Hardware)

- This layer figures out the address and best route between cities. It uses IP addresses - like zip codes for computers. Routers work here.
- Routers operate at this layer
- Figure out the best path for data to travel between different networks.
- Provide logical addressing (IP addresses). Provides path selection between source and destination.

<aside> 💡

IP Address

</aside>

### 2- Data-Link (Hardware)

- This layer handles local delivery - like a mailman delivering on one street. It uses MAC addresses - like house numbers. Switches work here.
- Switches operate at this Layer
- Helps devices on the same network talk to each other directly.
- Detects and (possibly) corrects physical layer errors.
- Uses Layer 2 addressing (MAC Addresses), separate from layer 3 addressing.

<aside> 💡

MAC Address

</aside>

### 1 - Physical (Hardware)

- This is the actual roads, trucks, and mailboxes. Cables, WiFi signals, voltage levels. The physical stuff you can touch.
- Digital bits are converted into eletrical (for wired connections) or radio (for wireless connections) signals
- This layer is about the actual cables, Wi-Fi, or other means that connect devices.

## Layer Interaction

- Communication between the same layer on different devices or systems. This type of interation enables devices to exchange data and coordinate actions.

## PDUS

- Protocol Data Unit is the specific term for the data unit at each layer of the model.

## The Wrapping Process - Encapsulation

![image.png](attachment:9eae4ae1-2a7c-4ef6-9b42-fe84f08c45b5:image.png)

Imagine wrapping a gift multiple times:

1. Start with your data (the gift)
2. Layer 4 wraps it in a box (adds transport info)
3. Layer 3 puts it in a shipping box (adds routing info)
4. Layer 2 puts a shipping label on it (adds local delivery info)
5. Layer 1 puts it on a truck (converts to electrical signals)