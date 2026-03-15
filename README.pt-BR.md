# SiteRedirect

![PHP](https://img.shields.io/badge/PHP-7%2B-777BB4?logo=php&logoColor=white)
![Licença](https://img.shields.io/badge/Licen%C3%A7a-Unlicense-green)

Leia em inglês: [README.md](README.md)

> **Nova versão:** Redirecionamento com contagem de acessos no Google Firebase → [**SiteRedirect2**](https://github.com/dmslabsbr/SiteRedirect2)

---

O **SiteRedirect** é um serviço mínimo de redirecionamento de URLs para seu servidor web. Você define aliases curtos (ex.: `amazon`, `uber`) em um arquivo de configuração; o visitante acessa `seusite.com/alias` e é enviado à URL de destino. Sem banco de dados—apenas PHP e regras de rewrite do Apache.

## Descrição

- Um único arquivo de configuração guarda todos os mapeamentos alias → URL.
- O Apache (ou compatível) reescreve caminhos limpos como `/amazon` para `redir.php?go=amazon`.
- Modo de debug opcional lista todos os aliases (protegido por um código especial).
- Fallback: requisições sem alias válido podem exibir um `index.html` personalizado.

## Instalação

1. Clone ou copie este repositório para a **raiz do documento** do seu servidor web (Apache com `mod_rewrite` habilitado).
2. Renomeie `htaccess` para `.htaccess`.
3. Edite `vai.php` e adicione ou altere as entradas alias → URL.

## Arquivos

| Arquivo | Função |
|---------|--------|
| `vai.php` | Mapa alias → URL; edite este arquivo para adicionar ou alterar redirecionamentos. |
| `redir.php` | Script principal: carrega `vai.php` e envia o header `Location` para o alias correspondente. |
| `htaccess` | Renomeie para `.htaccess` para o servidor encaminhar as requisições ao `redir.php`. |
| `index.html` | Exibido quando o usuário acessa a raiz ou um caminho desconhecido (personalize conforme necessário). |

## Uso

- **Redirecionar:** `https://seudominio.com/amazon` → redireciona para a URL definida para `amazon` em `vai.php`.
- **Lista de debug:** `https://seudominio.com/amazon?go=specialCode` (ou o caminho que você usa para o código especial em `redir.php`) lista todos os aliases e URLs.

## Configuração

- **Aliases:** Edite o array `$vai` em `vai.php`. As chaves são os aliases (convertidos para minúsculas no script), os valores são as URLs de destino completas.
- **Regras de rewrite:** No `.htaccess` (a partir de `htaccess`), a primeira regra envia `/{alias}` para `redir.php?go={alias}`. Ajuste as regras se seu servidor ou estrutura de caminhos for diferente.

## Licença

Este projeto não inclui arquivo de licença; use e modifique por sua conta e risco. O badge acima está como "Unlicense" como placeholder até que uma licença seja definida.
