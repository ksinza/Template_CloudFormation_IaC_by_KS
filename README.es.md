# Infraestructura como Código (IaC) con CloudFormation - Plantilla 

Este proyecto proporciona una plantilla de CloudFormation para desplegar una arquitectura serverless en AWS. Incluye un API Gateway, una función Lambda y una tabla de DynamoDB, junto con los roles y permisos de IAM necesarios.

## Arquitectura

- **AWS API Gateway**: Expone un endpoint RESTful (`POST`) que activa la función Lambda.
- **AWS Lambda**: Procesa las solicitudes entrantes e interactúa con la tabla de DynamoDB.
- **AWS DynamoDB**: Una tabla de base de datos NoSQL utilizada para el almacenamiento de datos.
- **Roles y Políticas de IAM**: Configurados con permisos específicos para el acceso a DynamoDB, CloudWatch Logs, EC2 y S3.

## Requisitos Previos

- Una cuenta de AWS.
- El código de la función Lambda subido a un bucket de S3 en formato `.zip`.
- AWS CLI instalado y configurado (opcional, para despliegue por consola).

## Parámetros

| Parámetro | Descripción |
|-----------|-------------|
| `DynamoName` | El nombre de la tabla de DynamoDB. |
| `DynamoKey` | El nombre de la clave de partición para la tabla de DynamoDB. |
| `LambdaName` | El nombre de la función Lambda. |
| `LambdaRuntime` | El entorno de ejecución para la Lambda (ej. `python3.13`, `nodejs24.x`). |
| `LambdaBucket` | El nombre del bucket de S3 donde se almacena el archivo `.zip` de la Lambda. |
| `ZipName` | El nombre del archivo `.zip` en el bucket de S3. |

## Despliegue

### Usando la Consola de AWS
1. Inicie sesión en la consola de AWS CloudFormation.
2. Cree un nuevo stack y cargue el archivo `template.yml`.
3. Complete los parámetros requeridos.
4. Siga las instrucciones para crear los recursos.

### Usando AWS CLI
```bash
aws cloudformation create-stack 
  --stack-name mi-stack-serverless 
  --template-body file://template.yml 
  --parameters 
    ParameterKey=DynamoName,ParameterValue=MiTabla 
    ParameterKey=DynamoKey,ParameterValue=id 
    ParameterKey=LambdaName,ParameterValue=MiFuncion 
    ParameterKey=LambdaRuntime,ParameterValue=python3.13 
    ParameterKey=LambdaBucket,ParameterValue=mi-bucket-de-codigo 
    ParameterKey=ZipName,ParameterValue=funcion.zip 
  --capabilities CAPABILITY_IAM
```

## Salidas (Outputs)
El stack exporta varios recursos que pueden ser utilizados por otros stacks de CloudFormation:
- `LambdaPolicyDynamo`
- `LambdaPolicyEC2`
- `LambdaPolicyCW`
- `LambdaFunction` (ARN)
- `RootResourceId` (ID de API Gateway)


## Author

**Kevin Sinza Salcedo** *Ingeniero en Sistemas | Desarrollando de Software*
[LinkedIn](https://www.linkedin.com/in/kevin-sinza-967488105)
