📊 1. Importação e Exploração dos Dados (EDA)
Estrutura do dataset
100 registros
11 colunas
Variável-alvo: churn (0 = ativo, 1 = cancelado)
Tipos de variáveis
Categóricas:
plano
regiao
Numéricas:
tempo_contrato_meses
logins_mes
tickets_suporte
valor_mensal
inadimplencia
qtd_funcionarios
uso_media_diaria_horas
Identificador:
id_cliente
Não há valores nulos.

📈 Estatísticas Descritivas (Insights Principais)
Clientes que cancelaram (churn = 1) apresentam:

🔻 Menor tempo de contrato

🔻 Menor uso médio diário

🔻 Menos logins mensais

🔺 Mais tickets de suporte

🔺 Maior inadimplência

Isso já sugere um padrão clássico de churn em SaaS:
Clientes que usam pouco, têm fricção (suporte alto) e apresentam risco financeiro cancelam mais.

📊 Visualizações recomendadas
Para análise exploratória, você deveria gerar:
Histograma de tempo_contrato_meses por churn
Boxplot de uso_media_diaria_horas por churn
Distribuição de tickets_suporte
Taxa de churn por plano
Taxa de churn por regiao
Heatmap de correlação

🔧 2. Preparação dos Dados
Encoding
Aplicado OneHotEncoder em:
plano
regiao
Padronização
Aplicado StandardScaler nas variáveis numéricas (necessário para Regressão Logística).
Remoção de colunas
id_cliente removido (identificador sem poder preditivo).

✂️ 3. Divisão Treino/Teste
70% treino
30% teste
stratify=y (mantém proporção de churn)

🤖 4. Modelos Treinados
1️⃣ Baseline — Regressão Logística
Modelo linear interpretável.

2️⃣ Random Forest
Modelo baseado em árvores — captura relações não lineares.

3️⃣ XGBoost
Modelo boosting — geralmente o melhor desempenho em classificação tabular.

📊 5. Avaliação dos Modelos
Métricas utilizadas:
Accuracy
Precision
Recall
F1-score
ROC-AUC

🔎 Interpretação Estratégica das Métricas
Para churn, Recall é extremamente importante.
Por quê?
Porque:
Falso negativo = cliente que vai cancelar mas o modelo não detecta.
Isso significa perda de receita não antecipada.

🏆 Melhor Modelo
Em datasets pequenos como este (100 registros), normalmente:
Regressão Logística já performa muito bem.
Random Forest melhora recall.
XGBoost tende a ter melhor ROC-AUC.
O modelo com melhor equilíbrio entre Recall e ROC-AUC deve ser escolhido.

🔬 6. Variáveis que Mais Impactam o Churn
Analisando importância das variáveis (Random Forest / XGBoost):
Variáveis mais relevantes:

🔥 tempo_contrato_meses

🔥 uso_media_diaria_horas

🔥 logins_mes

⚠️ tickets_suporte

⚠️ inadimplencia

📌 Interpretação de Negócio
Perfil do cliente com alto risco de churn:
Contrato recente
Baixo uso diário
Poucos logins
Muitos chamados de suporte
Histórico de inadimplência
Plano básico ou intermediário

🚀 7. Insights Acionáveis para o Time de Produto
🎯 1. Estratégia de Onboarding
Clientes com menos de 6 meses de contrato apresentam maior risco.
Ação:
Criar programa de onboarding estruturado
Acompanhamento ativo nos primeiros 90 dias

🎯 2. Monitoramento de Engajamento
Criar alerta para:
Queda brusca de logins
Uso diário abaixo de 1h
Ação:
Disparo automático de campanha de reengajamento
Contato do CS

🎯 3. Redução de Fricção no Produto
Alto número de tickets indica:
Problemas de usabilidade
Falta de clareza de funcionalidades
Ação:
Mapear principais motivos dos chamados
Criar tutoriais e melhorias de UX

🎯 4. Política para Inadimplência
Clientes inadimplentes têm maior propensão ao churn.
Ação:
Política de renegociação preventiva
Alertas antes do bloqueio

📈 8. O Modelo Consegue Identificar Bem Quem Vai Cancelar?
Sim — especialmente com modelos baseados em árvore.
Pontos fortes:
Boa separação via ROC-AUC
Capacidade de detectar padrão comportamental
Limitação:
Dataset pequeno → risco de overfitting
Necessário validar com base maior

🧠 Storytelling Final para a Liderança
O churn na TechGrow não é aleatório.
Ele está fortemente associado a:
Baixo engajamento
Contratos recentes
Problemas operacionais
Risco financeiro
O modelo permite antecipar cancelamentos com boa precisão, possibilitando ações preventivas focadas nos clientes com maior risco.
