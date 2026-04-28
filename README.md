# Cryptanalysis-of-Cross-Coupled-Chaotic-Maps-Multi-Image-Encryption-Scheme
Multiple grayscale image encryption using cross-coupled chaotic maps : 

1. Key Generation : 
The keys (initial parameters for two PWLCM systems) used in encryption scheme are derived 
from the hash value obtained using the SHA-256 algorithm on the combined multiple k input 
images. The resulting 256-bit hash value (hv1, hv2, …, hv256) is converted into 64 hexadecimal 
values (hd1, hd2, …, hd64), and the keys are generated using the Eq. 
The key generation equations are defined as follows: 
x(1) = xm − α1 − [α1] × 0.01 
ux = xx1 − α2 − [α2] × 0.01 
y(1) = ym − β1 − [β1] × 0.01 
uy = yx1 − β2 − [β2] × 0.01 
where, 
xm = 0.25686446985353 and xx1 = 0.35488659076447 
ym = 0.26457834689785 and yx1 = 0.36789543267894 
α1 = (hd1 + hd2 + … + hd16) × 10^-15 
α2 = (hd17 + hd18 + … + hd32) × 10^-15 
β1 = (hd33 + hd34 + … + hd48) × 10^-15 
β2 = (hd49 + hd50 + … + hd64) × 10^-15

2. PWLCM Cross-Coupled System Description :
   
Encryption/decryption scheme uses two PWLCM in a cross-coupled manner, as shown in Fig. 1. 
The output of PWLCM system-1 is utilized as an input for PWLCM system-2, and the output of 
PWLCM system-2 is utilized as an input for PWLCM system-1. The mathematical expression for 
the PWLCM system used in Patro’s et al. scheme is described as follows: 
σ(n+1) = f(σ(n), a), where: 
If 0 ≤ σ(n) < a, then σ(n+1) = σ(n) / a 
If a ≤ σ(n) < 0.5, then σ(n+1) = (σ(n) − a) / (0.5 − a) 
If 0.5 ≤ σ(n) < 1, then σ(n+1) = f(1 − σ(n), a) 
where σ₀ ∈ (0,1) is the initial value and the control parameter a ∈ (0, 0.5). 
<img width="2167" height="482" alt="d1" src="https://github.com/user-attachments/assets/79d0c1e0-4a20-4276-9c7e-259f177c2b3e" />

3. Encryption method : 
The schematic structure of encryption method is shown in Fig. 2.  
The input image 𝐼(𝑀1 × 𝑁1) is formed by combining 𝑘 gray-scale images of the same size where 
k is a perfect square. The cipher image in the encryption method is obtained after a scrambling 
operation and enciphering using XOR operation.

<img width="3000" height="2077" alt="d2" src="https://github.com/user-attachments/assets/658fd0a8-d1b0-4101-9203-03845d7e8133" />







Decrypting the Multiple grayscale image encryption using cross-coupled chaotic 
maps without using the keys: 
1. Scrambling : 
In order to get the scrambled image from the input image 𝐼, the following steps are performed:  
1. Using the initial parameters, the cross couple PWLCM is exe cuted for 𝑚𝑎𝑥 = 𝑀𝑎𝑥(𝑀1,𝑁1) 
iteration where 𝑀𝑎𝑥() selects the maximum between 𝑀1 or 𝑁1. The iteration generates two 
sequences:  
x𝑖 = 𝑥1,𝑥2,𝑥3,…,𝑥𝑚𝑎𝑥  
y𝑖 = 𝑦1,𝑦2,𝑦3,…,𝑦𝑚𝑎𝑥 
2. The sequence in 𝑥𝑖 and 𝑦𝑖 are sorted and their positions are used to generate the 
permutation table 𝑃𝑥 and 𝑃𝑦.  
3. Using 𝑃𝑥, the rows in the input image 𝐼 are scrambled.  
4. Using 𝑃𝑦, the columns in the output of Step[3] are scrambled, resulting in row-wise and 
column-wise scrambled image 𝐼𝑠𝑐𝑚. 
2. Enciphering : 
In order to get the cipher image from the scrambled image 𝐼𝑠𝑐𝑚, the following steps are 
performed:  
1. Chaotic sequence 𝑥1𝑖 and 𝑦1𝑖 are generated as:  
x1𝑖 = 𝑅𝑜𝑢𝑛𝑑(𝑥𝑖 ×106) mod 256  
y1𝑖 = 𝑅𝑜𝑢𝑛𝑑(𝑦𝑖 ×106) mod 256 where, 1 ≤ 𝑖 ≤ 𝑚𝑎𝑥  
2. Using 𝑥1𝑖, the first row of the scrambled image 𝐼𝑠𝑐𝑚 is XORed. This output is used to XOR the 
next row. Overall, the previous output is XORed with the next row till all rows in the scrambled 
image 𝐼𝑠𝑐𝑚 are exhausted.  
3. Using 𝑦1𝑖, the first column of the output from Step[2] is XORed. This output is used to XOR 
the next column. Overall, the previ ous output is XORed with the next column till all columns are 
exhausted. The resulting image is the cipher image in Patro’s et al. encryption scheme.




Algorithm : Row-wise Column-wise Unscrambling 
Input: Intermediate crypt-analysed image, image size m × n 
Output: Final unscrambled image 
1. ALL_col = {} 
2. THRESHOLD = 8(*An arbitrary small integer value can be taken, but ≠ 0*)  
3. INT_col = Intermediate crypt-analysed image 
4. Select random parent column from INT_col 
5. COL_set = INT_col - Parent_col 
6. For i = 1 to n-2: - Compute COL_diff[i] = pixel-wise difference - COUNT[i] = count where COL_diff[i] ≤ THRESHOLD - CHILD_col[i] = max(COUNT[i]) 
7. Update Parent_col and COL_set accordingly 
8. ALL_col = Append CHILD_col 
9. COL_descrambled_image = ImageAssemble(ALL_col) 
10. ALL_row = {} 
11. Select random parent row 
12. ROW_set = image - Parent_row 
13. For i = 1 to m-2: - Compute ROW_diff[i] - COUNT[i] = count where ROW_diff[i] ≤ THRESHOLD - CHILD_row[i] = max(COUNT[i]) 
14. Update Parent_row and ROW_set accordingly 
15. ALL_row = Append CHILD_row 
16. ROW_descrambled_image = ImageAssemble(ALL_row) 
17. Final unscrambled image obtained 
