# Добавить **Namespace labels** 

Теперь давайте внесем изменения в нашу развернутую инфраструктуру. В **Acme Inc**. мы хотим отслеживать владельцев и основные контакты для всех наших **namespaces**. 
Мы можем сделать это, используя метки **labels** в нашем **namespace**.

Давайте посмотрим на **labels** в настоящее время в нашем namespace:

 `kubectl get namespace test --show-labels`{{execute}}

Откройте `namespaces.tf` в редакторе и обновите ресурс:

 `nano namespaces.tf`{{execute}}

<pre class="file" data-filename="namespaces.tf" data-target="replace">resource "kubernetes_namespace" "test" {
  metadata {
    name = "test"

    labels = {
      "service.example.com/owner" = "infrastructure-team"
      "service.example.com/technical-contact" = "infrastructure.support"
      "service.example.com/business-contact" = "infrastructure.admin"
    }
  }
}
</pre>

Теперь давайте **"plan"** изменения.

`terraform plan -out plan`{{execute}}

```
Plan: 0 to add, 1 to change, 0 to destroy.
```

Мы видим, что **Terraform** хочет обновить наш ресурс и добавить **labels**. Давайте сделаем это:

`terraform apply plan`{{execute}}

```
Apply complete! Resources: 0 added, 1 changed, 0 destroyed.
```

И еще раз проверьте ваши тестовые метки **namespaces's labels** :

`kubectl get namespace test --show-labels`{{execute}}

> Если вы хотите проверить, обновлена ли ваша инфраструктура, вы можете запустить `terraform plan -out plan`{{execute}} в любое время.
> Если изменений нет, вы увидите **"No changes. Infrastructure is up-to-date."** in the output.


