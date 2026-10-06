# Atividade: layout em Flutter

Implementação do layout do [tutorial oficial Build a Flutter layout](https://docs.flutter.dev/ui/layout/tutorial?authuser=0), realizada em 06/10/2026.

## Resultado

A tela inicial apresenta uma foto do lago Oeschinen, nome e localização, uma estrela com a contagem 41, os ícones CALL / ROUTE / SHARE e a descrição do local. O conteúdo permite rolagem vertical quando não cabe na tela.

Os rótulos e o texto foram mantidos em inglês para acompanhar a referência. Esta atividade implementa a apresentação visual: os ícones não realizam ligações, navegação ou compartilhamento, e a avaliação é fixa.

## Passo a passo realizado

### 1. Inspecionar o projeto e consultar a referência

Foram lidos `lib/main.dart`, `pubspec.yaml` e as regras de análise do projeto, além do tutorial. O aplicativo existente continha apenas “Hello World!”. Foi mantida a classe de entrada `MainApp`, sem recriar o projeto nem adicionar dependências.

### 2. Planejar a árvore de widgets

A tela foi dividida em componentes independentes, todos em `lib/main.dart`:

```text
MainApp
└── MaterialApp
    └── Scaffold
        ├── AppBar
        └── SingleChildScrollView
            └── Column
                ├── ImageSection
                ├── TitleSection
                ├── ButtonSection
                │   └── 3 × ButtonWithText
                └── TextSection
```

### 3. Substituir a tela inicial

O `MaterialApp` recebeu o título `Flutter layout demo`. O `Scaffold` passou a ter uma `AppBar` e um corpo com `SingleChildScrollView`. A `Column` organiza as quatro seções na ordem de leitura; a rolagem permite acessar o conteúdo em telas com pouca altura.

Foi preservado o import `package:flutter/material.dart`, disponível no SDK deste projeto, para utilizar os componentes Material sem introduzir outro pacote.

### 4. Construir a seção de título

Foi criado o widget `TitleSection`, com parâmetros `name` e `location`. Um `Expanded` reserva o espaço disponível para os textos dentro da linha, ao lado da estrela vermelha e da contagem. O nome fica em negrito e a localização em cinza. A seção usa espaçamento externo de 32 e separação de 8 entre os textos.

### 5. Construir a seção de ações

O widget `ButtonWithText` recebe cor, ícone e rótulo, permitindo reutilizar a mesma apresentação nas três ações. `ButtonSection` distribui esses componentes horizontalmente. A cor vem do tema, e cada rótulo tem tamanho 12 e distância de 8 do ícone. Não foram adicionados callbacks, pois a atividade trata de layout.

### 6. Inserir a descrição

O widget `TextSection` recebe a descrição por parâmetro. O texto possui quebra automática de linhas (`softWrap: true`) e espaçamento de 32 ao redor. Foi usado o conteúdo apresentado no exemplo, com os créditos indicados ao final deste documento.

### 7. Baixar e registrar a imagem

Foi criada a pasta `images` e baixado o arquivo oficial para `images/lake.jpg`. O download inicial falhou por conexão no ambiente restrito; a nova tentativa autorizada foi concluída.

Comandos PowerShell equivalentes, executados na raiz do projeto:

```powershell
New-Item -ItemType Directory -Path images -Force
Invoke-WebRequest -Uri 'https://raw.githubusercontent.com/flutter/website/main/examples/layout/lakes/step5/images/lake.jpg' -OutFile images/lake.jpg
```

O arquivo foi declarado em `pubspec.yaml`:

```yaml
flutter:
  uses-material-design: true
  assets:
    - images/lake.jpg
```

`ImageSection` carrega o asset local com largura de 600, altura de 240 e `BoxFit.cover`, respeitando as restrições de largura da tela. Também foi adicionada uma descrição semântica em português para leitores de tela. A imagem é empacotada com o aplicativo e não depende de download durante o uso.

### 8. Formatar e validar

O arquivo Dart foi formatado e a análise estática foi executada com o SDK encontrado em `C:/Users/1028392/Documents/Flutter/flutter` (o comando `flutter` não estava no PATH desta sessão).

Comandos para repetir a validação com Flutter no PATH:

```powershell
dart format lib/main.dart
flutter analyze
flutter build web
```

A análise estática terminou sem problemas (`No issues found!`). O ambiente restrito impediu o início do analisador; a validação foi repetida com permissão para acessar o SDK e seus processos.

A compilação web foi concluída em `build/web` com Flutter 3.47.6 e Dart 3.13.5. O arquivo da foto foi incluído em `build/web/assets/images/lake.jpg`, com o mesmo SHA-256 do original. A compilação emitiu um aviso sobre a fonte opcional CupertinoIcons; a tela utiliza apenas MaterialIcons, cuja fonte foi incluída. Não houve execução manual em navegador ou emulador nesta sessão; a conferência visual descrita a seguir pode ser feita ao executar o aplicativo.

### 9. Executar e conferir a tela

Na raiz do projeto:

```powershell
flutter pub get
flutter run -d chrome
```

Para executar em outro dispositivo, consulte `flutter devices` e utilize `flutter run -d <id>`. Se o SDK não estiver no PATH, no PowerShell utilize `& 'C:/Users/1028392/Documents/Flutter/flutter/bin/flutter.bat'` no lugar de `flutter`.

Na conferência manual, verifique a foto no topo, as informações do local, os três ícones e a descrição. Reduza a altura da janela para conferir a rolagem. Ao adicionar um novo asset a uma execução existente, reinicie o aplicativo para atualizar o pacote de recursos.

## Arquivos da atividade

| Arquivo | Finalidade |
| --- | --- |
| `lib/main.dart` | Tela e componentes do layout |
| `pubspec.yaml` | Registro do asset |
| `images/lake.jpg` | Foto usada na tela |
| `README.md` | Passos de implementação, validação e execução |

## Referências e créditos

- [Tutorial oficial do Flutter](https://docs.flutter.dev/ui/layout/tutorial?authuser=0).
- [Imagem fornecida pelo exemplo](https://raw.githubusercontent.com/flutter/website/main/examples/layout/lakes/step5/images/lake.jpg).
- Fotografia: Dino Reichmuth / Unsplash, conforme crédito do tutorial.
- Texto descritivo: Switzerland Tourism, conforme crédito do tutorial.
- Os exemplos de código da documentação Flutter são disponibilizados sob licença BSD de três cláusulas; o restante da documentação, salvo indicação contrária, usa CC BY 4.0.
