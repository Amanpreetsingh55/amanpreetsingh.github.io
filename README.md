import React, { useState, useEffect } from 'react'; import Web3 from 'web3'; import { Button } from "@/components/ui/button";

export default function HomePage() { const [account, setAccount] = useState(null);

useEffect(() => { loadWeb3(); }, []);

const loadWeb3 = async () => { if (window.ethereum) { const web3 = new Web3(window.ethereum); await window.ethereum.request({ method: 'eth_requestAccounts' }); const accounts = await web3.eth.getAccounts(); setAccount(accounts[0]); } else { alert("Please install MetaMask"); } };

return ( <div className="p-6 max-w-4xl mx-auto"> <h1 className="text-3xl font-bold mb-4">Decentralized E-commerce Platform</h1> <p className="mb-4">Welcome, {account ? account : "Please connect your wallet."}</p> <Button onClick={loadWeb3} className="mb-4">Connect Wallet</Button>

{/* Components to be added here */}
  {/* - Product Listing */}
  {/* - Escrow Payment System */}
  {/* - Decentralized Reviews */}
  {/* - Token-Based Payments */}
  {/* - Loyalty Program */}
</div>

); }

