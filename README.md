# Enclave Exercises

Este repositório contém a solução dos desafios propostos na atividade prática de Intel SGX.

## 🔧 Ambiente

A atividade é composta por 5 desafios, cada um valendo 2 pontos. Para começar:

1. Acesse seu ambiente virtual seguindo as instruções no guia fornecido:  
   **Guia para Utilização do Laboratório Virtual (.pdf)**

2. No ambiente, você encontrará dois arquivos:

- `enclave-atividade.signed.so`: Enclave fornecido pelo professor
- `enclave-atividade.edl`: Interface com todas as ECALLs e OCALLs do enclave

Você também pode baixá-los:

- [`enclave-atividade.edl`](./enclave-atividade.edl)
- [`enclave-atividade.signed.so`](./enclave-atividade.signed.so)

> ⚠️ Você **não** tem acesso ao código fonte do enclave. Sua tarefa é interagir com ele.

## 🚀 Como configurar

1. Clone o projeto base:

```bash
git clone https://github.com/Lohann/intel-sgx-template
cd intel-sgx-template
```

2. Compile o projeto base para garantir que tudo está funcionando:

```bash
make SGX_MODE=SIM
```

3. Agora:

- Copie `enclave-atividade.signed.so` para a raiz do projeto.
- Altere o valor da constante `ENCLAVE_FILENAME` no arquivo `app/app.h` para `enclave-atividade.signed.so`.
- Substitua o conteúdo do arquivo `enclave/enclave.edl` por `enclave-atividade.edl`.

4. Compile apenas o aplicativo (sem recompilar o enclave):

```bash
make clean
make SGX_MODE=SIM main
```

5. Execute:

```bash
./main
```

Se tudo estiver funcionando, você está pronto para os desafios!

## 🧩 Desafios

### ✅ Desafio 1 – Chamar o Enclave

Implemente uma chamada para a ECALL `ecall_verificar_aluno`, que recebe uma `string` como parâmetro.

### 🔐 Desafio 2 – Quebrar a Senha

Interaja com `ecall_verificar_senha`, que recebe um número inteiro entre `0` e `99999`.  
Sua tarefa é descobrir a senha correta por tentativa e erro (força bruta).

- Retorno:
  - `0`: senha correta
  - `-1`: senha incorreta

### 🔤 Desafio 3 – Sequência Secreta

Interaja com `ecall_palavra_secreta`, que recebe um `char[20]`.

- O enclave guarda uma sequência secreta de 20 letras maiúsculas.
- Ele substitui as letras incorretas por `'-'`, mantendo as letras corretas nas posições certas.
- Você deve descobrir a sequência completa testando diferentes combinações.

### 📈 Desafio 4 – Polinômio Secreto

Chame `ecall_polinomio_secreto(x)`, que retorna:

```
(ax² + bx + c) % p
```

- `a`, `b`, `c` são secretos.
- `p = 2147483647` (maior primo de 32 bits).
- O valor `x = 0` é inválido.
- A tarefa é descobrir os coeficientes `a`, `b`, e `c` a partir de chamadas com diferentes valores de `x`.

### ✊🖐✌️ Desafio 5 – Pedra, Papel e Tesoura

Use os arquivos:

- [`enclave-desafio-5.edl`](./enclave-desafio-5.edl)
- [`enclave-desafio-5.signed.so`](./enclave-desafio-5.signed.so)

Substitua os arquivos do enclave pelos acima.

- Novas funções:
  - `ecall_pedra_papel_tesoura`
  - `ocall_pedra_papel_tesoura`

Sua tarefa:

- Implemente `ocall_pedra_papel_tesoura` no `app/app.c`
- Essa função será chamada 20 vezes pelo enclave e deve retornar:
  - `0`: Pedra
  - `1`: Papel
  - `2`: Tesoura
- Você **deve ganhar todas as 20 partidas**.
- Ao final, o enclave imprimirá o resultado:

```
[ENCLAVE] DESAFIO 5 CONCLUIDO!!
          ENCLAVE JOGADAS: 11212201212200121120
             SUAS JOGADAS: 22020012020011202201
```

## ✅ Entrega

A entrega consiste no código modificado no repositório e os logs/resultados impressos no terminal para os desafios.

## 📁 Estrutura recomendada

```
.
├── enclave-atividade.signed.so
├── enclave-atividade.edl
├── enclave-desafio-5.signed.so
├── enclave-desafio-5.edl
├── intel-sgx-template/ (clonado do projeto base)
│   ├── app/
│   │   └── app.c
│   │   └── app.h
│   └── enclave/
│       └── enclave.edl
└── README.md
```

Desenvolvido para fins acadêmicos no contexto de segurança com Intel SGX.
