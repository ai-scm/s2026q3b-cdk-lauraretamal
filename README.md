# Ejercicio práctico: AWS CDK

## Objetivo

Crear una aplicación utilizando AWS CDK con TypeScript, siguiendo el tutorial oficial de AWS, y modificarla para crear un bucket de Amazon S3 y cargar automáticamente un archivo de texto con el contenido `hola mundo`.

## 1. Creación del proyecto

Se creó el proyecto con:

```bash
mkdir hello-cdk
cd hello-cdk
cdk init app --language typescript
```

El proyecto utiliza TypeScript y AWS CDK v2.

## 2. Configuración de AWS

Se configuró el entorno de AWS indicando la cuenta y la región que utilizaría el stack.

Después se realizó el bootstrap del entorno:

```bash
cdk bootstrap
```

El bootstrap prepara el entorno de AWS para realizar despliegues mediante CDK.

## 3. Creación de la Lambda

Se definió una función AWS Lambda utilizando el construct `Function` de AWS CDK.

La función utiliza Node.js 20 y devuelve el mensaje `Hello World!`.

También se creó una Function URL para poder invocar la función mediante HTTP.

## 4. Compilación y síntesis

Se compiló el proyecto con:

```bash
npm run build
```

Luego se utilizó:

```bash
cdk synth
```

Este comando sintetiza los recursos definidos en CDK en una plantilla de AWS CloudFormation.

## 5. Despliegue

El stack se desplegó utilizando:

```bash
cdk deploy
```

Después del despliegue se verificó la Function URL de la Lambda y se confirmó que la función respondía correctamente.

## 6. Modificación para Amazon S3

Para cumplir con el ejercicio se modificó el stack para crear un bucket de Amazon S3.

También se agregó el archivo:

```text
files/hola-mundo.txt
```

cuyo contenido es:

```text
hola mundo
```

Para cargar automáticamente el archivo al bucket se utilizó `BucketDeployment` de AWS CDK.

La implementación utiliza:

```typescript
import * as s3 from 'aws-cdk-lib/aws-s3';
import * as s3deploy from 'aws-cdk-lib/aws-s3-deployment';
```

y:

```typescript
const bucket = new s3.Bucket(this, "HelloWorldBucket");

new s3deploy.BucketDeployment(this, "DeployFiles", {
  sources: [s3deploy.Source.asset("./files")],
  destinationBucket: bucket,
});
```

De esta forma, el bucket y el archivo son gestionados mediante CDK y el archivo se carga automáticamente durante el despliegue.

## 7. Verificación

Después de ejecutar nuevamente:

```bash
cdk synth
cdk deploy
```

se verificó el bucket creado en Amazon S3 y se confirmó que contiene el archivo `hola-mundo.txt` con el contenido `hola mundo`.

## 8. Eliminación de recursos

El tutorial indica que los recursos pueden eliminarse mediante:

```bash
cdk destroy
```

Este comando elimina el stack de CloudFormation y los recursos administrados por él.
