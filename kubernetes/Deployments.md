# DEPLOYMENTS

> - Faz a implantação da aplicação
> - `Rolling Updates (Rolling Release)` = executa uma atualização baseada em percentual de indisponibilidade de PODs por padrão é ter no maximo 25% de indisponibilidade do total de pods que voce tem rodando
> - EX: caso eu tiver quatro PODs associados a um Deployments a atualização sera feita de um por um. Ou seja no minimo eu terei 75% dos meus pods em status runing
> - `Recreate Deployment` = Mas pode causar indisponibilidade (Tem um risco associado). Ele vai parar todas as PODs e então vai subir todas as PODs com a versão nova da sua aplicação
> - `Rollback` = Se ouver algum problema em qualquer uma das estrategias voce pode fazer um Rollback e voltar ao estado que estava anteriormente
