# CS2160-Project3
Project 3 is mainly focused on preventing overflow cyber attacks using canary stack and forcing a method to work


In your README report, include the stack canary value you added to main() as both the 
printable string, and as a hexadecimal value. Show a screenshot of your QtRVSim 
window showing the register window when reproducing the attack from Project 2 Part 3 
that calls sekret_fn through the buffer overflow. 

<img width="1440" alt="Screen Shot 2024-05-03 at 8 30 52 PM" src="https://github.com/Yabi-real/CS2160-Project3/assets/111730954/f9c91279-620e-4358-877a-e5201f0c4884">

# Define the stack canary value as a printable ASCII string 

canary_value: .ascii "CANARY" 

# Define the stack canary value as a Hexadecimal 

canary_value: .byte 0x43, 0x41, 0x4E, 0x41, 0x52, 0x59 

 

The screenshot was the best I could come up with just trying to do it on my own. 

Part 2: 
Include a copy of your input string in your README. Provide a screenshot of QtRVSim
showing the values of the registers and the terminal window when you have successfully
called sekret_fn(). Assuming the attacker has a copy of your program, is there any stack
canary value that you could use that would prevent the attack from succeeding, or that
would make the attack more challenging? Briefly explain your reasoning.
<img width="1440" alt="Screen Shot 2024-05-03 at 9 05 17 PM" src="https://github.com/Yabi-real/CS2160-Project3/assets/111730954/d8223604-7e48-46d8-bf14-d216d49e47bc">


input_string:
    .ascii "AAAA"          # Fill the buffer until the canary
    .ascii "CANARY"        # Stack canary value
# Define the stack canary value as a printable ASCII string
canary_value: .ascii "CANARY"

# Define the prompt and sekret_data sections
.data
prompt:   .ascii  "Enter a message: "
prompt_end:
sekret_data:
#.word 0x73564753, 0x67384762, 0x79393256, 0x3D514762, 0x0000000A
.word 0x0804a030       # Address of sekret_fn

# this is the code that will oveflow then try to go through the method inside sekret_fn()
AAAAAAAAAAAAAAAAAAAAAAAAAAAA
BBBB\x30\xa0\x04\x08

To make the attack more challenging or prevent it altogether, you can use a strong and unpredictable stack canary value. Some approaches to selecting a stack canary value include:

Randomly Generated Canary: Generate a random canary value at runtime and place it on the stack. Since the attacker won't know the value in advance, it becomes much harder to craft a successful exploit.
Sentinel Value: Use a predefined but non-predictable value as the canary. This value should be known only to the system and should change every time the program runs.
Stack Canary Relocation: Move the location of the stack canary within the stack frame. This makes it harder for the attacker to predict where the canary is located and thus harder to overwrite it accurately.
Multiple Canary Values: Use multiple canary values throughout the stack, making it even more difficult for an attacker to predict and overwrite all of them correctly.
Canary Value Encryption: Encrypt the canary value using a key known only to the system. Decrypt it before using it in comparisons. This adds an extra layer of protection against attackers who might inspect memory.
