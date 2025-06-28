# 💰 SISTEMA_BANCÁRIO

Sistema bancário com saque, depósito e extrato criado em Python com visual colorido no terminal (ANSI).

> Desafio realizado na plataforma **Webdeal**, com objetivo de aplicar lógica de programação, controle de fluxo e boas práticas em Python.

---

## 👨‍💻 Desenvolvido por

**Matheus Rickson Sabino da Silva**

---

## 📌 Funcionalidades

- ✅ Depósito com validação de valor positivo
- ✅ Saque com:
  - Limite de **R$500 por saque**
  - Máximo de **3 saques por dia**
  - Verificação de saldo
- ✅ Visualização do extrato com saldo final
- ✅ Interface com **cores ANSI** no terminal:
  - Verde para sucesso
  - Vermelho para erros
  - Azul para títulos e menu
  - Amarelo para alertas

---

## 🧩 Estrutura do Código
```python


print('\033[1;34m' + '<->' * 10 + ' PYTHONBANK ' + '<->' * 10 + '\033[0m')
# Desenvolvido por Matheus Rickson Sabino da Silva

# CORES E ESTILOS PARA ENFEITAR
RESET = '\033[0m'
BRANCO = '\033[97m'
PRETO = '\033[30m'
VERMELHO = '\033[91m'
VERDE = '\033[92m'
AMARELO = '\033[93m'
AZUL = '\033[94m'
ROXO = '\033[95m'
CIANO = '\033[96m'
CINZA = '\033[90m'

NEGRITO = '\033[1m'
ITALICO = '\033[3m'
SUBLINHADO = '\033[4m'
saldo = 0.0  # SALDO INICIAL
extrato = ""  # ARMAZENA AS TRANSAÇÕES
limite_saque = 3  # MAXIMO DE SAQUES
saques_realizados = 0  # SAQUES EFETUADOS
LIMITE_VALOR_SAQUE = 500  # VALOR MAXIMO DE SAQUE

# Loop principal do sistema
while True:
    print(CINZA + "\n--- MENU BANCÁRIO ---" + RESET)
    print(NEGRITO + SUBLINHADO + "[1] Depositar")
    print("[2] Sacar")
    print("[3] Ver extrato")
    print("[4] Sair" + RESET)
    
    opcao = input("Escolha uma opção: ")

    # DEPÓSITO
    if opcao == "1":
        valor = float(input("Informe o valor para depósito: R$ "))
        if valor > 0:
            saldo += valor  # SOMA AO SALDO
            extrato += f"Depósito: R$ {valor:.2f}\n"
            print(VERDE + "Depósito realizado com sucesso!" +RESET)
        else:
            print(VERMELHO + "Valor inválido para depósito." + RESET)

    # Saque
    elif opcao == "2":
        valor = float(input("Informe o valor para saque: R$ "))

        # VERIFICAÇÃO PARA SAQUE
        if valor > saldo:
            print(VERMELHO + "Saldo insuficiente." + RESET)
        elif valor > LIMITE_VALOR_SAQUE:
            print(AMARELO + f"Limite por saque é R$ {LIMITE_VALOR_SAQUE}." + RESET)
        elif saques_realizados >= limite_saque:
            print(VERMELHO + "Número máximo de saques diários atingido." + RESET)
        elif valor <= 0:
            print(VERMELHO + "Valor inválido para saque." + RESET)
        else:
            saldo -= valor  # SUBTRI DO SALDO
            extrato += f"Saque: R$ {valor:.2f}\n"
            saques_realizados += 1
            print(VERDE + "Saque realizado com sucesso!" + RESET)

                # EXTRATO
    elif opcao == "3":
        print("\n--- EXTRATO ---")
        if extrato == "":
            print("Nenhuma movimentação realizada.")
        else:
            print(extrato)
        print(VERDE + f"Saldo atual: R$ {saldo:.2f}" +RESET)

        # SAI DO PROGRRAMA
    elif opcao == "4":
        print(AZUL + "Obrigado por usar nosso sistema bancário!"+ RESET)
        break  # Encerra o loop

    # OPÇÃO INVÁLIDA
    else:
        print(VERMELHO + "Opção inválida. Por favor, escolha entre 1 e 4." +RESET)
        break  # Encerra o loop

    
