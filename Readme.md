CrackQL
=======
CrackQL is a GraphQL password brute-force and fuzzing utility.

<h1 align="center">
	<img src="https://github.com/nicholasaleks/CrackQL/blob/master/static/CrackQL-Banner.png?raw=true" alt="CrackQL"/>
	<br>
</h1>

CrackQL is a versatile GraphQL penetration testing tool that exploits poor rate-limit and cost analysis controls to brute-force credentials and fuzz operations.
It works by automatically batching a GraphQL query or mutation operation which executes dynamic inputs from a supplied dictionary into a single request.
CrackQL evades traditional API rate and account take-over monitoring defenses since it uses query batching to stuff the entire set of credentials into a single HTTP request.


## Attack Use Cases

CrackQL can be used for a wide range of GraphQL attacks since it programmatically generate payloads based on a list of dynamic inputs, similar to [Burp Intruder](https://portswigger.net/burp/documentation/desktop/tools/intruder). However, unlike Intruder it does not send a request for each unique payload. Instead, CrackQL will optimize its unique payloads into a series of batch queries and mutations masked by different GraphQL aliases in order to evade rate-limit controls.

### Password Spraying Brute-forcing

CrackQL is perfect against GraphQL deployments that leverage in-band GraphQL authentication operations (such as the [GraphQL Authentication Module](https://www.graphql-modules.com/docs#authentication-module))

### Two-factor Authentication OTP Bypass

It is possible to use CrackQL to bypass two-factor authentication by sending all OTP (One Time Password) tokens

### User Account Enumeration

CrackQL can also be used for enumeration attacks to discover valid user ids, usernames and email addresses

### Field Stuffing Information Disclosure

If introspection is disabled, CrackQL could be used to stuff potential fields into query operations in order to leak information

### General Fuzzing


## Installation

### Requirements
- Python3
- Requests
- GraphQL

### Clone Repository
`git clone git@github.com:nicholasaleks/CrackQL.git`


### Get Dependencies
`pip install -r requirements.txt`

### Run CrackQL
`python3 CrackQL.py -h`

```
Usage: CrackQL.py -t http://example.com/graphql -q query.graphql -i users_passwords.csv -b 10 -a alias

Options:
  -h, --help            show this help message and exit
  -t URL, --target=URL  target url with a path to the GraphQL endpoint
  -b BATCH_SIZE, --batch-size=BATCH_SIZE
                        Number of batch operations per GraphQL request
  -o OUTPUT_JSON, --output-json=OUTPUT_JSON
                        Output results to a file (JSON)
  -i INPUTS_CSV, --input=INPUTS_CSV
                        Path to a csv list of arguments (i.e. usernames, emails, ids, passwords, otp_tokens, etc.)
  -v, --version         Print out the current version and exit.
```
