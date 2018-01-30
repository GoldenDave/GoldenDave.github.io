GOLDX Balance Checker
======================

Written with a zero knowledge of Web3.js and one week's experience of Bootstrap....

`start()`

```
if (typeof web3 !== 'undefined')
```
`web3` is set by Metamask - use that if it is available

otherwise

```
        web3 = new Web3();
        web3.setProvider(new web3.providers.HttpProvider('https://api.myetherapi.com/eth'));
```

create a new web3 object and link it up to MyEtherWallet'
s API.

(if you are going to make a lot of calls please use infura instead)


`getBalance()`

Loads of ways we could do this but since I am a low level hacker, I found somebody's notes on how to do this from a low level call.

`balanceOf(address)` gets converted to the following data

keccak-256('balanceof(address)') => `0x70a08231`

The address is encoded in 256 bits which means it needs to be padded with 24 zeros - 
`000000000000000000000000` followed by the address (with the `0x` stripped off)

This gets sent in the `data` field to the GOLDX token contract at `0xeAb43193CF0623073Ca89DB9B712796356FA7414` with a value of zero via a call (not transaction) function.

convert the answer from Wei to Ether (i.e. to 18 decimal places) and we are done!