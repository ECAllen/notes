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
