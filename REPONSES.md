B.1 - Identification du fichier XSD et son rôle

Fichier XSD : `src/main/resources/bank.xsd`

Rôle du XSD :
Le fichier XSD définit le contrat de données du service SOAP. Il spécifie la structure exacte des messages XML échangés entre le client et le serveur.

B.2 - Liste des éléments de requête/réponse

GetAccountRequest
    - accountId : `string` Identifiant du compte à consulter

GetAccountResponse
- account : `AccountType` Objet compte contenant :
  - accountId : `string` Identifiant du compte
  - owner : `string` Propriétaire du compte
  - balance : `decimal` Solde actuel
  - currency : `string` Devise

DepositRequest
- accountId : `string` Identifiant du compte
- amount : `decimal` Montant à déposer

DepositResponse
- newBalance : `decimal` Nouveau solde après dépôt

AccountType
Structure réutilisable représentant un compte bancaire avec ses 4 attributs (accountId, owner, balance, currency).


B.3 - Analyse du WSDL

Namespace cible

http://example.com/bank

Ce namespace identifie de manière unique le service SOAP et ses types de données.

PortType et Opérations

PortType : `BankPort`

Opérations disponibles :
1. GetAccount
   - Input : `GetAccountRequest`
   - Output : `GetAccountResponse`
   - Permet de consulter les informations d'un compte

2. Deposit
   - Input : `DepositRequest`
   - Output : `DepositResponse`
   - Permet de déposer un montant sur un compte

Endpoint (URL du service):

http://localhost:8081/ws

Binding SOAP
- Type : SOAP 1.1 over HTTP
- Style : Document/Literal
- Transport : HTTP
- Binding Name : `BankPortSoap11`

Partie C : Tests Postman

Voir captures d'écran :
- C1_GetAccount_Success.png
- C2_Deposit_Success.png
- C3_Error_NegativeAmount.png
- C4_Error_UnknownAccount.png

Partie D : Fonctionnalité ajoutée

D.1 Fonctionnalité choisie

J'ai ajouté l'opération Withdraw qui permet de retirer un montant d'un compte bancaire.

D.2 Mise à jour du contrat (XSD)

Fichier modifié : src/main/resources/bank.xsd

Ajout de deux nouveaux éléments :

WithdrawRequest :
- accountId : string (identifiant du compte)
- amount : decimal (montant à retirer)

WithdrawResponse :
- newBalance : decimal (nouveau solde après retrait)

D.3 Implémentation côté serveur

Fichiers modifiés :

1. BankEndpoint.java
2. BankService.java
3. InsufficientFundsException.java

D.4 Tests Postman

Voir captures d'écran :
- D1_Withdraw_Success.png
- D2_Error_InsufficientFunds.png
- D3_Error_NegativeAmount.png
- D4_Error_UnknownAccount.png
