### Scripts utilizados para criar um gerenciador de espaçonaves do star wars com SQL Server + .NET

Projeto elaborado pela [Digital Innovation One](https://digitalinnovation.one/sign-up?ref=BALFLCV08F)

Ministrado pelo professor **Thiago Campos** 

**Links úteis:**

- Curso para interessados: https://web.dio.me/course/modelando-um-banco-de-dados-na-pratica-com-sql-server/learning/abaae9eb-50d6-4ece-9af4-973354cd1a1a?back=/track/everis-new-talents-3-net
- API pública de Star Wars: https://swapi.dev/
- Link para clonar a aplicação feita pelo professor: https://github.com/ThiagoAcam/ControleAcessoEstrelaDaMorte.git


## **Criando tabela Planetas**
```
CREATE TABLE Planetas(
	IdPlaneta int NOT NULL,
	Nome varchar(50) NOT NULL,
	Rotacao float NOT NULL,
	Orbita float NOT NULL,
	Diametro float NOT NULL,
	Clima varchar(50) NOT NULL,
	Populacao int NOT NULL,
)
GO
ALTER TABLE Planetas ADD CONSTRAINT PK_Planetas PRIMARY KEY (IdPlaneta);
```


## **Criando tabela Naves**
```
CREATE TABLE Naves(
	IdNave int NOT NULL,
	Nome varchar(100) NOT NULL,
	Modelo varchar(150) NOT NULL,
	Passageiros int NOT NULL,
	Carga float NOT NULL,
	Classe varchar(100) NOT NULL,
)
GO
ALTER TABLE Naves ADD CONSTRAINT PK_Naves PRIMARY KEY (IdNave);

```

## **Criando tabela Pilotos**
```
CREATE TABLE Pilotos(
	IdPiloto int NOT NULL,
	Nome varchar(200) NOT NULL,
	AnoNascimento varchar(10) NOT NULL,
	IdPlaneta int NOT NULL,
)
Go
ALTER TABLE Pilotos ADD CONSTRAINT Pk_Pilotos PRIMARY KEY (IdPiloto);
GO
ALTER TABLE Pilotos ADD CONSTRAINT FK_Pilotos_Planetas FOREIGN KEY (IdPlaneta)
REFERENCES Planetas (IdPlaneta) 
```


## **Criando tabela PilotosNaves**
```
CREATE TABLE PilotosNaves(
	IdPiloto int NOT NULL,
	IdNave int NOT NULL,
	FlagAutorizado bit NOT NULL,
)
GO
ALTER TABLE PilotosNaves ADD CONSTRAINT PK_PilotosNaves PRIMARY KEY (IdPiloto, IdNave);

GO
ALTER TABLE PilotosNaves ADD CONSTRAINT FK_PilotosNaves_Pilotos FOREIGN KEY (IdPiloto)
REFERENCES Pilotos (IdPiloto);

GO
ALTER TABLE PilotosNaves ADD CONSTRAINT FK_PilotosNaves_Naves FOREIGN KEY (IdNave) 
REFERENCES Naves (IdNave);

GO
ALTER TABLE PilotosNaves ADD CONSTRAINT DF_PilotosNaves_FlagAutorizado DEFAULT (1) FOR FlagAutorizado;
```


## **Criando tabela HistoricoViagens**
```
CREATE TABLE HistoricoViagens(
	IdNave int NOT NULL,
	IdPiloto int NOT NULL,
	DtSaida datetime NOT NULL,
	DtChegada datetime NULL
)
GO
ALTER TABLE HistoricoViagens ADD CONSTRAINT FK_HistoricoViagens_PilotosNaves FOREIGN KEY (IdPiloto, IdNave) 
REFERENCES PilotosNaves (IdPiloto, IdNave)
GO
ALTER TABLE HistoricoViagens CHECK CONSTRAINT FK_HistoricoViagens_PilotosNaves
```
<div align="center">
<img src="https://user-images.githubusercontent.com/62768931/142573107-a1c88279-97a7-485c-bf68-f09b5d39509d.PNG" width="650px" />
</div>
