---
layout: post
title: "Notes on Even-Mansour Scheme"
---
[PDF version](.) to be written.
## Even Mansour Scheme 

**F**: randomly selected keyless permutation

> only way to access F is through a black box

![basic EM scheme image](.)

**Security Goal**: 
 - **D**: Data (X,W) pairs (plain/ciphertext pairs)
 - **T**: Time (Y,Z) pairs (computation)
 - **D x T > 2^n** for any attack
 
## Daemen Attack (Chosen Ciphertext)
[link to paper](.)
**Differential Crpytanalysis** Since **F** is random, 1 plain/ciphertext pair with dY->dZ expected on average.
(Y1,Z1), (Y2,Z2), Y2 = Y1 + dY, Z2 = Z1 + dZ

Attack Steps:
1. Choose *t* different input pairs with input difference dY. (Yi,Yi+dY)
2. Compute (Zi,Zi+dZi) for each input pair.
3. Make a list of (dZi, Yi) pairs. (sort the list)
4.1. Pick random input X1. X2 = X1 + dY.
4.2. Compute W1,W2 corresponding to X1,X2. dW = W1+W2.
4.3. Search the list for a match between dW and dZi.
4.3.1. When a match is found at index i, either
       X1+K1 = Yi
	   F(Yi)+K2 = W1
	   or
	   X1+K1 = Yi+dY
	   F(Yi)+K2 = W1+dZi
	   
Repeating step 4 2^n/t times reveals th correct key.
Data Complexity: 2^n/t
Time Complexity: t
D+T : 2^n/t + t   ( for t~2^(n/2) D+T ~ 2x2^(n/2))

## Biryukov-Wagner Attack (Known Plaintext)
[link to paper](.)
**Slide with a Twist** Attack uses pairs with X1 = Y2 (i.e. Y1 = X2)
![slide attack image](.)

X1 = Y2 --> W2 = Z2 + K2
            W2 = F(Y2) + K2
			W2 = F(X1) + K2
	
Y1 = X2 --> W1 = Z1 + K2
            W1 = F(Y1) + K2
			W1 = F(X2) + K2
			
K2       = W2 + F(X1) = W1 + F(X2)
W1+W2+K2 = W1 + F(X1) = W2 + F(X2)

Attack Steps:
1. Collect *t* encryptions (Xi,Wi) (p/c pairs)
2. Make a list of (F(Xi) + Wi, Xi) pairs.
3. Sort the list. (complexity tlog(t))
4. Locate pairs satisfying F(Xi) + Wi = F(Xj) + Wj.
4.1. Keys are K2 = F(Xi) + Wj
              K1 = Xi + Xj
			  
Birthday Paradox says t ~ 2^(n/2) is enough to produce matching (i,j)

Data complexity: t ~ 2^(n/2)
Time complexity: t ~ 2^(n/2)

## Dunkelman-Keller-Shamir Attack (Known Plaintext)
[link to paper](.)
**Slidex??** 
Assume we have X1 = Y2 + c , X2 = Y1 + c for some c
               
X1 = Y2 + c --> W2 = Z2 + K2
                W2 = F(Y2) + K2 
				W2 = F(X1+c) + K2
X2 = Y1 + c --> W1 = Z1 + K1
                W1 = F(Y1) + K2 
				W1 = F(X2+c) + K2
K2           = W1 + F(X2+c) = W2 + F(X1+c)
K2 + W1 + W2 = W2 + F(X2+c) = W1 + F(X1+c)

Attack Steps:
1. Collect *t* encryptions (Xi,Wi) (p/c pairs)
2. Choose *m* different c values.
3. For each c value make a list (L_c) of pairs (Wi + F(Xi+c), Xi)
3.1. Sort the list. (complexity tlog(t))
3.2. Locate pairs satisfying Wi + F(Xi + c) = Wj + F(Xj + c).
3.3. Keys are K2 = Wi + F(Xj + c)
              K1 = Xi + Xj + c
			  
How many c do we need? (m=?)
 - For each c we check t^2 i,j pairs: sorting the list reduces actual work done, but in theory we considered t^2 i,j pairs.
 - Each check has a probability of 2^(-n) of satisfying step 3.2.
 - To get 1 pair that satisfies 3.2 we need to do 2^n checks (on average).
 - Total number of checks: mt^2. mt^2 = 2^n --> m = 2^n / (t^2)

Data complexity: m ~ 2^n/(t^2)
Time complexity: mt ~ 2^(n)/t
 
