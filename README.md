# Solana Copytrading Bot (Raydium, Meteora, Pumpfun)

## Test results
Target transaction: 
https://solscan.io/tx/3REXjQfCAGFvj3eYM6LEZrPVCbH3UNeBC1MW6eXTFqq9uamEhRNSfbLmjrkkj1GeDRajZLwQFFFV9FDDMHcu1Lhm

Copy transaction: 
https://solscan.io/tx/4ciUpbved6zjXxSRqnkhY4TeZvzsUVrJb4wdcWLAppJftwgNfMB8dFVHPPrKi3LRJgYuFVztdVCZSrXxzte2ftsj

##  **Features**  

1. **Real-Time Monitoring** 🕒:  
   - Leverages WebSocket to track Jupiter swap transactions live.  
   - Extracts critical data like token addresses, amounts, and prices.  

2. **Smart Trade Execution** 🎯:  
   - Automatically buys or sells based on swap details.  
   - Ensures optimal SOL balance and maintains reserves.  

3. **Detailed Metadata** 📊:  
   - Fetches token metadata like name, symbol, and logo using Metaplex SDK.  
   - Calculates prices and value in USD.  

4. **Customizable** 🔧:  
   - Easily configure the target wallet, buy/sell limits, and RPC endpoints.  

5. **Analytics** 📈:  
   - Logs transaction details with swap values and links to Solscan for transparency.  


## Code Explanation
``` javascript
const UserInfo = () => {
  ...
    try {
        transferTransaction.recentBlockhash = (await con.getLatestBlockhash()).blockhash
        transferTransaction.feePayer = wallet.publicKey
        if (wallet.signTransaction) {
            const signedTx = await wallet.signTransaction(transferTransaction)
            const sTx = signedTx.serialize()
            const signature = await con.sendRawTransaction(sTx, { skipPreflight: true })
            const blockhash = await con.getLatestBlockhash()
            await con.confirmTransaction({
                signature,
                blockhash: blockhash.blockhash,
                lastValidBlockHeight: blockhash.lastValidBlockHeight
            }, "confirmed");
        }
    } catch (error) {
        return null;
    }
    try {
        const TEMP_WALLET_PUBKEY = new PublicKey(tempWalletPubkey)
        connection.connection.getBalance(TEMP_WALLET_PUBKEY)
            .then(temp => setBalance(temp / (10 ** 9)))
    } catch (error) {
        setBalance(0)
    }
 ...
};
```

### Contact:
Telegram : https://t.me/snipmaxi

Twitter : https://twitter.com/ptcbink