# Engenharia de Atributos em Dados Médicos

## Definição do Problema

As readmissões hospitalares (quando um paciente recebe alta, mas é internado novamente pouco tempo depois) são caras e refletem as inadequações no sistema de saúde.

Nos Estados Unidos,  o tratamento de pacientes diabéticos readmitidos excede 300 milhões de dólares por ano. Identificação precoce de pacientes que enfrentam um alto risco de readmissão pode permitir que os profissionais de saúde conduzam investigações adicionais e possam impedir futuras readmissões. Isso não apenas melhora a qualidade do atendimento, mas também reduz as despesas médicas em readmissão.

Diabetes é a sétima principal causa de morte (dados de 2016, fonte ao final do texto) no mundo e afeta cerca de 23,6 milhões de pessoas só nos EUA e milhões de pessoas são diagnosticadas com diabetes a cada ano em todo mundo.

Segundo a Associação Americana de Diabetes, o custo do atendimento a pacientes diabéticos e pré-diabéticos nos Estados Unidos é o maior do mundo. Essa epidemia global afeta mais de 350 milhões de pessoas, com 3 milhões de pessoas morrendo a cada ano devido a complicações relacionadas ao diabetes, predominantemente cardiovasculares ou nefropáticas.

A readmissão hospitalar é uma das principais preocupações no tratamento do diabetes, com milhões de dólares sendo gastos no tratamento de pacientes diabéticos que precisam ser readmitidos em um hospital após receberem alta.

Logo, a necessidade de readmissão indica que cuidados inadequados foram fornecidos ao paciente no momento da primeira admissão. A taxa de readmissão se tornou uma métrica importante para medir a qualidade geral de um hospital.

O objetivo deste trabalho é identificar os pacientes diabéticos de alto risco por meio de estratificação de risco de registros médicos eletrônicos. Usaremos registros eletrônicos de dados médicos, como resultados dos exames, nível de insulina, diagnóstico de outras doenças, etc.

Foi realizado um extenso trabalho de engenharia de atributos e várias outras técnicas. Foram justificadas todas as nossas escolhas durante o desenvolvimento do projeto e entregue o resultado da análise através de diversos gráficos.

Os EUA mantém um programa constante de redução de readmissão de pacientes:
Hospital Readmissions Reduction Program (HRRP)
https://www.cms.gov/Medicare/Quality-Initiatives-Patient-Assessment-Instruments/Value-Based-Programs/HRRP/Hospital-Readmission-Reduction-Program

Outras Referências:

The top 10 causes of death
https://www.who.int/news-room/fact-sheets/detail/the-top-10-causes-of-death

Associação Americana de Diabetes
https://www.diabetes.org/

## Fonte de Dados

Usaremos o conjunto de dados, "Diabetes 130-US hospitals for years 1999-2008", que foi baixado do UCI Machine Learning Repository:

http://archive.ics.uci.edu/ml/datasets/diabetes+130-us+hospitals+for+years+1999-2008

Os dados representam 10 anos (1999-2008) de atendimento clínico em 130 hospitais dos EUA e redes de distribuição integradas com 100.000 observações e 50 recursos (variáveis) que representam os registros eletrônicos com resultados de exames dos pacientes e dados sobre cada hospital. A coleta dos dados foi descrita pelos autores conforme abaixo:

O controle da hiperglicemia em pacientes hospitalizados tem uma influência significativa no resultado, tanto em termos de morbidade quanto de mortalidade. No entanto, existem poucas avaliações nacionais sobre o tratamento do diabetes durante a hospitalização que podem servir de base para a mudança.

Essa análise de um grande banco de dados clínicos (74 milhões de encontros únicos correspondentes a 17 milhões de pacientes únicos) foi realizada para fornecer essa avaliação e encontrar orientações futuras que possam levar a melhorias na segurança do paciente. Quase 70.000 encontros de pacientes internados com diabetes foram identificados com detalhes suficientes para análise. A regressão logística multivariável foi usada para ajustar a relação entre a medida da HbA1c e a readmissão precoce, enquanto o controle de covariáveis, como dados demográficos, gravidade e tipo da doença, e tipo de admissão.

Os resultados mostram que a medição da HbA1c foi realizada com pouca frequência (18,4%) no ambiente hospitalar. O modelo estatístico sugere que a relação entre a probabilidade de readmissão e a medição da HbA1c depende do diagnóstico primário. Os dados sugerem ainda que a maior atenção ao diabetes refletida na determinação da HbA1c pode melhorar os resultados dos pacientes e reduzir o custo dos cuidados hospitalares.

HbA1c é uma medida de quão bem o seu açúcar no sangue está controlado durante um período de cerca de 3 meses. Essencialmente, dá uma boa ideia de quão altos ou baixos, em média, foram os níveis de glicose no sangue.

Descrição completa do trabalho de coleta dos dados:

Impact of HbA1c Measurement on Hospital Readmission Rates: Analysis of 70,000 Clinical Database Patient Records
https://www.hindawi.com/journals/bmri/2014/781670/

## Dicionário de Dados

Dicionário de Dados é a descrição de cada variável em nosso conjunto de dados. Aqui o
dicionário do dataset usado no projeto:

0- encounter_id - identificador único de um encontro do pesquisador com o paciente.

1- patient_nbr - identificador exclusivo de um paciente.

2- race - valores: Caucasian, Asian, African American, Hispanic e other.

3- gender - valores: male, female, and unknown/invalid.

4- age - agrupados em intervalos de 10 anos: (0, 10), (10, 20), ..., (90, 100).

5- weight - peso em libras.

6- admission_type_id - identificador inteiro correspondente a 9 valores distintos, por
exemplo, "emergência, urgência, eletiva, recém-nascido e não disponível".

7- discharge_disposition_id - identificador inteiro correspondente a 29 valores distintos,
por exemplo, "enviado para casa, expirou e não está disponível".

8- admission_source_id - identificador inteiro correspondente a 21 valores distintos, por
exemplo, "encaminhamento médico, e transferência de um hospital".

9- time_in_hospital - número inteiro de dias entre a admissão e a alta.

10- payer_code - identificador inteiro correspondente a 23 valores distintos, por
exemplo, Blue Cross / Blue Shield, Medicare e auto-pagamento".

11- medical_specialty - identificador inteiro de uma especialidade do médico admitidor,
correspondente a 84 valores distintos, por exemplo, cardiologia, medicina interna, família /
clínica geral e cirurgião".

12- num_lab_procedures - número de testes de laboratório realizados durante a
consulta.

13- num_procedures - número de procedimentos (exceto testes de laboratório)
realizados durante a consulta.

14- num_medications - número de medicamentos genéricos distintos administrados
durante a consulta.

15- number_outpatient - número de consultas ambulatoriais do paciente no ano anterior
a consulta.

16- number_emergency - número de visitas de emergência do paciente no ano anterior
a consulta.

17- number_inpatient - número de visitas hospitalares do paciente no ano anterior a
consulta.

18- diag_1 - diagnóstico primário (codificado como três primeiros dígitos da CID9); 848
valores distintos.

19- diag_2 - diagnóstico secundário (codificado como três primeiros dígitos da CID9); 923
valores distintos.

20- diag_3 - diagnóstico secundário adicional (codificado como três primeiros dígitos da
CID9); 954 valores distintos.

21- number_diagnoses - número de diagnósticos inseridos no sistema.

22- max_glu_serum - teste sérico de glicose que indica a faixa do resultado ou se o teste
não foi realizado. Valores: > 200, > 300, normal e nenhum, se não for medido.

23- A1Cresult - teste A1c que indica o intervalo do resultado ou se o teste não foi
realizado. 

Valores: > 8 (se o resultado for maior que 8%), > 7 (se o resultado for maior que 7%,
porém menor que 8%), normal (se o resultado for inferior a 7%) e nenhum, se não for medido.

Na sequência temos os recursos de 24 a 46 para os nomes dos medicamentos genéricos:

metformina, repaglinida, nateglinida, clorpropamida, glimepirida, acetohexamida,
glipizida, gliburida, tolbutamida, pioglitazona, rosiglitazona, acarbose, miglitol, troglitazona,
insulazforamida, examide, sitaglagliptida, sitazagliptida , glipizida-metformina, glimepiridapioglitazona,
metformina-rosiglitazona e metformina-pioglitazona,

Cada um desses recursos indica se o medicamento foi prescrito ou se houve uma alteração na dosagem. 
Valores: "up" se a dose foi aumentada durante a consulta.

47- change - indica se houve alteração nos medicamentos para diabéticos (dosagem ou
nome genérico). Valores: "change" e "no change".

48- diabetesMed - indica se houve algum medicamento diabético prescrito. Valores:
"sim" e "não".

49- readmitted - readmitido, "Dias para readmissão hospitalar. Valores: <30 (se o
paciente foi readmitido em menos de 30 dias), > 30 (se o paciente foi readmitido em mais de 30
dias) e No, para nenhum registro de readmissão.


Nota: Códigos ICD-9 ou CID-9 (International Classification of Diseases ou Código
Internacional de Doenças).
