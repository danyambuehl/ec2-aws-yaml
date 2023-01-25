AWS
====

# Ziel

Ziel ist es mit AWS CLI und AWS Cloud Formation eine EC2 Instance mit allem was dazugehört zu deployen. 

# Voraussetzung
**KeyPair File für SSH vorhanden**
 
 - In der AWS Console gehe zum EC2 Widget unter dem Punkt KeyPairs
 - Wenn du noch keinen erstellt hast, erstelle nun ein neues Keypair File mit einem belibigen Namen im .pem format. 
 - Und lege das Key File lokal auf deinem Computer ab. 

**Identity and Access Management (IAM) ein User mit Admin rechten erstellen**
 
 - Gehe zu Webconsole des IAM, wähle Users und erstelle einen neuen User mit AdministratorAccess.
 - Unter "Security Credentionals" clicke auf den Button "Create access key"
 - Wähle Command Line Interface(CLI) aus, bestätige die Empfehlungen und erstelle einen neuen Access Key. 
 - Speichere den Access Key und den Secret Access Key bei dir Lokal ab.

**AWS Command Line Interface download and install**

Download und installiere die [`AWS CLI`](https://aws.amazon.com/cli/)

 Windows CMD Öffnen und Version überprüfen
![CLI Version](../00_images/aws_cli.png)


# AWS Command Line Interface

  **AWS Command Line Interface Verbindung Konfigurieren**

Hier wird die Verbindung der AWS CLI zum erstellten User Access Key und Secret Acces Key hergestellt:
Die Region ausgewählt 
Und das Config File Format definiert.  

  > `$ aws configure`

![CLI Config](00_images/aws_configure.png)

  **AWS Command Line Interface testen**

Nun Sollte zumindest der erstelle User hier angezigt werden.

  > `$ aws iam list-users`

## AWS Cloud Formation

Benutze das CMD um in deinen Project Ordner zu wechseln in welchem das yaml file liegt.


 **Erstellen einer EC2 Instance mit Template ec2.yaml**

 Mit diesem Befehl können wir eine neue EC2 Instance wie im ec2.yaml konfiguriert ist erstellen. 
 Dabei wurde das yaml File so dynamisch erstellt das noch zusätliche Paramerter angegeben werden können/müssen.
 Dies führt dazu das dieses yaml Variabler genutzt werden kann von anderen Benutzern oder in anderen Umgebungen.
  - Mit --stack-name wird der stack Name definiert 
  - template-body das yaml file angegeben 
  - ParameterKey=EnvironmentType,ParameterValue=dev -> wird die dev Parameter für EnvironmentType weitergegeben mit diesem im yaml File definiert ist welche EC2-Instance grösse erstellt wird. 
  - ParameterKey=KeyPairName,ParameterValue=dam-auto -> gibt das bei mir "dam-auto" genannte keypair File mit. 
  
  > `$ aws cloudformation create-stack --stack-name ec2-example --template-body file://ec2.yaml --parameters ParameterKey=EnvironmentType,ParameterValue=dev ParameterKey=KeyPairName,ParameterValue=dam-auto`

**Zeigt den neuen Stack an**

Hier wird der neue Stack angezeigt 
  
  > `$ aws cloudformation describe-stacks`
![CLI Version](00_images/aws_stack_status.png)

**Auf die EC2 Instance verbinden**

Nun wurde die yaml Datei so ergänzt, dass man unter OutputKey: PublicConnect direkt das benötigte SSH Kommando generiert wird, um sich auf der neuen Linux Maschine zu verbinden. 
Dazu öffnet man z.B. eine GitBash Console, wechselt in das Verzeichnis wo das zuvor generierte Keyfile liegt (bei mir dam-auto.pem).
Und braucht dann nur noch den Befehl in die Console zu kopieren.

![CLI Version](00_images/aws_ssh.png)


**Mit dem Befehl update-stack Stock aktuallisieren**

Mit dem Befehl update-stack kann man änderungen im yaml file machen und diese auf den bestehenden Stock zu aktualisieren*
  
  > `$ aws cloudformation update-stack --stack-name ec2-example --template-body file://ec2.yaml`

**Den Stock wieder löschen**
  
  > `$ aws cloudformation delete-stack --stack-name ec2-example`

**Sie können den Stack Status und die Fehler hier sehen**

Es ist auch möglich den erstellten Stock und Status in der AWS Console einzusehen. 

![CLI Version](00_images/aws_stack.png)

# Das YAML File wurde sehr Deteiliert mit Komentaren versehen so das dies Selbsterklärend ist. 

- Hier das Erstellte Script mit Kommentaren
```
# Indicates the format version of the CloudFormation template.
AWSTemplateFormatVersion: 2010-09-09
Description: This script creates an EC2 instance, a security group and allows traffic on ports 80, 443 and 22. It also returns the PublicDNS and SSH Connection command of the created EC2 instance in the Outpoot.

# Defines input parameters that are passed when creating the stack. In this case, it takes two parameters:
Parameters:
# Defines two Parameter Option for Deploying the new EC2 Instance dev and test. You can add this Parameter on the Deploy commend
  EnvironmentType:
    Description: "Specify the Type of the EC2."
    Type: String
    Default: dev  # When no Parameter is given on the Deploy commend this will be the Default 
    AllowedValues: #  We use the AllowedValues constraint so the parameter valve must be one of the two options dev or test
      - dev   # In Mapping the dev Values is mappt to a t2.nano instance
      - test  # In Mapping the test Values is mappt to a t2.micro instance
    ConstraintDescription: must specify dev, or test.
  KeyPairName:  # KeyPair Parameter so you can add your Persenal KeePair File Name : z.b dam-auto which is refering on the dam-auto.pem File in the same Folder as the Deploy commend ist executed
                # If there is no Default: attribute like here in KeyPairName the Users must specify a keyname value at the stack creation
    Type: String
    MinLength: 1  # We use the MinLength constraint so the parameter value must be at leaste 1 character long
    MaxLength: 32 # We use the MaxLength constraint so the parameter value can be a maximum of 32 character long
    Description: The name of an existing Amazon EC2 key pair to SSH into the Amazon EC2 instances.

# It maps the EnvironmentType parameter to the corresponding InstanceType of the EC2 instance.
Mappings:
  EnvironmentToInstanceType:
    dev:
      InstanceType: t2.nano
    test:
      InstanceType: t2.micro

# Defines the AWS resources that are created as part of the stack.
Resources:
  WebAppInstance:
    Type: AWS::EC2::Instance
    Properties:   # This propertie of the EC2 Instance has multiple subproperties -ImageID -Instance Type -KeyName and -Secuirty GroupIds
      ImageId: ami-0778521d914d23bc1 # ImageID valid only in us-east-1 region for Ubuntu 20.04
      InstanceType:  # An EC2 instance of type t2.nano or t2.micro depending on the EnvironmentType passed as parameter
        !FindInMap [
          EnvironmentToInstanceType,
        !Ref EnvironmentType,   # This Referance function is used to link to the EnvironmentType definded in the Parameter, so it will take the Valve we give it with the Deploy commend
          InstanceType,
        ]
      KeyName: !Ref KeyPairName # Another Referance to the KeyPariName Parameter. It will take the Valvue we give it with the Deploy commend
      SecurityGroupIds:  # The SecurityGroups property is a list of security groups In this case its a Reference to the WebAppSecurityGroup Object just two lines lower
        - !Ref WebAppSecurityGroup # Another Referance to the creation of the WebAppSecurityGroup one line lower

# A security group that allows inbound traffic on ports 80, 443 and 22 and outbound traffic.
  WebAppSecurityGroup:
    Type: AWS::EC2::SecurityGroup
    Properties:
      GroupName: !Join ["-", [webapp-security-group, !Ref EnvironmentType]] # The name of the security group is based on the fix String "webapp-security-group" and the EnvironmentType passed as parameter
      GroupDescription: "Allow HTTP/HTTPS and SSH inbound and outbound traffic"
      SecurityGroupIngress:
        - IpProtocol: tcp
          FromPort: 80
          ToPort: 80
          CidrIp: 0.0.0.0/0
        - IpProtocol: tcp
          FromPort: 443
          ToPort: 443
          CidrIp: 0.0.0.0/0
        - IpProtocol: tcp
          FromPort: 22
          ToPort: 22
          CidrIp: 0.0.0.0/0

# Defines the output values that are returned after the stack is created
# You can see it when you go to the AWS Web Console -> Cloud Formation -> Stacks -> Outputs 
# Or in the AWS CLI with the Commend: aws cloudformation describe-stacks
Outputs:
      # It returns the PublicDNS of the EC2 instance
   PublicDNS:
    Description: "Shows the Public DNS Name"
    Value: !GetAtt WebAppInstance.PublicDnsName  

      # Shows how to Connect to the EC2 Instance by Combining the "ssh -i" String with a space "" , a Referation to the KeyPair Attribut, another String ".pem ubuntu@" and getting the PublicDNS Name of the EC2 Instanc with !GetAtt
   PublicConnect:
    Description: "Shows the exact commend to connect to the newly deployed EC2 Instance"
    Value: !Join ["", [ssh -i , " " ,  !Ref KeyPairName,.pem ubuntu@,  !GetAtt WebAppInstance.PublicDnsName]]   # The Fn::GetAtt function will get the PublicDNSName Parameter from the newly installed WebAppInstance EC2 Instance





```
---

web: [`yaml File`](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/gettingstarted.templatebasics.html),
web: [`yaml Template`](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/conditions-sample-templates.html),
web: [`Provisioning`](https://jennapederson.com/blog/2021/6/21/provisioning-an-ec2-instance-with-cloudformation-part-1/),
---

> [⇧ **Zurück zur Hauptseite**](/README.md)

---
