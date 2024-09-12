# Setting Up Solana Wallet Adapter in Next.js Projects Using `solana-wallet-setup` CLI Tool

## Introduction

Adding a Solana wallet adapter to your Next.js project is now as simple as running **one command**! This step-by-step guide will walk you through how to use the `solana-wallet-setup` CLI tool, which automates the entire process, including configuring components, installing dependencies, and adding wallet functionalities.

With this tool, you can set up the wallet adapter in minutes, whether you're using a standard `app` directory or a `src` directory structure.

### Prerequisites

1. A Next.js project should already be set up on your machine.
    
2. shadcn should be configured. It's necessary as `Connect Wallet` is the custom component.
    

---

## Step-by-Step Guide to Using `solana-wallet-setup`

### 1\. Install `solana-wallet-setup`

The first step is to globally install the `solana-wallet-setup` CLI tool on your machine.

Run the following command: (with your preferred package manager)

```bash
npm install -g solana-wallet-setup@latest
```

This will install the CLI tool globally so that you can use the `solana-wallet-setup` command in any Next.js project.

---

### 2\. Run the Setup Command

Navigate to the root of your Next.js project where the `package.json` file exists. Then run the following command to set up the Solana wallet adapter:

```bash
solana-wallet-setup --setup-wallet
```

The tool will perform several tasks automatically:

* Detect your package manager (e.g., npm, yarn, or pnpm).
    
* Install the required Solana wallet adapter packages.
    
* Install `shadcn/ui` components like dropdown menus and buttons.
    
* Create the necessary wallet context and wallet connect components.
    
* Update your `layout.tsx` file to wrap your app with the `WalletContext`.
    

---

### 3\. Confirm Setup in the CLI

Once you run the command, the tool will guide you through a series of simple questions in the terminal:

* **Which package manager are you using?**  
    If your project has no lock file, the tool will ask which package manager you prefer (npm, yarn, or pnpm).
    
* **What is your project structure?**  
    You’ll be prompted to choose whether your project uses a standard `app` directory or a `src` directory.
    
* **Proceed with Solana Wallet setup?**  
    Before starting the setup, the tool will ask you to confirm if you'd like to proceed.
    

The tool will then verify whether the project is indeed a Next.js project by checking the `package.json` file and looking for Next.js dependencies.

---

### 4\. Automatic Installation

After confirming your selections, the `solana-wallet-setup` CLI tool will automatically install the required dependencies for the Solana wallet adapter:

* `@solana/wallet-adapter-wallets`
    
* `@solana/wallet-adapter-react-ui`
    
* `@solana/wallet-adapter-react`
    
* `@solana/wallet-adapter-phantom`
    
* `@solana/wallet-adapter-base`
    
* `@solana/web3.js`
    
* `@radix-ui/react-slot`
    
* `@radix-ui/react-dropdown-menu`
    

Additionally, the tool will install the required components from `shadcn/ui`:

* `dropdown-menu`
    
* `button`
    

---

### 5\. File and Code Setup

#### 5.1 Creating Wallet Components

The tool will automatically create a `wallets/` folder inside your `components` directory and add two files:

1. **WalletContextProvider.tsx**  
    This file sets up the wallet context and connects it to the Solana network. you can change network from here.
    
2. **CustomWalletConnect.tsx**  
    This file provides a custom wallet connect button that you can use in your app to connect and disconnect from the Solana wallet.
    

#### 5.2 Modifying `layout.tsx`

The CLI tool will modify your existing `layout.tsx` file to include the wallet context. It will wrap your app’s `children` inside the wallet provider, so the wallet functionalities are available globally across the app.

---

### 6\. Using the Wallet in Your App

After the setup is complete, you can now start using the wallet in your components.

#### 6.1 How to Use Wallet Connect in Your Components

To use the wallet connect functionality in any of your components, you need to import the `CustomWalletConnect` component that the CLI tool added for you.

Here’s how to do it:

```jsx
import dynamic from 'next/dynamic';

const WalletsProvider = dynamic(
  () => import('../components/wallets/CustomWalletConnect'),
  { ssr: false }
);

const YourComponent = () => {
  return (
    <div>
      <WalletsProvider />
      {/* Rest of your component */}
    </div>
  );
};

export default YourComponent;
```

---

### 7\. Using Solana Wallet Hooks

You can now use Solana wallet hooks in any of your components. Here are the most commonly used hooks:

* **useWallet**: This hook lets you connect, disconnect, and retrieve wallet states.
    
* **useConnection**: This hook provides the connection to the Solana blockchain.
    

Here’s an example of how to use these hooks:

```jsx
import { useWallet, useConnection } from '@solana/wallet-adapter-react';

const MyComponent = () => {
  const { connected, connect, disconnect } = useWallet();
  const { connection } = useConnection();

  return (
    <div>
      {connected ? (
        <button onClick={disconnect}>Disconnect Wallet</button>
      ) : (
        <button onClick={connect}>Connect Wallet</button>
      )}
    </div>
  );
};
```

---

### 8\. Check WALLET\_[USAGE.md](http://USAGE.md)

Once the setup is complete, a `WALLET_USAGE.md` file will be created in your project directory. This file contains detailed instructions on how to use the wallet in your app, along with additional information about customizing and managing wallet components.

---

## Conclusion

You’ve now set up a fully functional Solana wallet adapter in your Next.js project using the `solana-wallet-setup` CLI tool. This tool streamlines the entire process, making it easy to integrate Solana wallet functionalities into your app with minimal effort.

For advanced usage, refer to the official [Solana Wallet Adapter Documentation](https://github.com/anza-xyz/wallet-adapter) for more details.

Happy coding! 🚀

---

