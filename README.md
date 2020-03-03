# EnqueteApi
Get /poll/:id
É necessário criar uma rota sendo:
https://localhost:44306/Enquete/poll/1
Será retornado um objeto do tipo Enquete.
O objeto é construído da seguinte forma.
public class Enquete
    {
        public long Id { get; set; }
        public string Questao { get; set; }
        public List<Opcoes> Opcoes { get; set; }
        public long? QtdVisualizacao { get; set; }
    }

public class Opcoes
    {
        public long Id { get; set; }
        public string Descricao { get; set; }
        public long? QtdVoto { get; set; }
    }

Post /poll
Deve-se passar um objeto do tipo Enquete, na seguinte rota.
https://localhost:44306/Enquete/poll
E será retornado um id do tipo long.

Get /poll/:id/vote
A rota para realizar o voto é
https://localhost:44306/Enquete/poll/1/vote

Get /poll/:id/vote
Para as estatísticas, a rota necessária é
https://localhost:44306/Enquete/poll/1/stats
Será retornado um objeto do tipo Enquete contendo as visualizações e a somatória dos votos.


BANCO DE DADOS
O banco foi desenvolvido em sql server, e o mesmo é construído da seguinte forma:
Nome do Banco: EnqueteDB
Usuário: hygor
Senha: 123
CREATE TABLE Enquete
(
Id BIGINT NOT NULL IDENTITY(1,1) PRIMARY KEY,
Questao VARCHAR(MAX) NOT NULL,
QtdVisualizacao BIGINT NOT NULL,
);

CREATE TABLE Opcoes
(
Id BIGINT NOT NULL IDENTITY(1,1) PRIMARY KEY,
Descricao VARCHAR(MAX) NOT NULL,
QtdVoto BIGINT NOT NULL,
IdEnquete BIGINT NOT NULL
);


A API e o banco, estão rodando no mesmo servidor (localhost).
Caso o banco seja instalado em um servidor separado da API, será necessário trocar a ConnetionString, colocando o endereço do servidor, junto com suas credenciais.

Com o SQL Server já instalado, é necessário habilitar o protocolo TCP/IP no Sql Server Configuration Manager, e reiniciar o serviço.
  

Liberar a porta 1433 no firewall, para poder realizar a conexão com uma máquina diferente.
