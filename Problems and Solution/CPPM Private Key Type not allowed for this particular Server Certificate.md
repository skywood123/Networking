When uploading HTTPS certificate to CPPM, Error showing Private Key Type not allowed for this particular Server Certificate.
![image](https://github.com/user-attachments/assets/468bab40-005a-40e4-9e12-224d11d28595)

1. Check your certificate hashing algorithm, check whether its using RSA or ECC.
2. Upload to the correct usage. HTTPS(ECC) or HTTPS(RSA) based on your certificate algorithm.
![img2](https://github.com/user-attachments/assets/6c2ee116-9336-4e4f-96f3-990bbe75be1c)
![img1](https://github.com/user-attachments/assets/ae9c945a-5f28-4dae-a1c0-c95e698da873)
