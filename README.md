# Meu-codigo-em-java
code (eu+java)

import java.util.Scanner;

// ==========================================
// 1. O MOLDE DA CONTA (CLASSE)
// ==========================================
class ContaBancaria {
    // Variáveis privadas - NINGUÉM mexe direto de fora da classe!
    private String titular;
    private double saldo;

    // Construtor: Exige o nome do titular para criar a conta, começando com saldo 0
    public ContaBancaria(String titular) {
        this.titular = titular; // 'this.titular' é a variável lá de cima, 'titular' é o parâmetro
        this.saldo = 0.0;
    }

    // GETTER para ler o Titular (Apenas leitura, não tem "setTitular" pois não muda)
    public String getTitular() {
        return this.titular;
    }

    // GETTER para ler o Saldo (Apenas leitura direto, para alterar precisa depositar/sacar)
    public double getSaldo() {
        return this.saldo;
    }

    // SETTER / MÉTODO DE DEPÓSITO (Com validação do "porteiro")
    public void depositar(double valor) {
        if (valor > 0) {
            this.saldo += valor; // soma o valor ao saldo atual do objeto
            System.out.println("✅ Depósito de R$ " + valor + " realizado com sucesso!");
        } else {
            System.out.println("❌ Erro: O valor do depósito precisa ser maior que zero!");
        }
    }

    // SETTER / MÉTODO DE SAQUE (Com validação de saldo suficiente)
    public void sacar(double valor) {
        if (valor <= 0) {
            System.out.println("❌ Erro: Valor de saque inválido!");
        } else if (valor > this.saldo) {
            System.out.println("❌ Erro: Saldo insuficiente! Você tem apenas R$ " + this.saldo);
        } else {
            this.saldo -= valor; // subtrai o valor do saldo do objeto
            System.out.println("✅ Saque de R$ " + valor + " realizado com sucesso!");
        }
    }
}

// ==========================================
// 2. O SISTEMA DO BANCO (MAIN)
// ==========================================
public class Principal {
    public static void main(String[] args) {
        Scanner teclado = new Scanner(System.in);

        System.out.println("🏦 Bem-vindo ao banco Java! Digite o seu nome para abrir a conta:");
        String nome = teclado.nextLine();

        // Criando o objeto usando o CONSTRUTOR!
        ContaBancaria minhaConta = new ContaBancaria(nome);

        System.out.println("\n✨ Conta criada para " + minhaConta.getTitular() + "!");

        boolean rodando = true;
        while (rodando) {
            System.out.println("\n--- MENU ---");
            System.out.println("1. Consultar Saldo (Usa o GET)");
            System.out.println("2. Depositar (Usa o SET de depósito)");
            System.out.println("3. Sacar (Usa o SET de saque)");
            System.out.println("4. Sair");
            System.out.print("Escolha uma opção: ");
            int opcao = teclado.nextInt();

            switch (opcao) {
                case 1:
                    // Usando o GETTER para ler o saldo em segurança!
                    System.out.println("\n💰 Saldo atual de " + minhaConta.getTitular() + ": R$ " + minhaConta.getSaldo());
                    break;

                case 2:
                    System.out.print("\nDigite o valor para depósito: R$ ");
                    double valorDeposito = teclado.nextDouble();
                    // Enviando o valor para o método que valida e altera o saldo
                    minhaConta.depositar(valorDeposito);
                    break;

                case 3:
                    System.out.print("\nDigite o valor para saque: R$ ");
                    double valorSaque = teclado.nextDouble();
                    // Enviando o valor para o método que valida e subtrai do saldo
                    minhaConta.sacar(valorSaque);
                    break;

                case 4:
                    System.out.println("\n👋 Obrigado por usar o nosso banco! Até mais.");
                    rodando = false;
                    break;

                default:
                    System.out.println("⚠️ Opção inválida!");
            }
        }

        teclado.close();
    }
}




