---
title: Azure Open AI em uma VNet
tags: azure, openai, segurança, redes
author: Kenakamu
---

Os modelos GPT estão hospedados em diversos provedores de serviço, e a **Microsoft Azure** é um deles.

Embora os modelos sejam os mesmos, há muitas diferenças entre os provedores, incluindo:

- **Custo**  
- **Funcionalidades**  
- **Tipos e versões dos modelos**  
- **Localização geográfica**  
- **Segurança**  
- **Suporte**  
- E outros.  

Um dos aspectos mais importantes ao usar esses serviços em um ambiente corporativo é, naturalmente, a **segurança**.

Ao utilizar os recursos de segurança de rede da Azure com o Azure Open AI, os clientes podem consumir o serviço Open AI dentro de uma **VNet (Virtual Network)**, garantindo que nenhuma informação flua pela rede pública.

---

## Exemplo de Implantação

O repositório de exemplos do Azure fornece arquivos Bicep para implementar o Azure Open AI em um ambiente de VNet.

GitHub: [openai-enterprise-iac](https://github.com/Azure-Samples/openai-enterprise-iac)

Os principais recursos utilizados nesses Bicep são:

- **VNet**  
- **Integração da VNet para o Web App**  
- **Private Endpoint para o Azure Open AI**  
- **Private Endpoint para o Cognitive Search**  
- **Zona DNS Privada**  

Utilizando esses recursos, todo o tráfego de saída do Web App será roteado apenas dentro da VNet, e todos os nomes serão resolvidos em endereços IP privados. O Open AI e o Cognitive Search desativam os endereços IP públicos, eliminando interfaces públicas disponíveis.

---

## Implantação

O arquivo Bicep criará os seguintes recursos no Azure:

![Arquitetura](#) <!-- Adicione o link para a imagem da arquitetura, se necessário -->

Vamos realizar a implantação e verificar como funciona. Criei um grupo de recursos na região East US para meus próprios testes.

### Comandos para Implantação

```bash
git clone https://github.com/Azure-Samples/openai-enterprise-iac
cd openai-enterprise-iac
az group create -n openaitest -l eastus
az deployment group create -g openaitest -f .\infra\main.bicep
