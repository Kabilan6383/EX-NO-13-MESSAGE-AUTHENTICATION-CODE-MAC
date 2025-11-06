# EX-NO-13-MESSAGE-AUTHENTICATION-CODE-MAC

## AIM:
To implement MESSAGE AUTHENTICATION CODE(MAC)

## ALGORITHM:

1. Message Authentication Code (MAC) is a cryptographic technique used to verify the integrity and authenticity of a message by using a secret key.

2. Initialization:
   - Choose a cryptographic hash function \( H \) (e.g., SHA-256) and a secret key \( K \).
   - The message \( M \) to be authenticated is input along with the secret key \( K \).

3. MAC Generation:
   - Compute the MAC by applying the hash function to the combination of the message \( M \) and the secret key \( K \): 
     \[
     \text{MAC}(M, K) = H(K || M)
     \]
     where \( || \) denotes concatenation of \( K \) and \( M \).

4. Verification:
   - The recipient, who knows the secret key \( K \), computes the MAC using the received message \( M \) and the same hash function.
   - The recipient compares the computed MAC with the received MAC. If they match, the message is authentic and unchanged.

5. Security: The security of the MAC relies on the secret key \( K \) and the strength of the hash function \( H \), ensuring that an attacker cannot forge a valid MAC without knowledge of the key.

## Program:
~~~
#include <stdio.h>
#include <string.h>

unsigned char generateMAC(char message[], char key[]) {
    unsigned char mac = 0;
    int i;

    for (i = 0; i < strlen(message); i++)
        mac ^= message[i];

    for (i = 0; i < strlen(key); i++)
        mac ^= key[i];

    return mac;
}

int main() {
    char message[100], receivedMessage[100], key[50];
    unsigned char mac, receivedMAC, newMAC;

    printf("Enter the message: ");
    scanf("%s", message);

    printf("Enter the shared secret key: ");
    scanf("%s", key);

    mac = generateMAC(message, key);
    printf("\nGenerated MAC: %u\n", mac);

    printf("\n--- Receiver Side ---\n");
    printf("Enter the received message: ");
    scanf("%s", receivedMessage);

    printf("Enter the received MAC: ");
    scanf("%hhu", &receivedMAC);

    newMAC = generateMAC(receivedMessage, key);

    if (newMAC == receivedMAC)
        printf("\nMessage is authentic and unaltered.\n");
    else
        printf("\nMessage integrity verification failed.\n");

    return 0;
}
~~~



## Output:

<img width="1609" height="721" alt="Screenshot 2025-11-06 090143" src="https://github.com/user-attachments/assets/d914687e-0016-436c-b9df-1581b7feb2a0" />


## Result:
The program is executed successfully.
