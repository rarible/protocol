// Imports
import Web3 from "web3"
import { createRaribleSdk } from "@rarible/sdk"
import { EthereumWallet } from "@rarible/sdk-wallet"
import { Blockchain } from "@rarible/api-client"
import { Web3Ethereum } from "@rarible/web3-ethereum"

// Code
const { ethereum } = window as any
const web3 = new Web3(provider)
const web3Ethereum = new Web3Ethereum({ web3 })
const ethWallet = new EthereumWallet(web3Ethereum)
const raribleSdk = createRaribleSdk(ethWallet, "staging")