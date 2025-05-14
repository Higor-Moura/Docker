
# VOLUMES

> - Um **volume** no Kubernetes é um diretório acessado pelos containers para armazenar dados.
> - Existem volumes **efêmeros** e **persistentes**:

## Volumes Efêmeros

> - São temporários e duram apenas enquanto o pod está em execução.
> - Se o pod for deletado, reiniciado ou movido para outro nó, o conteúdo do volume é perdido.

## Volumes Persistentes

> - Garantem que os dados continuem disponíveis mesmo após reinicializações ou exclusões do pod.
> - São essenciais para aplicações que não podem perder dados.

---

### Exemplo com volume `emptyDir` (efêmero)

```yaml
apiVersion: v1
kind: Pod
metadata:
  name: redis-pod
spec:
  containers:
  - name: redis-container
    image: redis
    volumeMounts:
    - name: "cache-storage"
      mountPath: "/my-volume"

  volumes:
  - name: cache-storage
    emptyDir: {} 
```

> Neste exemplo:
> - Usamos o tipo de volume `emptyDir`, que é efêmero.
> - O conteúdo do volume **permanece** se o container reiniciar.
> - **Mas será perdido** se o pod for destruído ou agendado em outro nó.
