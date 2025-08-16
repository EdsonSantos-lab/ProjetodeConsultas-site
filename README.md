# Projeto: Automação de Preenchimento de Formulários com Selenium
Descrição:
Este projeto demonstra a automação de tarefas repetitivas em navegadores web usando Python e Selenium WebDriver. Ele lê dados de uma planilha Excel e preenche automaticamente formulários em um site local (index.html), simulando interações humanas como cliques, preenchimento de campos e navegação entre abas.

Funcionalidades implementadas:
Leitura de dados de Excel

Utiliza Pandas para importar uma planilha chamada "Cópia de Processos.xlsx".

Cada linha da tabela contém informações como: Cidade, Nome, Advogado e Processo.

python
Copiar
Editar
import pandas as pd
tabela = pd.read_excel("Cópia de Processos.xlsx")
display(tabela)
Automação do navegador com Selenium

Inicializa o ChromeDriver de forma dinâmica usando webdriver_manager.

Navega até a página local (index.html).

python
Copiar
Editar
from selenium import webdriver
from selenium.webdriver.chrome.service import Service
from webdriver_manager.chrome import ChromeDriverManager

servico = Service(ChromeDriverManager().install())
navegador = webdriver.Chrome(service=servico)
Interação com elementos dinâmicos

Acessa menus dropdown usando ActionChains para simular o movimento do mouse.

Clica nos links correspondentes às cidades listadas na planilha.

python
Copiar
Editar
from selenium.webdriver import ActionChains
botao = navegador.find_element(By.CLASS_NAME, 'dropdown-menu')
ActionChains(navegador).move_to_element(botao).perform()
navegador.find_element(By.PARTIAL_LINK_TEXT, cidade).click()
Preenchimento automático de formulários

Preenche campos de Nome, Advogado e Número do Processo.

Submete o formulário com o botão registerbtn.

Lida com alertas do navegador automaticamente.

python
Copiar
Editar
navegador.find_element(By.ID, 'nome').send_keys(tabela.loc[linha, "Nome"])
navegador.find_element(By.ID, 'advogado').send_keys(tabela.loc[linha, "Advogado"])
navegador.find_element(By.ID, 'numero').send_keys(tabela.loc[linha, "Processo"])
navegador.find_element(By.CLASS_NAME, 'registerbtn').click()
alerta = navegador.switch_to.alert
alerta.accept()
Gerenciamento de abas

O script gerencia múltiplas abas do navegador para cada registro processado.

Alterna entre a aba original e a nova aba para garantir que cada formulário seja preenchido corretamente.

Benefícios do Projeto:
Automação de tarefas repetitivas, reduzindo erros manuais.

Demonstra habilidades em Python, Selenium, manipulação de abas, alertas e Excel.

Pode ser aplicado a diferentes sistemas de cadastro, testes de software ou entrada de dados em massa.

Próximos Passos / Melhorias Futuras:
Adicionar validação de campos vazios antes de enviar o formulário.

Implementar tratamento de erros caso algum elemento não seja encontrado.

Tornar o script mais dinâmico, permitindo que diferentes planilhas ou sites sejam processados sem alterações no código 
