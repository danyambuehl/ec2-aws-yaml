Titel
====

# Ziel

Beschreibung des Ziel

# Voraussetzung

Identity and Access Management (IAM) ein User mit Admin rechten erstellen
 
 Go To the User und unter "Security Credentionals" clicke auf den Button "Create access key"

 Wähle CLI aus und erstelle einen neuen Access Key. 

 Speichere den Access Key und den Secret Access Key ab.

# AWS Command Line Interface

  
  **AWS Command Line Interface download and install **
  
  **CMD Öffnen und Version überprüfen**
  
  > `$ aws --version`

![CLI Version](images/aws_cli.png)

  **AWS Command Line Interface Konfigurieren**
  
  > `$ aws configure`

![CLI Config](images/aws_configure.png)

  **AWS Command Line Interface testen**
  
  > `$ aws iam list-users`

## AWS Cloud Formation
- Benutze das CMD um in deinen Project Ordner zu wechseln in welchem das yaml file liegt.


 **Führe folgenden Befehl aus:**
  
  > `$ aws cloudformation create-stack --stack-name ec2-example --template-body file://ec2.yaml --parameters ParameterKey=EnvironmentType,ParameterValue=dev ParameterKey=KeyPairName,ParameterValue=dam-auto`

**You can Update the Stock by using the update-stack command **
  
  > `$ aws cloudformation update-stack --stack-name ec2-example --template-body file://ec2.yaml`


**You can Delete the Stock**
  
  > `$ aws cloudformation delete-stack --stack-name ec2-example`

**You can see the Stacks Process and Errors here**

![CLI Version](images/aws_stack.png)

**Shows the new Stack**
  
  > `$ aws cloudformation describe-stacks`

---

web: [`Weblnk`](https://www.linkl.com),
---

> [⇧ **Zurück zur Hauptseite**](/README.md)

---
