## EX 13 : IMPLEMENTATION OF MESSAGE AUTHENTICATION CODE(MAC)


## AIM:

To implement a Message Authentication Code (MAC) using a shared secret key and a hash function to verify the integrity and authenticity of a message.


## ALGORITHM:

1.	Choose a shared secret key that will be known to both the sender and the receiver.
2.	Define the message that needs to be authenticated.
3.	Concatenate the message and the secret key to form a new string.
4.	Apply a hash function (e.g., simple XOR-based hash or any secure hashing function like SHA) to the concatenated string to generate the MAC.
5.	Send the message along with the generated MAC.
6.	For verification, the receiver uses the same shared key, concatenates it with the received message, and applies the hash function to generate a new MAC.
7.	Compare the generated MAC with the received MAC. If they match, the message is authentic; otherwise, it has been tampered with.


## PROGRAM:
```
#include <stdio.h>
#include <string.h>

#define MAC_SIZE 32 // Define MAC size in bytes

// Function to compute a simple MAC using XOR
void computeMAC(const char *key, const char *message, char *mac) {
    int key_len = strlen(key);
    int msg_len = strlen(message);
    
    // XOR the key and message, repeating if necessary
    for (int i = 0; i < MAC_SIZE; i++) {
        mac[i] = key[i % key_len] ^ message[i % msg_len]; // Simple XOR operation
    }
    mac[MAC_SIZE] = '\0'; // Null-terminate the MAC string
}

int main() {
    char key[100], message[100];
    char mac[MAC_SIZE + 1]; // Buffer for MAC (+1 for null terminator)
    char receivedMAC[MAC_SIZE + 1]; // Buffer for input of received MAC

    // Step 1: Input secret key
    printf("Enter the secret key: ");
    scanf("%s", key);

    // Step 2: Input the message
    printf("Enter the message: ");
    scanf("%s", message);

    // Step 3: Compute the MAC
    computeMAC(key, message, mac);

    // Step 4: Display the computed MAC in hexadecimal
    printf("Computed MAC (in hex): ");
    for (int i = 0; i < MAC_SIZE; i++) {
        printf("%02x", (unsigned char)mac[i]); // Print each byte as hex
    }
    printf("\n");

    // Step 5: Input the received MAC (for verification)
    printf("Enter the received MAC (as hex): ");
    for (int i = 0; i < MAC_SIZE; i++) {
        scanf("%02hhx", &receivedMAC[i]);
    }

    // Compare the computed MAC with the received MAC
    if (memcmp(mac, receivedMAC, MAC_SIZE) == 0) {
        printf("MAC verification successful. Message is authentic.\n");
    } else {
        printf("MAC verification failed. Message is not authentic.\n");
    }

    return 0;
}
```


## OUTPUT:
<img width="1553" height="647" alt="image" src="https://github.com/user-attachments/assets/cca04651-4873-4220-9c82-7be780a79e17" />

 
## RESULT:

The Message Authentication Code (MAC) was implemented successfully, allowing the verification	of	message	integrity	and	authenticity	using	a	shared	secret	key.
