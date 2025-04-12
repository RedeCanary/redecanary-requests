# Rede Canary - Requests
> Não recomendada para uso oficial no momento!

🧩 Este repositório serve para desenvolvedores ou curiosos requisitarem informações constantes do SKY BLOCK de maneira rápida,
os recursos das requisições são atualizados a cada modificação feita por nós.

🧶 **Destrinchando as requisições**
As requisições podem ser usadas para quaisquers finalidades:
  - Clientes de Minecraft
  - Criação de (plugins/mods/sites)
  - Criação de bibliotecas
  - E muito mais!

🪡 **Com a agulha na mão**
Abaixo há exemplos de como fazer usos de requisições em algumas
linguagens de programação comumente usadas:

🐍 **Python**
```python
import requests

def main():
    try:
        response = requests.get("https://raw.githubusercontent.com/RedeCanary/redecanary-requests/refs/heads/main/enchants.json")
        response.raise_for_status()
        data = response.json()
        
        for enchant in data:
            print("ID: {}\nNome: {}\nConflitos: {}".format(
                data[enchant]["id"], 
                data[enchant]["translated"], 
                data[enchant]["extra"]["conflicts"]
            ))

    except Exception as e:
        print(f"Ocorreu um erro: {e}")

if __name__ == "__main__":
    main()
```
