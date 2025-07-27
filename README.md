# Desafio Projeto Hospedagem 🏨💻

Este projeto faz parte de um desafio de lógica de programação para simular um sistema de gerenciamento de reservas de hospedagem. Ele permite cadastrar hóspedes, suítes e realizar reservas, calculando o valor total com base nas informações fornecidas.

---

## Funcionalidades ✨

- **Cadastro de Hóspedes:** Adiciona pessoas à reserva. 🧑‍🤝‍🧑
- **Cadastro de Suítes:** Define os detalhes da suíte, como tipo, valor da diária e capacidade. 🛏️
- **Cálculo de Valor:** Calcula o total da reserva, considerando o número de dias reservados e um desconto de 10% para reservas de 10 dias ou mais. 💰
- **Verificação de Capacidade:** Garante que o número de hóspedes não ultrapasse a capacidade da suíte. 🚶‍♂️🚶‍♀️

---

## Classes Principais 🏷️

### Pessoa
Representa um hóspede com as seguintes propriedades:
- `Nome` (string) 🙂  
- `Sobrenome` (string) 👤  
- `NomeCompleto` (propriedade somente leitura que combina nome e sobrenome) 📛  

### Suite
Representa uma suíte com detalhes como:
- `TipoSuite` (string) 🏷️  
- `Capacidade` (int) 🚻  
- `ValorDiaria` (decimal) 💵  

### Reserva
Gerencia as reservas e possui:
- `Hospedes` (Lista de `Pessoa`) 🧑‍🤝‍🧑  
- `Suite` (`Suite`) 🛏️  
- `DiasReservados` (int) 📅  

### Métodos da classe `Reserva`
- `CadastrarHospedes(List<Pessoa> hospedes)`: Adiciona hóspedes à reserva, verificando se a capacidade é suficiente. Lança exceção se exceder. ⚠️  
- `CadastrarSuite(Suite suite)`: Associa uma suíte à reserva. 🏨  
- `ObterQuantidadeHospedes()`: Retorna o número de hóspedes. 🔢  
- `CalcularValorDiaria()`: Calcula o valor total, aplicando desconto de 10% para reservas de 10 dias ou mais. 💸  

---

## Como Usar 🚀

Para utilizar este sistema, crie instâncias de `Pessoa`, `Suite` e `Reserva`, e utilize seus métodos para gerenciar as reservas.

### Exemplo Básico 💡

```csharp
using DesafioProjetoHospedagem.Models;
using System;
using System.Collections.Generic;

public class Program
{
    public static void Main()
    {
        // Criação de hóspedes
        var hospedes = new List<Pessoa>
        {
            new Pessoa(nome: "João", sobrenome: "Silva"),
            new Pessoa(nome: "Maria", sobrenome: "Souza")
        };

        // Criação da suíte
        var suite = new Suite(tipoSuite: "Premium", capacidade: 2, valorDiaria: 100);

        // Nova reserva
        var reserva = new Reserva(diasReservados: 5);
        reserva.CadastrarSuite(suite);

        try
        {
            reserva.CadastrarHospedes(hospedes);
        }
        catch (Exception ex)
        {
            Console.WriteLine($"Erro ao cadastrar hóspedes: {ex.Message}");
        }

        Console.WriteLine($"Quantidade de hóspedes: {reserva.ObterQuantidadeHospedes()}");
        Console.WriteLine($"Valor total: {reserva.CalcularValorDiaria():C}");

        // Reserva com desconto (10 dias ou mais)
        var reservaComDesconto = new Reserva(diasReservados: 10);
        reservaComDesconto.CadastrarSuite(suite);
        try
        {
            reservaComDesconto.CadastrarHospedes(hospedes);
        }
        catch (Exception ex)
        {
            Console.WriteLine($"Erro ao cadastrar hóspedes: {ex.Message}");
        }

        Console.WriteLine($"\nReserva de 10 dias:");
        Console.WriteLine($"Hóspedes: {reservaComDesconto.ObterQuantidadeHospedes()}");
        Console.WriteLine($"Valor com desconto: {reservaComDesconto.CalcularValorDiaria():C}");
    }
}
