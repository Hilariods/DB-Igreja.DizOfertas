# Projeto: Igreja-ColetaDizimosOfertas

## Descrição do Projeto

Desenvolvimento de um sistema para gerenciamento da coleta de dízimos e ofertas em uma igreja com 50 mil membros. O sistema será responsável por registrar as doações feitas nos cultos realizados às terças, quartas, quintas, sábados e domingos, ao longo de um período de 5 anos. A cada 6 meses, será gerado um relatório para verificar o montante acumulado. Quando o montante acumulado exceder 200 mil, o valor será retirado do banco imediatamente para investimento em projetos sociais e infraestrutura da igreja.

## Tecnologias Utilizadas

- **Banco de Dados**: MySQL
- **Backend**: Não especificado
- **Infraestrutura**: Docker
- **Controle de Versão**: Git

## Script SQL para Criação de Tabelas

```sql
-- Criar tabela Membros
CREATE TABLE Membros (
    id INT AUTO_INCREMENT PRIMARY KEY,
    nome VARCHAR(255) NOT NULL,
    data_nascimento DATE NOT NULL,
    cpf VARCHAR(11) NOT NULL UNIQUE,
    endereco VARCHAR(255),
    telefone VARCHAR(20),
    email VARCHAR(100),
    data_batismo DATE,
    situacao VARCHAR(50) DEFAULT 'Ativo'
);

-- Criar tabela Cultos
CREATE TABLE Cultos (
    id INT AUTO_INCREMENT PRIMARY KEY,
    data_culto DATE NOT NULL,
    tipo_culto VARCHAR(50) NOT NULL,
    UNIQUE KEY (data_culto, tipo_culto)
);

-- Criar tabela DizimosOfertas
CREATE TABLE DizimosOfertas (
    id INT AUTO_INCREMENT PRIMARY KEY,
    id_membro INT NOT NULL,
    id_culto INT NOT NULL,
    tipo_doacao ENUM('Dízimo', 'Oferta') NOT NULL,
    valor DECIMAL(10, 2) NOT NULL,
    data_doacao DATETIME NOT NULL,
    FOREIGN KEY (id_membro) REFERENCES Membros(id),
    FOREIGN KEY (id_culto) REFERENCES Cultos(id)
);

-- Criar tabela RelatorioSemestral
CREATE TABLE RelatorioSemestral (
    id INT AUTO_INCREMENT PRIMARY KEY,
    semestre INT NOT NULL,
    ano INT NOT NULL,
    total_arrecadado DECIMAL(15, 2) DEFAULT 0.00,
    data_geracao TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);

-- Criar tabela Investimentos
CREATE TABLE Investimentos (
    id INT AUTO_INCREMENT PRIMARY KEY,
    descricao VARCHAR(255) NOT NULL,
    valor DECIMAL(15, 2) NOT NULL,
    data_investimento DATE NOT NULL,
    id_projeto INT
);

-- Criar tabela Projetos
CREATE TABLE Projetos (
    id INT AUTO_INCREMENT PRIMARY KEY,
    nome VARCHAR(255) NOT NULL,
    descricao TEXT,
    data_inicio DATE,
    data_fim DATE,
    status ENUM('Planejamento', 'Em Andamento', 'Concluído') DEFAULT 'Planejamento'
);

```

Este Markdown descreve o projeto de coleta de dízimos e ofertas para uma igreja, incluindo a estrutura das tabelas necessárias no MySQL. Certifique-se de ajustar conforme necessário antes de subir para o GitHub ou utilizar em seu ambiente Dockerizado.

---
