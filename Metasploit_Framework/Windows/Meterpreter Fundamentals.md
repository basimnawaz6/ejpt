![[Pasted image 20250818124633.png]]
### What is a DLL?

- **DLL = Dynamic Link Library**
- Think of it like a **toolbox** that programs use.
- Instead of every program carrying all the tools inside itself, they just say:
   "Hey, I’ll borrow the `math.dll` toolbox when I need to do math stuff."
   
**Example:**
- When you open a game, it might use `graphics.dll` for graphics, `sound.dll` for audio, etc.
- This saves space and makes programs run smoother.
### What is DLL Injection?

- DLL injection is when someone **forces a program to use a DLL that wasn’t originally part of it.**
- Imagine you walk into a factory, and secretly replace one of their toolboxes with your own toolbox.
- Now the workers (the program) will use **your tools (DLL)** instead of the real ones.

## How Meterpreter Works

### 1. **Exploit the target**

- First, the attacker (or penetration tester) uses an **exploit** (a way to break into a system).  
    Example: exploiting a vulnerable web server, an outdated Windows service, or a weak password.


At this stage, the door is opened, but the attacker needs a way _in_.

---

### 2. **Payload is delivered**

- A **payload** is the code that actually runs on the victim once the exploit succeeds.
- Meterpreter is one of those payloads.
- Instead of just giving a basic shell (like CMD), Meterpreter gives a **fancy, powerful shell** with many built-in features.

This is like not just sneaking into a house, but also setting up hidden cameras and tools inside.

---

### 3. **Runs in memory**

- Once delivered, Meterpreter loads itself **directly in RAM** (no file written on disk).
- This makes it **stealthy** (as we discussed earlier).

Like entering the house but not leaving any footprints on the floor.

---

### 4. **Establishes a connection back**

- Meterpreter usually connects back to the attacker’s system (reverse connection).   
- Example: Victim → Attacker (on port X).
- This gives the attacker control.
 Like calling the thief and saying: “I’m inside, what should I do next?”

---

### 5. **Interactive control**

Once the connection is made, the attacker can:

- **Explore files** (`ls`, `download`, `upload`)
- **Gather info** (`sysinfo`, `getuid`)
- **Spy** (screenshots, webcam, keylogger)
- **Pivot** (use this machine to attack others on the same network)
- **Stay persistent** (set up so it survives reboot, if attacker wants)

This is the “toolbox” part: you don’t just get in, you get _lots_ of tools ready to use.

Basic session management in msf:
![[Pasted image 20250820092604.png]]
check basic commands:
![[Pasted image 20250820093808.png]]
![[Pasted image 20250820093853.png]]