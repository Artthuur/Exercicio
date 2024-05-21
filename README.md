# Exercicio

import java.util.ArrayList;
import java.util.Scanner;

class Empregado {
    private String nome;
    private int idade;
    private double salario;

    public String getNome() {
        return nome;
    }

    public void setNome(String nome) {
        this.nome = nome;
    }

    public int getIdade() {
        return idade;
    }

    public void setIdade(int idade) {
        this.idade = idade;
    }

    public double getSalario() {
        return salario;
    }

    public void setSalario(double salario) {
        this.salario = salario;
    }

    @Override
    public String toString() {
        return "Empregado [nome=" + nome + ", idade=" + idade + ", salario=" + salario + "]";
    }

    public void promover() {
        if (idade > 18) {
            aumentarSalario(25);
            System.out.println("O empregado " + nome + " foi promovido!");
        } else {
            System.out.println("O empregado não tem idade necessária");
        }
    }

    public void aumentarSalario(double percent) {
        salario = (percent * salario / 100) + salario;
    }

    public void demitir(int motivo) {
        switch (motivo) {
            case 2:
                double multa = 40 * salario / 100;
                System.out.println("O empregado deverá receber " + multa + " de multa");
                break;
            case 3:
                if (salario >= 1000 && salario <= 2000) {
                    salario = 1500;
                } else if (salario >= 2001 && salario <= 3000) {
                    salario = 2500;
                } else if (salario >= 3001 && salario <= 4000) {
                    salario = 3500;
                } else {
                    salario = 4000;
                }
                System.out.println("O salário de aposentadoria é: " + salario);
                break;
            default:
                System.out.println("O empregado deverá cumprir aviso prévio");
                break;
        }
    }

    public void fazerAniversario() {
        idade++;
    }
}

public class Principal {

    public static void main(String[] args) {
        Scanner leitor = new Scanner(System.in);
        ArrayList<Empregado> empregados = new ArrayList<>();

        int opcao = 0;

        while (opcao != 7) {
            System.out.println("Selecione uma opção: ");
            System.out.println("1 - Criar novo empregado");
            System.out.println("2 - Promover empregado");
            System.out.println("3 - Aumentar salário do empregado");
            System.out.println("4 - Demitir empregado");
            System.out.println("5 - Fazer aniversário do empregado");
            System.out.println("6 - Mostrar detalhes dos empregados");
            System.out.println("7 - Sair");
            opcao = leitor.nextInt();
            
            switch (opcao) {
                case 1:
                    Empregado emp = new Empregado();
                    System.out.println("Digite o nome do empregado: ");
                    String nome = leitor.next();
                    emp.setNome(nome);
                    System.out.println("Digite a idade do empregado: ");
                    int idade = leitor.nextInt();
                    emp.setIdade(idade);
                    System.out.println("Digite o salário do empregado: ");
                    double salario = leitor.nextDouble();
                    emp.setSalario(salario);
                    empregados.add(emp);
                    System.out.println("Empregado " + emp.getNome() + " criado!");
                    break;

                case 2:
                    if (empregados.isEmpty()) {
                        System.out.println("Nenhum empregado cadastrado.");
                        break;
                    }
                    System.out.println("Digite o número do empregado para promover: ");
                    for (int i = 0; i < empregados.size(); i++) {
                        System.out.println(i + " - " + empregados.get(i).getNome());
                    }
                    int indicePromover = leitor.nextInt();
                    if (indicePromover >= 0 && indicePromover < empregados.size()) {
                        Empregado empPromover = empregados.get(indicePromover);
                        empPromover.promover();
                    } else {
                        System.out.println("Empregado inválido.");
                    }
                    break;

                case 3:
                    if (empregados.isEmpty()) {
                        System.out.println("Nenhum empregado cadastrado.");
                        break;
                    }
                    System.out.println("Digite o número do empregado para aumentar o salário: ");
                    for (int i = 0; i < empregados.size(); i++) {
                        System.out.println(i + " - " + empregados.get(i).getNome());
                    }
                    int indiceAumentarSalario = leitor.nextInt();
                    if (indiceAumentarSalario >= 0 && indiceAumentarSalario < empregados.size()) {
                        Empregado empAumentarSalario = empregados.get(indiceAumentarSalario);
                        System.out.println("Digite o percentual de aumento: ");
                        double percentual = leitor.nextDouble();
                        empAumentarSalario.aumentarSalario(percentual);
                        System.out.println("Novo salário do " + empAumentarSalario.getNome() + ": " + empAumentarSalario.getSalario());
                    } else {
                        System.out.println("Empregado inválido.");
                    }
                    break;

                case 4:
                    if (empregados.isEmpty()) {
                        System.out.println("Nenhum empregado cadastrado.");
                        break;
                    }
                    System.out.println("Digite o número do empregado para demitir: ");
                    for (int i = 0; i < empregados.size(); i++) {
                        System.out.println(i + " - " + empregados.get(i).getNome());
                    }
                    int indiceDemitir = leitor.nextInt();
                    if (indiceDemitir >= 0 && indiceDemitir < empregados.size()) {
                        Empregado empDemitir = empregados.get(indiceDemitir);
                        System.out.println("Digite o motivo da demissão (1 - justa causa, 2 - decisão empregador, 3 - aposentadoria): ");
                        int motivo = leitor.nextInt();
                        empDemitir.demitir(motivo);
                        empregados.remove(indiceDemitir);
                        System.out.println("Empregado " + empDemitir.getNome() + " demitido.");
                    } else {
                        System.out.println("Empregado inválido.");
                    }
                    break;

                case 5:
                    if (empregados.isEmpty()) {
                        System.out.println("Nenhum empregado cadastrado.");
                        break;
                    }
                    System.out.println("Digite o número do empregado para fazer aniversário: ");
                    for (int i = 0; i < empregados.size(); i++) {
                        System.out.println(i + " - " + empregados.get(i).getNome());
                    }
                    int indiceAniversario = leitor.nextInt();
                    if (indiceAniversario >= 0 && indiceAniversario < empregados.size()) {
                        Empregado empAniversario = empregados.get(indiceAniversario);
                        empAniversario.fazerAniversario();
                        System.out.println("Empregado " + empAniversario.getNome() + " fez aniversário e agora tem " + empAniversario.getIdade() + " anos.");
                    } else {
                        System.out.println("Empregado inválido.");
                    }
                    break;

                case 6:
                    if (empregados.isEmpty()) {
                        System.out.println("Nenhum empregado cadastrado.");
                        break;
                    }
                    for (Empregado empregado : empregados) {
                        System.out.println(empregado);
                    }
                    break;

                case 7:
                    System.out.println("Saindo...");
                    break;

                default:
                    System.out.println("Opção inválida.");
                    break;
            }
        }
        leitor.close();
    }
}
