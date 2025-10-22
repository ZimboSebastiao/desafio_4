# Desafio AWS CloudFormation - Infraestrutura como Código

## Descrição do Projeto

Este repositório documenta minha jornada de aprendizado e implementação de infraestrutura automatizada usando AWS CloudFormation. O projeto consiste na criação de templates CloudFormation para provisionar recursos AWS de forma consistente e reproduzível.

## Objetivos Alcançados

- [x] Compreensão dos conceitos fundamentais do AWS CloudFormation
- [x] Criação de templates YAML para infraestrutura como código
- [x] Implementação de stacks automatizadas
- [x] Documentação clara do processo técnico
- [x] Organização do repositório no GitHub

### Conceitos Fundamentais

1. **Templates CloudFormation**: Estruturas YAML/JSON que definem a infraestrutura
2. **Stacks**: Instâncias implantadas dos templates
3. **Recursos**: Componentes AWS criados (EC2, VPC, S3, etc.)
4. **Parâmetros**: Valores personalizáveis durante a implantação
5. **Outputs**: Valores retornados após a criação da stack

### Melhores Práticas Aplicadas

- **Modularidade**: Templates separados por funcionalidade
- **Reutilização**: Parâmetros para customização
- **Validação**: Uso do `aws cloudformation validate-template`
- **Documentação**: Comentários detalhados nos templates

## Implementação

### Template Exemplo: VPC Básica

```yaml
AWSTemplateFormatVersion: '2010-09-09'
Description: 'VPC básica com subnets públicas e privadas'

Parameters:
  VpcCidr:
    Type: String
    Default: 10.0.0.0/16
    Description: CIDR block for the VPC

Resources:
  VPC:
    Type: AWS::EC2::VPC
    Properties:
      CidrBlock: !Ref VpcCidr
      EnableDnsHostnames: true
      Tags:
        - Key: Name
          Value: !Sub ${AWS::StackName}-vpc

Outputs:
  VpcId:
    Description: ID da VPC criada
    Value: !Ref VPC
    Export:
      Name: !Sub ${AWS::StackName}-VPCID
```

### Comandos Utilizados

```bash
# Validar template
aws cloudformation validate-template --template-body file://templates/vpc-basic.yml

# Criar stack
aws cloudformation create-stack \
  --stack-name minha-vpc \
  --template-body file://templates/vpc-basic.yml \
  --parameters ParameterKey=VpcCidr,ParameterValue=10.0.0.0/16

# Ver status da stack
aws cloudformation describe-stacks --stack-name minha-vpc

# Deletar stack
aws cloudformation delete-stack --stack-name minha-vpc
```

## Resultados Obtidos

- ✅ Stack criada com sucesso na AWS
- ✅ Recursos provisionados conforme especificado
- ✅ Templates validados e funcionais
- ✅ Documentação completa do processo


## Recursos Utilizados

- [Documentação AWS CloudFormation](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/Welcome.html)
- [AWS CloudFormation Designer](https://us-east-1.console.aws.amazon.com/cloudformation/designer)
- [GitHub Markdown Guide](https://docs.github.com/en/get-started/writing-on-github/getting-started-with-writing-and-formatting-on-github)

## Conclusão

Este desafio proporcionou uma compreensão sólida sobre infraestrutura como código com AWS CloudFormation. A capacidade de versionar, replicar e gerenciar infraestrutura de forma programática é fundamental para ambientes cloud modernos e este projeto foi um excelente ponto de partida.

