---

# Kit Inicial v4 - Eleventy Blog + Netlify CMS  

## Índice  

- [Visão Geral](#visao-geral)  
- [Recursos](#recursos)  
- [Estrutura de Arquivos](#estrutura-de-arquivos)  
- [Como Funciona](#como-funciona)  
- [Usando o Kit](#usando-o-kit)  
- [Convertendo um Site Estático](#convertendo-um-site-estatico)  
- [Blog](#blog)  
- [Coisas a fazer antes da implantação](#antes-da-implantacao)  

---

# Visão Geral  
<a name="#visao-geral" />  

### Introdução  
Este kit contém tudo o que você precisa para usar o Netlify CMS personalizado e criar um blog que pode ser editado pelos clientes por meio de uma interface amigável da Netlify. Já configuramos todos os scripts e definições necessárias para que funcione, então tudo o que você precisa fazer é adicioná-lo a um site na Netlify, ativar a Identidade, clicar no botão para ativar o Git Gateway (para que os blogs enviados pelos clientes sejam salvos no repositório) e pronto. Você também pode configurar o registro para ser apenas por convite e adicionar um botão "entrar com Google" nas opções.  

Aqui está um link para uma demonstração ao vivo deste kit na Netlify:  
[https://starterkit-v4-eleventy.netlify.app/](https://starterkit-v4-eleventy.netlify.app/)  

### Vídeo de Apresentação  
Aqui está uma introdução ao novo kit para ver o que há de novo:  
[https://youtu.be/JvEXfQGFKu4](https://youtu.be/JvEXfQGFKu4)  

---

# Recursos  
<a name="#recursos" />  

Este kit inicial tem o objetivo de colocar qualquer projeto no ar no menor tempo possível. Ele imita um site pré-pronto, permitindo que você faça modificações onde for necessário para ter um site totalmente funcional e otimizado em poucas horas. Ele já vem com um design responsivo por padrão e possui alguns recursos adicionais para melhorar a experiência de desenvolvimento.  

Alguns dos recursos incluem:  

- **Eleventy** – Permite usar linguagens de template dentro do projeto, possibilitando a reutilização de componentes e layouts para manter seu código mais organizado. O template usado neste kit é o **Nunjucks**, mas o Eleventy permite o uso de múltiplas linguagens ao mesmo tempo.  
- **Eleventy Images** – Plugin que otimiza automaticamente imagens para formatos de última geração, garantindo um desempenho melhor no Lighthouse.  
- **Eleventy Navigation** – Simplifica a criação de navegações, exigindo apenas três linhas no frontmatter do HTML.  
- **Dados Centralizados** – Todas as informações essenciais do cliente são armazenadas em um único local, facilitando futuras alterações.  
- **Netlify CMS** – O blog já vem configurado com Netlify CMS, então não é necessário configurar nada.  
- **Modo Escuro** – O kit inclui suporte a **dark mode**, detectando automaticamente a preferência do usuário no primeiro acesso.  

Se alguma dessas funcionalidades não fizer sentido para você, não se preocupe! Tudo será explicado na seção [Começando](#usando-o-kit). Mas antes, vamos entender a estrutura do projeto...  

---

# Estrutura de Arquivos  
<a name="#estrutura-de-arquivos" />  

Antes de começar a usar o kit, é útil entender como o projeto está estruturado para expandi-lo da maneira correta.  

### Raiz do Projeto  
Na raiz do projeto, você encontrará algumas pastas e arquivos, como `.eleventy.js`, `.gitignore` e `package.json`.  

O **arquivo mais importante** é `.eleventy.js`, que contém as configurações do Eleventy SSG. É aqui que definimos como as imagens serão otimizadas, onde os componentes, dados e layouts estão localizados e quais arquivos serão incluídos na versão final do site.  

O `.gitignore` mantém as pastas `node_modules` e `public` fora do repositório, pois são pastas volumosas e não precisam ser enviadas.  

### `public` vs `src` vs `node_modules`  
Das três pastas principais, você só precisa se preocupar com a `src`:  

- **`node_modules`** – Contém todas as dependências do projeto. **Não edite nada aqui.**  
- **`public`** – Armazena o código pronto para produção. **Não edite nada aqui.**  
- **`src`** – Aqui é onde você trabalha. Contém todas as pastas necessárias para modificar o site.  

---

# Como Funciona  
<a name="#como-funciona" />  

[Assista ao vídeo explicativo](https://youtu.be/UDU38awKQeg)  

O projeto utiliza um arquivo base (`base.html`) que contém as partes repetitivas do site, como `<head>`, navegação e rodapé. Em cada página específica, apenas o conteúdo necessário é inserido nos locais apropriados dentro desse arquivo base.  

---

# Usando o Kit  
<a name="#usando-o-kit" />  

### Começando  
<a name="#getting-started" />  

1. **Clone o repositório** e abra-o no seu editor de código. Recomendamos o Visual Studio Code.  
2. **Abra o terminal** no editor (Ctrl + ~ no Windows) e digite `npm install` para instalar as dependências.  
3. **Execute `npm start`** para iniciar o servidor local. No terminal, um link como `http://localhost:8080` será exibido. Segure `Ctrl` e clique nele para abrir o site no navegador. As alterações serão atualizadas automaticamente.  
4. Agora você pode começar a editar o kit conforme suas necessidades.  

**Nota:** Se fechar e reabrir o projeto, precisará rodar `npm start` novamente para iniciar o servidor.  

---

# Configurando Eleventy  
<a name="#setting-up-eleventy" />  

Abra o arquivo `.eleventy.js` e edite as configurações conforme suas necessidades.  

- **Imagens responsivas:**  
  No código:  
  ```js
  async function imageShortcode(src, alt, className, loading, sizes = '(max-width: 600px) 400px, 850px')
  ```
  A parte `sizes = '(max-width: 600px) 400px, 850px'` define os tamanhos padrão das imagens. Altere conforme necessário.  

- **Larguras das imagens geradas:**  
  ```js
  widths: [200, 400, 850, 1920, 2500]
  ```
  Modifique essa lista para controlar os tamanhos das imagens otimizadas.  

Leia mais na [documentação do Eleventy Images](https://www.11ty.dev/docs/plugins/image/).  

---

# Criando Páginas  
Todas as páginas devem ser adicionadas à pasta `/pages`.  

Se estiver migrando um site estático para este kit, cada página antiga precisa ser movida para esta pasta.  

Dentro da pasta `/pages`, há um arquivo `_new-page-template.txt` que contém um modelo de estrutura para novas páginas. Basta copiá-lo e usá-lo sempre que precisar criar uma nova página.  

**Exemplo de estrutura de frontmatter:**  

```yaml
---
layout: 'base.html'
description: "Descrição da página"
metaTitle: 'Título para redes sociais'
tagTitle: 'Título para SEO | Nome do Cliente'
preloadImg: '/images/imageName.format'
preloadCSS: '/css/fileName.css'
permalink: 'pagina/'
eleventyNavigation:
    key: Nome da Navegação
    order: 1000
---
```

Coloque o conteúdo HTML da página abaixo do frontmatter.  

---

# Convertendo um Site Estático  
<a name="#convertendo-um-site-estatico" />  

Se você já tem um site em HTML e CSS, pode migrá-lo facilmente para este sistema.  

1. Copie seus arquivos HTML para a pasta `/pages`.  
2. Adicione o frontmatter no topo de cada página.  
3. Mova o conteúdo dentro da tag `<main>` do seu site antigo para abaixo do frontmatter.  
4. Adapte os links das imagens e estilos.  

---







---

### Convertendo caminhos antigos de arquivos para os novos e removendo a extensão .html de todos os links  

Se você copiou e colou o HTML de um site antigo para uma nova página no kit, faça um **CTRL + F** e encontre todas as instâncias do caminho do arquivo de imagem, substituindo-as por **/assets/images/**.  

Por exemplo, ao migrar um site antigo para o kit, todas as minhas imagens tinham o caminho **/images/image.jpg**. No novo kit, todas as imagens ficam dentro da pasta **/assets/images**. Portanto, substituo **"/images** por **"/assets/images** (sim, as aspas fazem parte da busca). Isso garante que apenas os caminhos corretos sejam substituídos, já que eles sempre aparecem junto com **src="/images/image.jpg"**.  

Se eu apenas substituísse **/images** por **/assets/images**, poderia modificar caminhos indesejados, como **/assets/images/image.jpg**, transformando-o em **/assets/assets/images/image.jpg**, o que não é o que queremos.  

Você pode estar se perguntando: por que usamos **"/assets/images"** ao referenciar imagens? O README menciona que a pasta **/public** é onde o código é compilado e carregado pelo Netlify. O **/** inicial garante que o Netlify sempre busque os arquivos a partir da raiz do projeto. Sem esse **/**, o Netlify procuraria a imagem dentro da pasta onde a página está localizada, em vez da raiz do site.  

Depois disso, certifique-se de remover a extensão **.html** de todos os links no HTML, pois o Eleventy não a reconhece. Por exemplo, **/contact.html** deve ser alterado para **/contact**.  

Recomendo fazer um **CTRL + F** para **.html** e substituir manualmente, verificando se o arquivo **base.html** no cabeçalho da página ainda mantém sua extensão. Se ela for removida acidentalmente, coloque-a de volta!  

Se tiver dúvidas sobre os caminhos dos arquivos, confira a pasta **/public** e siga a estrutura do diretório (mas não altere nada nela, pois todas as mudanças serão perdidas na próxima compilação!). O Eleventy usa um sistema baseado em pastas: **/contact** aponta para a pasta **contact**, e o Netlify carrega o **index.html** dessa pasta quando acessamos **www.website.com/contact**. É por isso que não usamos **.html** nos links.  

---

### Mantendo os mesmos caminhos de arquivos  

Se houver caminhos que você não deseja alterar para manter o SEO, como **/pearland/pearland-piano-lessons**, basta definir o **permalink** para esse caminho no front matter da página:  

```yaml
---
layout: 'base.html'
description: "Descrição da página"
metaTitle: 'Título que aparece nas buscas do Google'
tagTitle: 'Sobre'
preloadImg: '/images/cabinets2-1920w.webp'
preloadCSS: '/css/about.css'
permalink: 'folder/page'
eleventyNavigation:
    key: Sobre Nós
    order: 200
---
```

Normalmente, o **permalink** usa o slug da página (**pearland-piano-lessons/**), mas se houver um caminho específico, basta incluí-lo no **permalink**. Não coloque **/** antes do slug, apenas um **/** depois, como no exemplo acima.  

---

## Blog  
<a name="#blog"></a>  
### Adicionando um novo post ou migrando um antigo para o novo kit  

Na pasta **/blog**, há um arquivo markdown chamado **blog-template.md**. Use-o para criar novos posts. Ele contém um **front matter** específico para blogs:  

```yaml
---
pageName: blog-template
blogTitle: Quanto custa a instalação de um painel solar?
titleTag: Quanto custa a instalação de um painel solar?
blogDescription: Saiba tudo sobre preços de painéis solares com uma empresa transparente.
author: Joe Mendez
date: 2022-12-16T19:40:18.253Z
tags:
  - post
  - featured
image: /images/blog/landing.jpg
imageAlt: Cozinha
---
```

Essas variáveis estão conectadas ao arquivo **config.yml** na pasta **/admin**, onde configuramos as entradas do CMS que o cliente usará para criar novos posts.  

```yaml
collections:
  - name: 'blog'
    label: 'Blog'
    folder: 'src/blog'
    create: true
    slug: '{{pageName}}'
    fields:
      - { label: 'Nome da Página', name: 'pageName', widget: 'string' }
      - { label: 'Título do Blog', name: 'blogTitle', widget: 'string' }
      - { label: 'Tag do Título', name: 'titleTag', widget: 'string' }
      - { label: 'Descrição', name: 'blogDescription', widget: 'string' }
      - { label: 'Autor', name: 'author', widget: 'string' }
      - { label: 'Data', name: 'date', widget: 'datetime' }
      - { label: 'Tags', name: 'tags', widget: 'list', default: ['post'] }
      - { label: 'Imagem Destacada', name: 'image', widget: 'image' }
      - { label: 'Legenda da Imagem', name: 'imageAlt', widget: 'string' }
      - { label: 'Conteúdo', name: 'body', widget: 'markdown' }
```

---

### Migrando posts antigos para o novo blog  

Basta duplicar o **blog-template.md** e criar um novo arquivo markdown com o mesmo nome do slug do blog antigo.  

Se o post antigo tinha o slug **"how-to-do-something.html"**, crie um arquivo **how-to-do-something.md** dentro da pasta **/blog** e preencha as informações do front matter.  

A variável **pageName** deve corresponder ao caminho correto. Se o post antigo era **/blog/how-to-do-something**, defina **pageName** como **"blog/how-to-do-something"**. Isso preserva o SEO e evita erros **404**.  

Copie o conteúdo do post antigo e converta-o para **Markdown** usando esta ferramenta:  
🔗 [HTML para Markdown](https://www.browserling.com/tools/html-to-markdown)  

Depois, cole o texto convertido no novo arquivo. O blog.css já tem os estilos aplicados, então todas as imagens, títulos e listas serão formatadas corretamente.  

Assim que o site for atualizado, o cliente poderá editar os posts diretamente pelo CMS.  

---

### Adicionando posts em destaque  

Para destacar um post no blog, basta adicionar a tag **featured** no front matter:  

```yaml
tags:
  - post
  - featured
```

O cliente pode gerenciar isso no CMS, bastando adicionar **,featured** na caixa de tags.  

---

### Coisas a fazer antes da publicação  

#### Criar um **sitemap.xml**  

1. Gere um sitemap usando esta ferramenta:  
   🔗 [Gerador de Sitemap](https://www.xml-sitemaps.com/)  
2. Crie um arquivo **sitemap.njk** na pasta **/src** e adicione:  

```yaml
---
permalink: '/sitemap.xml'
eleventyExcludeFromCollections: true
---
```

3. Cole o código do sitemap logo abaixo do front matter, **sem espaços** entre eles.  

---

#### Criar um **robots.txt**  

1. Adicione um arquivo **robots.txt** na pasta **/src**.  
2. Inclua **Disallow: /admin/** para impedir que essa pasta seja indexada pelo Google.  
3. Adicione a URL do sitemap:  

```
Sitemap: https://www.seusite.com/sitemap.xml
```

---

#### Criar **redirecionamentos** no Netlify  

1. Crie um arquivo **_redirects** na pasta **/src** (sem extensão).  
2. Adicione redirecionamentos no formato:  

```
/pagina-antiga /pagina-nova
```

---

### Conectando o blog ao Netlify CMS  

1. No Netlify, vá até **Identity** e clique em **Enable Identity**.  
2. Convide o cliente para acessar o site.  
3. Configure as preferências de registro.  

🔗 [Vídeo tutorial](https://youtu.be/v6LaVds4yeU?t=3361)  

---