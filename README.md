# TP - pipeline GITHUB
## ROUGEON Corentin

### 1.  lié votre compte via clé SSH à votre ordinateur


via gitbash on crée notre clé ssh :
`ssh-keygen -t ed25519 -C "corentin.rougeon@ynov.com"`

on Copie le contenue notre clé publique et on la colle dans 
`Setting > SSH and GPG KEYS > New SSH Key` via le site github 

pour tester notre clé :
`ssh -T git@github.com`

resultat :

`Hi Corentin-Rougeon! You've successfully authenticated, but GitHub does not provide shell access.`
