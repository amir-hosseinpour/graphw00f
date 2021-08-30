<h1 align="center">
 <img src="https://github.com/dolevf/graphw00f/blob/main/static/graphw00f.png?raw=true" width="alt="graphw00f"/>
 <br>
 graphw00f - GraphQL Fingerprinting
</h1>

graphw00f (inspired by [wafw00f](https://github.com/EnableSecurity/wafw00f)) is the GraphQL fingerprinting tool for GQL endpoints.

# Table of Contents
* [How does it work?](#how-does-it-work)
* [Detections](#detections)
* [GraphQL Technologies Defence Matrices](#graphql-technologies-defence-matrices)
* [Prerequisites](#prerequisites)
* [Installation](#installation)
* [Support & Issues](#support-and-issues)
* [Resources](#resources)


# How does it work?
graphw00f is a Python utility which sends a mix of benign and malformed queries to determine the GraphQL engine running behind the scenes.

Specially crafted queries cause different GraphQL server implementations to respond uniquely to queries, mutations and subscriptions, this makes it trivial to fingerprint the backend engine and distinguish between the various GraphQL implementations. (CWE: [CWE-200](#CWE-Reference))

# Detections
graphw00f currently attempts to discover the following GraphQL engines:
* Graphene - Python
* Ariadne - Python
* Apollo - TypeScript
* graphql-go - Go
* gqlgen - Go
* WPGraphQL - PHP
* GraphQL API for Wordpress - PHP
* Ruby - GraphQL
* graphql-php - PHP
* Hasura - Haskell
* HyperGraphQL - Java
* graphql-java - Java
* Juniper - Rust
* Sangria - Scala
* Flutter - Dart
* Diana.jl - Julia
* Strawberry - Python
* Tartiflette - Python
                                                                                           
# GraphQL Technologies Defence Matrices
Each fingerprinted technology (e.g. Graphene, Ariadne, ...) has an associated document ([example for graphene](https://github.com/dolevf/graphw00f/blob/main/docs/graphene.md)) which covers the security defence mechanisms the specific technology supports to give a better idea how the implementation may be attacked.
                                                                                                              
```
| Field Suggestions | Query Depth Limit | Query Cost Analysis | Automatic Persisted Queries | Introspection      | Debug Mode | Batch Requests  |
|-------------------|-------------------|---------------------|-----------------------------|--------------------|------------|-----------------|
| On by Default     | No Support        | No Support          | No Support                  | Enabled by Default | N/A        | Off by Default  |
```

# Prerequisites
* python3
* requests                   
                                                                                                              
# Installation
## Clone Repository
`git clone git@github.com:dolevf/graphw00f.git`

## Run graphw00f
`python3 main.py -h`

```
Usage: main.py -h

Options:
  -h, --help            show this help message and exit
  -r, --noredirect      Do not follow redirections given by 3xx responses
  -t URL, --target=URL  target url with the path
  -o OUTPUT_FILE, --output-file=OUTPUT_FILE
                        Output results to a file (CSV)
  -l, --list            List all GraphQL technologies graphw00f is able to
                        detect
  -v, --version         Print out the current version and exit.
```

# Example
```
python3 main.py -t http://127.0.0.1:5000/graphql

+-------------------+           +--------------------+
|      GRAPHQL      |           |     FINGERPRINT    |
+-------------------+           +--------------------+
                  **              **                  
                    ***        ***                    
                       **    **                       
                +-------------------+                 
                |     graphw00f     |                 
                +-------------------+                 
                  ***            ***                  
                **                  ***               
              **                       **             
    +--------------+              +--------------+       
    |    Node X    |              |    Node Y    |       
    +--------------+              +--------------+     
                  ***            ***                  
                     **        **                     
                       **    **                       
                    +------------+                      
                    |   Node Z   |                      
                    +------------+    

                graphw00f - v1.0.0
          The fingerprinting tool for GraphQL
  
[*] Checking if GraphQL is available at https://demo.hypergraphql.org:8484/graphql...
[*] Found GraphQL...
[*] Attempting to fingerprint...
[*] Discovered GraphQL Engine: (HyperGraphQL)
[!] Attack Surface Matrix: https://github.com/dolevf/graphw00f/blob/main/docs/hypergraphql.md
[!] Technologies: Java
[!] Homepage: https://www.hypergraphql.org
[*] Completed.
```
                                                                                                              
# Support and Issues
Any issues with graphw00f such as false/true positives, inaccurate detections, etc. please create a GitHub issue with environment details.

# Resources
Want to learn more about GraphQL? head over to my other project and hack GraphQL away: [Damn Vulnerable GraphQL Application](https://github.com/dolevf/Damn-Vulnerable-GraphQL-Application/)
