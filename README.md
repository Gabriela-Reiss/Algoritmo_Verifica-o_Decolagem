# Algoritmo de Verificação Operacional de Pré-Decolagem

## Sobre o projeto 

Este projeto tem como objetivo desenvolver um sistema de análise de telemetria para verificar as condições de segurança de uma nave antes da decolagem.

O sistema recebe um conjunto de dados de telemetria contendo informações relacionadas às condições internas e externas da nave, integridade estrutural, energia disponível, pressão dos tanques e funcionamento dos módulos críticos.

A partir desses dados, o script analisa cada registro e determina se as condições atendem aos critérios estabelecidos para a decolagem.

O resultado da análise pode ser:

✅ PRONTO PARA DECOLAR
❌ DECOLAGEM ABORTADA

Quando uma condição não atende aos critérios definidos, o sistema também apresenta o motivo pelo qual a decolagem foi abortada.

----------------------------------------------------------------------------------------------

## Objetivo 

O principal objetivo do projeto é demonstrar como dados de telemetria podem ser utilizados para apoiar uma decisão operacional de pré-decolagem.

O sistema busca:

- Ler e analisar dados de telemetria;
- Calcular o nível percentual de energia disponível;
- Verificar as condições de temperatura;
- Avaliar a integridade estrutural;
- Verificar a pressão dos tanques;
- Verificar o funcionamento dos módulos críticos;
- Identificar condições que possam impedir a decolagem;
- Apresentar uma decisão para cada registro analisado;
- Utilizar Inteligência Artificial como apoio para analisar os resultados e sugerir possíveis     riscos ou melhorias.

----------------------------------------------------------------------------------------------

## Entrada dos dados

O projeto permite trabalhar com duas formas de entrada de dados de telemetria.

**1. Dataset disponibilizado no projeto**

Para facilitar a reprodução dos testes e da execução apresentada neste repositório, é disponibilizado um dataset de exemplo:

Esse arquivo contém registros de telemetria utilizados para testar o algoritmo de avaliação das condições de pré-decolagem.

O usuário pode carregar esse arquivo no Google Colab e executar a análise utilizando os dados já preparados.

**2. Dataset gerado por Inteligência Artificial**

O projeto também permite que o usuário solicite à Inteligência Artificial a geração de um novo dataset de telemetria em formato .csv.

Nesse caso, a IA gera dados seguindo a estrutura e os critérios definidos pelo projeto:

| Variável                  |           Limite esperado | Unidade | Condição fora do limite                         |
| ------------------------- | ------------------------: | ------- | ----------------------------------------------- |
| `temperatura_interna_c`   |                   18 a 35 | °C      | Temperatura interna inadequada                  |
| `temperatura_externa_c`   |                   -5 a 30 | °C      | Temperatura externa inadequada                  |
| `integridade_estrutural`  |                         1 | —       | Integridade estrutural comprometida             |
| `energia_maxima_kwh`      |                900 a 1100 | kWh     | Capacidade máxima fora do padrão definido       |
| `energia_disponivel_kwh`  | Deve ser ≤ energia máxima | kWh     | Energia disponível superior à capacidade máxima |
| `nivel_energia`           |                      ≥ 60 | %       | Nível de energia insuficiente                   |
| `pressao_tanque_bar`      |                  95 a 145 | bar     | Pressão do tanque inadequada                    |
| `status_modulos_criticos` |                         1 | —       | Módulo crítico indisponível                     |


O arquivo gerado pode ser utilizado como entrada para o mesmo processo de análise.

Essa funcionalidade permite testar o algoritmo com diferentes conjuntos de dados, além do dataset de exemplo disponibilizado no repositório.

----------------------------------------------------------------------------------------------------

## Tecnologias utilizadas

- Python — desenvolvimento do algoritmo;
- Google Colab — ambiente de execução;
- Pandas — manipulação e análise dos dados;
- Dataset de telemetria — fonte dos dados utilizados na análise;
- Inteligência Artificial / API Gemini — análise complementar dos resultados.

---------------------------------------------------------------------------------------------------------------------------------------

## Funcionamento do algoritmo 

O script percorre os registros do dataset e analisa as condições de cada momento da telemetria.

Para cada registro, são obtidas as informações necessárias para realizar as verificações.

**-Cálculo da energia disponível**

O nível percentual de energia é calculado utilizando a energia disponível e a energia máxima:

nivel_energia = (energia_disponivel / energia_maxima) * 100

Dessa forma, o sistema consegue trabalhar com um percentual de energia em vez de utilizar somente os valores absolutos.

**-Regras de decisão**

A lógica utilizada pelo sistema considera que todas as condições críticas precisam estar dentro dos limites estabelecidos para que a nave seja considerada pronta para decolar.

Portanto, se pelo menos uma condição crítica apresentar uma situação fora do padrão estabelecido, o sistema registra a ocorrência e classifica o momento como:

"DECOLAGEM ABORTADA"

Isso permite que o sistema adote uma abordagem conservadora, priorizando a identificação de qualquer condição que possa representar risco operacional.

O algoritmo também registra os motivos encontrados durante a análise para facilitar a interpretação do resultado.

------------------------------------------------------------------------------------------------------

## Análise assistida por Inteligência Artificial

Além da análise baseada nas regras programadas, o projeto utiliza Inteligência Artificial como uma camada complementar de análise.

A IA recebe informações relacionadas aos registros de telemetria e aos resultados produzidos pelo algoritmo.

Com isso, ela pode auxiliar na:

- Interpretação dos resultados;
- Identificação de possíveis padrões de risco;
- Análise das condições encontradas;
- Sugestão de melhorias;

## Instruções para execução

**- Carregar o dataset**

Antes de executar a análise, o dataset de telemetria deve estar disponível para o código.

O arquivo deve conter as colunas utilizadas pelo algoritmo:

timestamp
temperatura_interna_c
temperatura_externa_c
integridade_estrutural
energia_maxima_kwh
energia_disponivel_kwh
pressao_tanque_bar
status_modulos_criticos

Anexe o arquivo CSV na aba "Arquivos" do Colab, e certifique-se de que o nome do arquivo seja o mesmo definido no algoritmo: "dataset_telemetria.csv", ou o renomeie no código.

Após carregar o arquivo, o código realiza a leitura dos dados e inicia o processo de análise.

**- Executar o algoritmo**
Execute as células responsáveis pela análise da telemetria.

O programa irá:

1. Percorrer os registros do dataset;
2. Obter os valores de telemetria;
3. Calcular o nível de energia;
4. Verificar as condições estabelecidas;
5. Determinar o status da decolagem;
6. Armazenar os resultados;
7. Apresentar as decisões e os motivos.


**-Executar a análise por IA**

Depois da execução das regras do algoritmo, a etapa de Inteligência Artificial pode ser executada.

Essa etapa utiliza os resultados obtidos anteriormente para gerar uma análise complementar.

Para isso, é necessário configurar a chave da API utilizada pelo projeto, acesse o site do Google IA Studio (), acesse sua conta Google e crie uma API Key.

Crie uma variável na aba "Secrets" do Colab e cole sua API Key como valor da variável.

Certifique-se que o nome da variável seja o mesmo nome definido no script: "GEMINI_API_KEY" ou o renomeie no código.

**Observação: Não é recomendável colocar sua chave de API diretamente no código**

----------------------------------------------------------------------------------------------------

## Executando o script

1. Carregamento do dataset e armazenamento em uma variácel:
<img width="1467" height="725" alt="image" src="https://github.com/user-attachments/assets/c7d091e2-73a5-40b6-bcc5-35f58465142e" />

2. Verificação dos dados do dataset:
 <img width="1542" height="581" alt="image" src="https://github.com/user-attachments/assets/7d452bae-75c7-4fc1-b04d-71450dff40e8" />

3. Criando variáveis para receber os dados do dataset:
<img width="537" height="292" alt="image" src="https://github.com/user-attachments/assets/e7ddf8f6-c3d8-4fd7-8569-e69e9f3ebf4c" />

4. Realização dos fluxos de decisão com base na análise da telemetria e cálculo do nível de energia:
<img width="950" height="632" alt="image" src="https://github.com/user-attachments/assets/7dd53a79-c304-4d9c-b3e8-28f9e8d90292" />

5. Armazenando os motivos (caso condições falsas, para justificar a decisão de "DECOLAGEM ABORTADA")
<img width="750" height="123" alt="image" src="https://github.com/user-attachments/assets/011178c0-4d6a-4318-b96c-ed352ea44e50" />

6. Visualizando as decisões:
<img width="302" height="101" alt="image" src="https://github.com/user-attachments/assets/e016cf84-a48f-4267-a5ba-da2cb2f9d523" />
<img width="902" height="651" alt="image" src="https://github.com/user-attachments/assets/616896e8-49ce-4483-b664-00932f8dc47f" />

8. Salvando os dados da telemetria e as decisões em um Data Frame:
<img width="510" height="276" alt="image" src="https://github.com/user-attachments/assets/856a3331-5b2d-42c0-b48e-6303683bd0aa" />

9. Visualizando o Data Frame gerado:
<img width="762" height="697" alt="image" src="https://github.com/user-attachments/assets/eb902921-79bd-4028-a1b3-6092778270c4" />

10. Conversão o Data Frame para JSON:
<img width="570" height="138" alt="image" src="https://github.com/user-attachments/assets/9015cb6b-130a-4c39-8234-cadb59caf7b9" />

11. Configurando a API Gemini:
<img width="957" height="415" alt="image" src="https://github.com/user-attachments/assets/ad6cfd5f-fde8-43d1-bbc5-91102710ad47" />

12. Enviando Prompt para a IA:
<img width="1008" height="512" alt="image" src="https://github.com/user-attachments/assets/c93ac984-d853-4327-83a2-3943f8a2d2de" />

13. Visualizando a resposta da IA:
<img width="1792" height="763" alt="image" src="https://github.com/user-attachments/assets/1bcfa42d-d227-458d-8e44-2a9f07bf0f19" />

---------------------------------------------------------------------------------------------------------






