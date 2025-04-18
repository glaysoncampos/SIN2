CRIE UM o aplicativo educacional possa implementar para simular o cálculo de uma conta de internação hospitalar de até 4 dias, conforme as regras e tabelas do IPASGO.Para fins de simplicidade, DEVE éSER estático e não inclui lógica de backend ou banco de dados. A implementação completa exigiria integração com JavaScript para cálculos dinâmicos e uma base de dados para armazenar as tabelas do IPASGO. ENTÃO SE NOS PARAMETROS DISSER QUE TEM QUE PEGAR FONTE DE DADOS EXTERNA, DESCONSIDERE É CRIE UMA SIMULADA COM SEUS PROPRIOS DADOS

Parâmetros de Entrada (Definidos pelo Usuário/Cenário):

Datas e Horários de Admissão e Alta do Paciente (essencial para calcular a permanência).
Tipo de Acomodação Utilizada (Enfermaria, Apartamento, UTI, etc.).
Diagnóstico Principal (Código CID-10).   
Procedimentos Médicos Realizados (Lista selecionável com base em códigos TUSS da Tabela Médica , indicando se houve anestesia, auxiliares, etc.).   
Materiais Utilizados (Lista selecionável com códigos TUSS/IPASGO da Tabela MAT/MED , com quantidades e status simulado de autorização).   
Medicamentos Administrados (Lista selecionável com códigos TUSS/IPASGO da Tabela MAT/MED , com quantidades/doses e status simulado de autorização).   
Visitas Médicas Diárias (Número de visitas, usando o código TUSS 10102019 / IPASGO 00020010 ).   
Lógica do Motor de Cálculo:

Calcular Permanência (Número de Diárias):
Aplicar a regra assumida ou configurada pelo usuário para contar os dias de internação, considerando datas/horas de admissão/alta e tratando casos < 24h e a possível aplicação de "Meia Diária". É crucial que a premissa utilizada seja claramente informada ao usuário do aplicativo.
Calcular Custo das Diárias: Multiplicar o número de diárias (calculado no passo 1) pela tarifa correspondente ao tipo de acomodação, obtida na Tabela de Serviços Hospitalares.   
Calcular Taxas Hospitalares: Somar os custos das taxas aplicáveis ao cenário (ex: Taxa de Sala Cirúrgica baseada no Porte Anestésico do procedimento principal, taxas de uso de equipamentos), conforme valores da Tabela de Serviços Hospitalares.   
Calcular Custos de Procedimentos: Para cada procedimento informado:
Buscar na Tabela Médica  o valor base do procedimento, o valor da anestesia (se aplicável), o valor dos auxiliares (se aplicável) e o valor de insumos associados (se houver).   
Somar esses componentes para obter o custo total do procedimento.
Calcular Custos de Materiais: Para cada material informado:
Buscar o preço unitário na Tabela MAT/MED.   
Verificar o status simulado da autorização. Se o item exige autorização e a simulação indica que não foi obtida, marcar o item como potencialmente glosado ou excluí-lo do cálculo final (conforme a lógica educacional desejada).
Multiplicar a quantidade utilizada pelo preço unitário.
Calcular Custos de Medicamentos: Para cada medicamento informado:
Buscar o preço unitário na Tabela MAT/MED.   
Verificar o status simulado da autorização e marcar se necessário.
Multiplicar a quantidade administrada pelo preço unitário.
Calcular Custos de Visitas Médicas (Escopo da Conta Hospitalar):
Opção 1 (Padrão): Excluir do cálculo, assumindo que são faturadas separadamente pelo médico.
Opção 2 (Alternativa): Incluir no cálculo se a simulação representar um cenário onde o hospital emprega o médico visitador. Multiplicar o número de visitas pelo valor do código TUSS 10102019 / IPASGO 00020010 da Tabela Médica. A premissa adotada deve ser clara.   
Somar Componentes: Adicionar os custos calculados nos passos 2 a 7 para obter o valor total simulado da conta hospitalar.
Saída (Conta Simulada):

Apresentar um resumo que pode mimetizar a estrutura da Conta Nosocomial  ou um formato de fatura padrão.   
Detalhar os custos por categoria: Diárias, Taxas, Procedimentos (listando códigos e valores individuais), Materiais (listando códigos, quantidades, valores unitários e totais), Medicamentos (idem).
Exibir o valor total final da conta simulada.
Incluir indicadores visuais ou notas para itens que seriam potencialmente glosados na simulação (ex: por falta de autorização prévia simulada).
