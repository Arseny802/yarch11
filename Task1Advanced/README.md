# Terraform VM Module

Модуль для развёртывания ВМ в Yandex Cloud: `dev`, `stage`, `prod`.


## ⚙️ Переменные модуля (`modules/vm/variables.tf`)
| Переменная       | Тип         | Описание                          |
| ---------------- | ----------- | --------------------------------- |
| `vm_name`        | string      | Имя ВМ                            |
| `cores`          | number      | Ядра CPU                          |
| `memory`         | number      | RAM (ГБ)                          |
| `disk_size`      | number      | Размер диска                      |
| `disk_type`      | string      | Тип: `network-ssd`, `network-hdd` |
| `zone`           | string      | Зона, например `ru-central1-a`    |
| `image_family`   | string      | ОС: `ubuntu-2004-lts`             |
| `subnet_id`      | string      | ID подсети                        |
| `ssh_public_key` | string      | SSH-ключ (`ssh-rsa ...`)          |
| `environment`    | string      | `dev`/`stage`/`prod`              |
| `labels`         | map(string) | Метки, например `{"env": "dev"}`  |

---

## 📤 Выходы
| Выход           | Описание      |
| --------------- | ------------- |
| `instance_id`   | ID ВМ         |
| `instance_name` | Имя ВМ        |
| `internal_ip`   | Внутренний IP |
| `external_ip`   | Публичный IP  |
| `disk_id`       | ID диска      |

---

## 🌍 Как использовать (пример для `dev`)
```bash
cd envs/dev
Задайте переменные в terraform.tfvars:
hcl
vm_name        = "dev-vm"
cores          = 2
memory         = 4
disk_size      = 20
subnet_id      = "e9bn5d6hjcvd3rda1234"
ssh_public_key = "ssh-rsa AAA..."
environment    = "dev"
labels         = { env = "dev" }
```

Запуск:
```bash
terraform init
terraform plan -var-file=terraform.tfvars
terraform apply -var-file=terraform.tfvars
```
