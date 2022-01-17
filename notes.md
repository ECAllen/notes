## About this dump file

A co-worker of mine used to keep all his notes in one large notepad file. He literally used Windows notepad. Then when he needed to check his notes, he would simply do keyword searches on the file. It went back years and proved to be a better reference than a fancy knowledge base. This file is a similar dump for myself. It includes everything I read, notes and cheatsheets. Organized with markdown but may move for emacs org mode format in the future. Creative commons license.  

## Ideas and Slogans

Simple tools for complex interactions

Tools over process

## vim

format a file
gg =G

indent
visual select
< or >

## Doom Emacs

### Projectile

M-x projectile-discover-in-directory

### Dired

create file spc-. then type filename

open neotree: SPC-o-p 

### Buffers and windows

buffers - hold data, usually file

## Golang

```shell: 

go get -u ./...

```


## Python

Get methods

dir(<object>)

Get help

help(<object>)

identity - location in memory of an object

id(<var>) - location in memory

type(<var>)

mutable - dict,list
immutable - strings tuples, integers *reassignment changes identity

Dunder methods - Double UNDERscore methods __add__ or magic methods

help(object.method)

coerce booleans
ex.
bool(0) -> False
bool(4) -> True


singleton - one copy, example None
ex.
```python:

a = None
b = None
id(a)
id(b)

```

will be the same value

PEP8 prefer 4 spaces to indent code

define a list
names = ['Evee','Harper','Lily','Linus']

A for loop ccan have a else clause. Code in the else clause will execute if the for loop did not hit a break statement.

```python:
    
positive = False
for num in items:
    if num < 0:
        break
    else:
        postive = True
               
```
               
set default method

```python: 

count = {}
for name in names:
    count.setdefault(name,0)
	count[name] += 1
	

def funcname(arg):
    body
			   
stride
every_other_name[0:4:2]

Files
fin = open('etc/passwd')
for line in fin:
     print line
	 
with open('/tmp/names.txt','w') as fout:
    fout.write('Evee\n')
	
Using file as seq
def add_numbers(filename):
    with open(filename) as fin:
	    return add_nums_to_seq(fin)

def add_nums_to_seq(seq):
    results = []
    for num, line in enumerate(seq):
    enumerate(seq):
    results.append('{0}-{1}'.format(num,line))
    return results
               
```
               
Object - grouping together state and methods

Class - define objects 

class Animal
               
generator example

```python: 

xs = (x for x in range(4))
xs.__next__()

```

### Introspection

objects store their type in their __class__ attr

type()

issubclass()

isinstance()

dir()

hasattr(<object>, 'attr')

getattr(<object>, 'attr') or <object>.'attr' example a.denonminator

prefer EAFP easier to as for forgiveness

globals() - introspect the global namespace

globals()[foo] = 'bar' <-- globals dict IS the global namespace

locals() - introspect the local namespace

f-strings - PEP 498, ex. f"{name}"

inspect module :wqa



### Django

- start a project

django-admin startproject myproject

- run project

python manage.py runserver

- create a app

python manage.py startapp <app>

- show migrations

python manage.py showmigrations

- run all pending migrations

python manage.py migrate

- create migrations based on models

python manage.py makemigrations

- see a specific migration

python manage.py sqlmigrate <migration>

- misc

python manage.py createsuperuser


#### Meta





#### Files

settings.py - INSTALLED_APPS[] list of apps

urls.py - routing


## Terraform

### Blocks

block template:

```json
block_type label_one label_two {
    key = value
    embedded_block {
        key = value
    }
}
```


### object types:

- string
- number
- bool
- list
- map

### Keyword references

var.somevariable

local.someobject.somevar

module.someobject.somevar

### Provisioners

last resort prefer puppet,chef, ansible

local - executes on local server

remote - executes on remote server

can happen at creation or destruction

example file provisioner with heredoc syntax:

```json
provisioner "file" {
  content = <<EOF
access_key = 
secret_key = 
EOF
  destination = "/home/aws-user/.s3cfg"
}
```

### Resources

example random int

```json
resource "random_integer" "rand"{
    min = 10000
    max = 99999
}
```

### Functions

merge() - takes two maps and merges them.

 
### CLI

terraform init

terraform plan

terraform apply

### variables

precedence: env, file, command line


# Books

## Optionality 

Optionality = the right but not the obligation to take action.

Generating better options is more important thaant beinbg a perffect decision-maker.

We should think of tradeoffs as the enemy: then are massinvely time-cincuming;, and they make ud unhappy... we want to /make asa fee as we can get away with.

So the question if not what to cut. Our starting point is thta everything gets cut, and has to earn its way back into ciniseradriotn,


## Writing an Interpreter in Go by Thorsten Ball

parser - takes text and builds data structure that represents the input 

statements vs. expressions - expressions produce values and statements dont. 

lexer - reduces to tokens

ast - abstract syntax tree

## ECDSA

https://www.instructables.com/Understanding-how-ECDSA-protects-your-data/

Allows verification of authenticity without compromising security. It is impossible to forge a signature. It does no encrypt the data but ensures it is not tampered with.

Algo (high level)
    
    choose random point on curve, point of origin
    
    generate a random number, private keys
    
    apply equation to private key and point of origin, public key
   
Sign the file
    
    equation(use the private key, with a hash of the file), signature

    signature is divided into R and S
    
Verification

    equation(S, public key) == R
    

ECDSA uses SHA1 hashes
    

## Mastering Bitcoin

transaction input and output - there will be a difference between them which is the miner fee

transactions form a chain 

users keys can unlock previous output in the chain proving ownership

change address - address of new and old user

UTXO - unspent transactions database

### Constructing a transaction

## (Ethereum Book)[https://github.com/ethereumbook/ethereumbook]

## Fallback functions

It is called when a non-existent function is called on the contract.

It is required to be marked external.

It has no name.

It has no arguments

It can not return any thing.

It can be defined one per contract.

If not marked payable, it will throw exception if contract receives plain ether without data.

Solidity fallback function:

It has no name, no arguments, no return values. It external and payable. Defined once. Called when non-existent function called. 

### EOA vs. Contract Accounts

Externally owned accounts are those that have a private key; having the private key means control over access to funds or contracts. 

A contract account has smart contract code, which a simple EOA can’t have. Furthermore, a contract account does not have a private key. Instead, it is owned (and controlled) by the logic of its smart contract code: the software program recorded on the Ethereum blockchain at the contract account’s creation and executed by the EVM.

account addresses are derived directly from private keys: a private key uniquely determines a single Ethereum address, also known as an account.

### Cryptography

There is no encryption as part of the Ethereum protocol—all messages that are sent as part of the operation of the Ethereum network can (necessarily) be read by everyone. As such, private keys are only used to create digital signatures for transaction authentication.

Starting with a private key in the form of a randomly generated number k, we multiply it by a predetermined point on the curve called the generator point G to produce another point somewhere else on the curve, which is the corresponding public key K:
K = k * G 

the generator point is always the same for all Ethereum users

Ethereum only uses uncompressed public keys; therefore the only prefix that is relevant is (hex) 04.

The test most commonly used for a hash function is the empty input. If you run the hash function with an empty string as input you should see the following results:

Keccak256("") =
  c5d2460186f7233c927e7db2dcc703c0e500b653ca82273b7bfad8045d85a470

SHA3("") =
  a7ffc6f8bf1ed76651c14756a061d662f580ff4de43b49fa82d80a4b80f8434a

Ethereum uses Keccak-256, even though it is often called SHA-3 in the code.

Ethereum addresses are unique identifiers that are derived from public keys or contracts using the Keccak-256 one-way hash function.


We use Keccak-256 to calculate the hash of this public key:

Keccak256(K) = 2a5bc342ed616b5ba5732269001d3f1ef827552ae1114027bd3ecf1f086ba0f9

Then we keep only the last 20 bytes (least significant bytes), which is our Ethereum address:

001d3f1ef827552ae1114027bd3ecf1f086ba0f9


### Wallet


### Transactions

A transaction is a serialized binary message that contains the following data:

Nonce

    A sequence number, issued by the originating EOA, used to prevent message replay

Gas price

    The amount of ether (in wei) that the originator is willing to pay for each unit of gas

Gas limit

    The maximum amount of gas the originator is willing to buy for this transaction

Recipient

    The destination Ethereum address

Value

    The amount of ether (in wei) to send to the destination

Data

    The variable-length binary data payload

v,r,s

    The three components of an ECDSA digital signature of the originating EOA

### Smart Contracts and Solidity

Computer programs

    Smart contracts are simply computer programs. The word “contract” has no legal meaning in this context.

Immutable

    Once deployed, the code of a smart contract cannot change. Unlike with traditional software, the only way to modify a smart contract is to deploy a new instance.

Deterministic

    The outcome of the execution of a smart contract is the same for everyone who runs it, given the context of the transaction that initiated its execution and the state of the Ethereum blockchain at the moment of execution.

EVM context

    Smart contracts operate with a very limited execution context. They can access their own state, the context of the transaction that called them, and some information about the most recent blocks.

Decentralized world computer

    The EVM runs as a local instance on every Ethereum node, but because all instances of the EVM operate on the same initial state and produce the same final state, the system as a whole operates as a single "world compute
    

#### Lifecycle

0x0    special contract creation address

contracts only run if they are called by a transaction

contracts are atomic 

To delete a contract, you execute an EVM opcode called SELFDESTRUCT. That operation costs “negative gas,” a gas refund, thereby incentivizing the release of network client resources from the deletion of stored state. 

#### Solidity 

function syntax:

function FunctionName([parameters]) {public|private|internal|external}
[pure|view|payable] [modifiers] [returns (return types)]


#### Gas

estimating gas cost:

var contract = web3.eth.contract(abi).at(address);
var gasEstimate = contract.myAweSomeMethod.estimateGas(arg1, arg2,
    {from: account});
    

To obtain the gas price from the network you can use:

var gasPrice = web3.eth.getGasPrice();

And from there you can estimate the gas cost:

var gasCostInEther = web3.utils.fromWei((gasEstimate * gasPrice), 'ether');

### Security 

#### Re-entrency

This type of attack can occur when a contract sends ether to an unknown address. An attacker can carefully construct a contract at an external address that contains malicious code in the fallback function. 

##### prevention

The first is to (whenever possible) use the built-in transfer function when sending ether to external contracts.

The second technique is to ensure that all logic that changes state variables happens before ether is sent out of the contract (or any external call).

A third technique is to introduce a mutex.

#### over flow under flow

##### prevention

The current conventional technique to guard against under/overflow vulnerabilities is to use or build mathematical libraries that replace the standard math operators addition, subtraction, and multiplication (division is excluded as it does not cause over/underflows and the EVM reverts on division by 0).

### Tokens

#### Interface

ERC20 

The ERC20 Interface in Solidity:

```solidity

contract ERC20 {
   function totalSupply() constant returns (uint theTotalSupply);
   function balanceOf(address _owner) constant returns (uint balance);
   function transfer(address _to, uint _value) returns (bool success);
   function transferFrom(address _from, address _to, uint _value) returns
      (bool success);
   function approve(address _spender, uint _value) returns (bool success);
   function allowance(address _owner, address _spender) constant returns
      (uint remaining);
   event Transfer(address indexed _from, address indexed _to, uint _value);
   event Approval(address indexed _owner, address indexed _spender, uint _value);
}

```

data structures

mapping(address => uint256) balances;

mapping (address => mapping (address => uint256)) public allowed;

#### Workflows

1) transfer - wallet to wallet direct transfer of tokens, uses the 'transfer' function

2) approve and transfer - two transaction


## Buildspace Solana project

program: 

    a) piece of code that lives on the blockchain

    b) programs are stateless
    
    c) programs interact with accounts for data
    
accounts

    a) stores data
    
    b) users can have 1,000s of accounts 
    
Configuring Solana

    Install rust
    https://doc.rust-lang.org/book/ch01-01-installation.html
    
    Install Solana: https://docs.solana.com/cli/install-solana-cli-tools#use-solanas-install-tool
    
    set Solana network to localhost

    ```bash
solana config set --url localhost 
    ```
   
   
   start a local Solana node

   ```bash
solana-test-validator 
   ```
   
   Install mocha, anchor, npm anchor, npm solana/web3.js
   
  ```bash

npm install -g mocha

cargo install --git https://github.com/project-serum/anchor anchor-cli --locked
  
npm install @project-serum/anchor @solana/web3.js
  
  ``` 
    
    
   Create a project
   
   ```bash

anchor init myproject --javascript 

```
   
   Generate local Solana wallet
   
   ```bash

solana-keygen new

```
   
   Get public key for local wallet
   
   ```bash

solana address

    ```

    airdrop sol 
    
    ```bash

solana airdrop 5 93SAmhpBneKq6UybsFbn5gf9kzAcooCz732bGaGiBehg  --url https://api.devnet.solana.com

```

# React

https://scrimba.com/learn/learnreact


global var ReactDOM

```javascript

ReactDOM.render(<h1>Hello</h1>, document.getElementById("root"))

```

## Components

Pascal case component, not camel case

Wrap it in angle brackets in ReactDOM.render()

Components can have parent child relationship

```javascript

function Navbar() {
    return (
       <div></div> 
    )
}

function MainContent() {
    return (
        <div></div>
    )
}

ReactDOM.render(
    <div>
        <Navbar />
        <MainContent />
    </div>,
    document.getElementById("root")
)



```



## JSX

Like html with some differences.

    html => JSX 

    class => className
    
    
## organization

create a react project

```javascript

npx create-react-app hello

```

Use import and export from ES6

## Props

Use mustache syntax


```javascript

import React from "react"
import ReactDOM from "react-dom"

function App() {
    const userName = "me"
    
    return (
        <h1>Hello {userName} !</h1>
    )
}

ReactDOM.render(<App />, document.getElementById("root"))

```

```javascript

// Somewhat bogus example

export default function Contact(props) {
    return (
        <div className="contact-card">
            <img src={props.image}/>
            <h3>{props.name}</h3>
            <div className="info-group">
                <p>{props.phone}</p>
            </div>
            <div className="info-group">
                <img src="./images/mail-icon.png" />
                <p>{props.email}</p>
            </div>
        </div>
    )
}

function App() {
    return (
        <div className="contacts">
            <Contact 
                image="./images/mr-whiskerson.png" 
                name="Mr. Whiskerson"
                phone="(212) 555-1234"
                email="mr.whiskaz@catnap.meow"
            />
            <Contact 
                img="./images/fluffykins.png"
                name="Fluffykins"
                phone="(212) 555-2345"
                email="fluff@me.com"
            />
        </div>
    )
}

```

## Props and arrays

```javascript

// contrived example from scrimba

jokesData = [
    {
        setup: "I got my daughter a fridge for her birthday.",
        punchline: "I can't wait to see her face light up when she opens it."
    },
    {
        setup: "How did the hacker escape the police?",
        punchline: "He just ransomware!"
    }
]

export default function Joke(props) {
    return (
        <div>
            {props.setup && <h3>Setup: {props.setup}</h3>}
            <p>Punchline: {props.punchline}</p>
            <hr />
        </div>
    )
}

export default function App() {
    const jokeElements = jokesData.map(joke => {
        return <Joke setup={joke.setup} punchline={joke.punchline} />
    })
    return (
        <div>
            {jokeElements}
        </div>
    )
}

```


## Events

Do not use the "()" for function call in the JSX

```javascript

import React from "react"

export default function App() {
    function handleClick() {
        console.log("I was clicked!")
    }
    
    function handleOnMouseOver() {
        console.log("MouseOver")
    }
    
    return (
        <div className="container">
            <img 
                src="https://picsum.photos/640/360" 
                onMouseOver={handleOnMouseOver} 
            />
            <button onClick={handleClick}>Click me</button>
        </div>
    )
}


```

## State 

React.useState()

```javascript

const [someval,setterFunc] = React.useState(someInitVal)

```


## useEffects

used for side effects ie API calls


# react-three-fiber


https://github.com/pmndrs/react-three-fiber

https://threejs.org/docs/index.html#manual/en/introduction/Creating-a-scene

## Basics

scene -> camera -> renderer -> attach to canvas

geometry -> mesh -> scene.add()

frustum - A frustum is the name of a 3d shape that is like a pyramid with the tip sliced off. In other words think of the word "frustum" as another 3D shape like sphere, cube, prism, frustum.

mesh = geometry + material + orientation


Example set camera width to canvas 

```javascript

    function render(time) {
      time *= 0.001;
     
      const canvas = renderer.domElement;
      camera.aspect = canvas.clientWidth / canvas.clientHeight;
      camera.updateProjectionMatrix();
     
      ...

```


### Create app
```bash
npx create-react-app my-app
cd my-app
```

### Install dependencies
```bash
npm install three @react-three/fiber

npm install --save husky lint-staged prettier
```

### Start
```bash
npm run start
```


# Node.js

## cheatsheet

```bash

# initialize minimum node project with a minimal package.json
npm init -y 

# install a package 
npm i <some package> 
npm i express 

```

