# Definition

In the world of computing, a **Server** is a specialized computer or software program that provides a service to another computer or program, known as the **Client**. 

This relationship is the foundation of the [[Client-Server Model]], which governs almost everything we do online from sending an email to streaming a movie.

# What Makes a Computer a "Server"?

Technically, almost any computer can act as a server if it has the right software installed. However, in a professional or [[Cloud Computing]] context, servers differ from "Desktop" computers in several ways:

---

## The Role

- Adesktop computer is designed for a single human user (running a browser, games, or office tools).

- A server is designed to sit and wait for "requests" from thousands of other computers simultaneously.

## **The Hardware:

Servers are built for **Reliability** and **Uptime**. They often have:

>[!NOTE] Redundant Power Supplies 
>- If one fails, another takes over instantly.
>    
>	- **ECC RAM:** Error-Correcting Code memory that can detect and fix data corruption on the fly.
>	- **High Core Counts:** Specialized [[CPU|CPUs]] (like Intel Xeon or AMD EPYC) designed to handle many tasks at once.

>[!NOTE] The [[Operating System|OS]] 
>- They run server-specific operating systems (like **[[Linux]] Ubuntu Server**, **[[Windows]] Server**, or **[[RHEL]]**) which lack a fancy visual interface to save [[Compute]] resources.

# Types of Servers

Servers are often named after the specific job they perform:

- **[[Web Server]]:** Delivers website content ([[HTML]], [[CSS]], images) to your browser (e.g., [[Apache]], [[Nginx]]).

- **[[Database Server]]:** Stores and manages structured data (e.g., [[MySQL]], [[PostgreSQL]], [[MongoDB]]).

- **[[Application Server]]:** Runs the actual "logic" of an app—like calculating a bank balance or processing a video.

- **[[File Server]]:** A central location for storing and sharing files within a network.

- **[[DNS Server]]:** The "phonebook of the internet" that translates names like `google.com` into [[IP Address|IP addresses]].

- **[[Mail Server]]:** Handles the sending and receiving of emails.

# Physical vs. Virtual Servers

In the past, one "Server" meant one physical metal box in a closet. Modern computing has changed this:

## Bare Metal Servers

This is a physical machine dedicated entirely to one user. 

>It offers the highest performance because there is no "middleman," but it is slow to set up and expensive.

## [[Virtual Private Server]] (VPS)

Using a technology called a **[[Hypervisor]]**, a single powerful physical server is "sliced" into many smaller virtual servers. Each slice thinks it is an independent machine. This is the basis of most cloud computing.

## [[Serverless]]

The most modern evolution. You don't manage a "server" at all. You just give the [[Cloud Computing|cloud]] provider your code, and they create a temporary server environment to run it for a fraction of a second, then delete it.

# The [[Ports]] Concept

Servers use **Ports** to distinguish between different services running on the same machine. 

Think of the server's [[IP Address|IP address]] as the building address and the Port as the specific apartment number:

- **Port 80/443:** Reserved for Web traffic (HTTP/HTTPS).

- **Port 22:** Reserved for [[SSH]] (Secure Shell) to remotely control the server.

- **Port 25:** Reserved for Email (SMTP).

# Common Misconceptions

- **"Servers are always in the Cloud":** Not true. Many companies still maintain "On-Premises" servers in their own offices for security or speed.

- **"A server is just a fast PC":** While they are fast, their real strength is **Throughput** (handling many small tasks) rather than just "speed" (completing one task quickly).

- **"If the server is off, the data is gone":** No. The data is stored in persistent [[Storage]]. When the server turns back on, it retrieves the data and starts serving it again.

# The Lifecycle of a Request

1. **Request:** Your phone (Client) asks for a photo.

2. **Listening:** The Server is "listening" on a specific port. It accepts the connection.

3. **Processing:** The Server's [[Compute]] resource finds the photo in [[Storage]].

4. **Response:** The Server sends the data back to your phone.

5. **Close:** The connection is closed, and the server waits for the next request.
# Tags

#servers #infrastructure #backend #networking #hardware #learning