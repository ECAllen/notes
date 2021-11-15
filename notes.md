# Notes

## Ideas and Slogans

Simple tools for complex interactions

```shell: 

go get -u ./...

```


## Doom Emacs

### Dired

create file spc-. then type filename

## Pandoc

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


## Mastering Bitcoin

transaction input and output - there will be a difference between them which is the miner fee

transactions form a chain 

users keys can unlock previous output in the chain proving ownership

change address - address of new and old user

UTXO - unspent transactions database

### Constructing a transaction

## (Ethereum Book)[https://github.com/ethereumbook/ethereumbook]

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
