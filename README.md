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
  Requisitos:
    - Biblioteca requests
    - Python 3.0 ou superior
```python
import requests

def main():
    try:
        response = requests.get("https://raw.githubusercontent.com/RedeCanary/redecanary-requests/refs/heads/main/enchants.json")
        response.raise_for_status()
        data = response.json()
        
        for enchant in data:
            print("ID: {}\nNome: {}\nConflitos: {}".format(
                data[enchant]["CRITICAL"]["id"], 
                data[enchant]["CRITICAL"]["translated"], 
                data[enchant]["CRITICAL"]["extra"]["conflicts"]
            ))

    except Exception as e:
        print(f"Ocorreu um erro: {e}")

if __name__ == "__main__":
    main()
```

☕ **Java**
  Requisitos:
    - Biblioteca GSON (Google)
    - Framework Lombok
    - Java 8 ou superior
```java
    public static void main(String[] args) {
        try {
            final String URL_LINK = "https://raw.githubusercontent.com/RedeCanary/redecanary-requests/refs/heads/main/enchants.json";
            final URL url = new URL(URL_LINK);
            final HttpURLConnection connection = (HttpURLConnection) url.openConnection();
            connection.setRequestMethod("GET");

            final String content = getContent(URL_LINK);
            connection.disconnect();

            final Gson gson = new Gson();
            final EnchantmentsMap enchantmentMap = gson.fromJson(content, EnchantmentsMap.class);
            final EnchantmentsMap.Enchant enchant = enchantmentMap.getEnchantments().get("CRITICAL");

            System.out.println("Nome: " + enchant.getTranslatedName());
            System.out.println("Referência: " + enchant.getReference());
            System.out.println("Id: " + enchant.getId());

        } catch (IOException ignored) {}
    }

@Getter
@AllArgsConstructor
public class EnchantmentsMap {

        @SerializedName("enchantments")
        protected Map<String, Enchant> enchantments;

        @Getter
        @AllArgsConstructor
        public static class Enchant {
                @SerializedName("id")
                protected int id;

                @SerializedName("reference")
                protected String reference;

                @SerializedName("translated")
                protected String translatedName;
        }
}
```

⚙️ **Rust**
  Requisitos:
    - Biblioteca serde/serde_Json
    - Biblioteca reqwest/tokio
    - Rust nightly ou outro
```rust
#[derive(Debug, Serialize, Deserialize)]
struct EnchantmentMap {
    pub enchantments: HashMap<String, Enchantment>,
}

#[derive(Debug, Serialize, Deserialize)]
struct Enchantment {
    pub translated: String,
    pub reference: String,
    pub id: i32,
}

#[tokio::main]
async fn main() -> Result<(), Box<dyn std::error::Error>> {
    let resp = reqwest::get("https://raw.githubusercontent.com/RedeCanary/redecanary-requests/refs/heads/main/enchants.json")
        .await?
        .json::<EnchantmentMap>()
        .await?;

    if let Some(enchant) = resp.enchantments.get("CRITICAL") {
        println!("Nome: {}", enchant.translated);
        println!("Referência: {}", enchant.reference);
        println!("Id: {}", enchant.id);
    }

    Ok(())
}
```
