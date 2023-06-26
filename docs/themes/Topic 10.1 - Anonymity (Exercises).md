
![[entropy_calculation_example.png]]
# Wieso wird hie /1000 und /10 grächnet?


## Explain the Dining Cryptographers Problem
Every two cryptographers establish a shared one-bit secret. Everyone then makes an XOR out of the two shared one-bit secrets and reveals the result.

- If they payed they invert the XOR
- If they didn't pay they just reveal the XOR of the shared one-bit secrets

Finally the revealed results are XORed aswell

- If the result is 1 then someone payed but this person stays anonymous
- If the result is 0 then the NSA payed
