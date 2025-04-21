// Decentralized E-commerce Platform
// Technologies: React.js, TailwindCSS, Web3.js, IPFS, Solidity (Smart Contracts)

import React, { useState, useEffect } from 'react';
import Web3 from 'web3';
import { ethers } from 'ethers';
import { Card, CardContent } from '@/components/ui/card';
import { Button } from '@/components/ui/button';

const Product = ({ product, buyProduct }) => (
  <Card className="m-4 p-4">
    <CardContent>
      <h2 className="text-xl font-bold">{product.name}</h2>
      <p>{product.description}</p>
      <p className="text-green-600">Price: {product.price} ETH</p>
      <Button onClick={() => buyProduct(product.id)}>Buy</Button>
    </CardContent>
  </Card>
);

const App = () => {
  const [account, setAccount] = useState('');
  const [products, setProducts] = useState([]);

  useEffect(() => {
    loadBlockchainData();
  }, []);

  const loadBlockchainData = async () => {
    const web3 = new Web3(Web3.givenProvider);
    const accounts = await web3.eth.requestAccounts();
    setAccount(accounts[0]);
    // Fetch products from IPFS / smart contract (mocked here)
    setProducts([
      { id: 1, name: 'T-Shirt', description: 'Cotton T-shirt', price: 0.05 },
      { id: 2, name: 'Cap', description: 'Cool cap', price: 0.02 },
    ]);
  };

  const buyProduct = async (productId) => {
    console.log(`Buying product with ID: ${productId}`);
    // Interact with smart contract to initiate escrow payment
  };

  return (
    <div className="p-8">
      <h1 className="text-3xl font-bold mb-4">Decentralized E-commerce</h1>
      <p className="mb-6">Connected Wallet: {account}</p>
      <div className="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-3 gap-4">
        {products.map((product) => (
          <Product key={product.id} product={product} buyProduct={buyProduct} />
        ))}
      </div>
    </div>
  );
};

export default App;
