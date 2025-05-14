# LIVENESS PROBES

- No Kubernetes, são mecanismos que verificam se um contêiner está em um estado saudável e em execução.
- A verificação é feita através do agente **kubelet**.
- A **Liveness Probe** toma uma ação quando o teste não é bem-sucedido — essa ação geralmente se traduz em **reiniciar o contêiner**.

## Criando o arquivo YAML para Liveness Probes

Crie o arquivo chamado `livenessprobe.yml`:

```bash
sudo vi livenessprobe.yml
```

### Conteúdo do arquivo

```yaml
apiVersion: v1
kind: Pod
metadata:
  name: liveness-pod
spec:
  containers:
  - name: liveness-container-test
    image: busybox
    args:
      - /bin/sh
      - -c
      - touch /tmp/healthy; sleep 30; rm -f /tmp/healthy; sleep 600

    livenessProbe:
      exec:
        command:
        - cat
        - /tmp/healthy
      initialDelaySeconds: 5
      periodSeconds: 5
      failureThreshold: 3
```

## Explicação

- `args:` define os comandos executados no container:
  - Cria um arquivo `/tmp/healthy`
  - Aguarda 30 segundos
  - Remove o arquivo
  - Aguarda 600 segundos (simulando atividade longa)
- `livenessProbe:` realiza um `cat /tmp/healthy` para verificar se o arquivo existe
  - `initialDelaySeconds`: aguarda 5s antes do primeiro teste
  - `periodSeconds`: faz o teste a cada 5s
  - `failureThreshold`: se falhar 3 vezes consecutivas, o contêiner é reiniciado
