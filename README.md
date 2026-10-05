# AWS CDK - S3 Bucket

Proyecto realizado con AWS CDK y TypeScript para crear recursos de AWS mediante código.

## ¿Qué hace?

El proyecto crea:

- Una función AWS Lambda con una Function URL.
- Un bucket de Amazon S3.
- Un archivo `hola-mundo.txt` dentro del bucket con el contenido `hola mundo`.


## Comandos principales

Instalar dependencias:

```bash
npm install
```

Compilar el proyecto:

```bash
npm run build
```

Generar la plantilla de CloudFormation:

```bash
cdk synth
```

Desplegar los recursos:

```bash
cdk deploy
```

Eliminar los recursos creados:

```bash
cdk destroy
```

## Recursos principales

### AWS Lambda

Se crea una función Lambda que responde mediante una Function URL.

### Amazon S3

Se crea un bucket S3 y se utiliza `BucketDeployment` para cargar automáticamente el archivo `files/hola-mundo.txt`.

El archivo contiene:

```text
hola mundo
```

## Tecnologías

* AWS CDK v2
* TypeScript
* AWS Lambda
* Amazon S3
* AWS CloudFormation
