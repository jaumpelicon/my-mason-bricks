# Project Setup Brick
Esta brick deve ser utilizada para acelerar o processo de setup de um projeto ou módulo Flutter.

Contém as seguintes configurações:
 - Localize
 - Lints
 - Force update
 - Service locator
 - Git ignore
 - Mobile router (opcional com ou sem go_router)
 - Merge request template
 - Classes de estilo como o AppColors e o AppThemes
 - Uma tela inicial de exemplo
 - Fastlane

## Como usar esta brick?

1. Desative as opções web, windows e linux caso o projeto seja apenas mobile usando:
```bash
$ flutter config --no-enable-web
$ flutter config --no-enable-linux-desktop
$ flutter config --no-enable-windows-desktop
```

2. Crie seu projeto usando o seguinte comando:
```bash
$ flutter create -org br.com.organization nomedoprojeto
```

3. Instale a dependência desta brick usando este comando:
```bash
$ mason add project_setup
```

4. Adicione a brick de setup com o seguinte comando dentro do seu projeto:
```bash
$ mason make project_setup
```

5. Alguns arquivos terão conflitos ao gerar a brick, aceite sobrescreve-los utilizando o `y (yes)` para substituir pelo arquivo gerado pela brick
<div style="text-align: left"> 
	<img src="images/brick_conflicts_example.jpeg" height="200">
</div>


- Está quase pronto, mas para conseguir rodar seu projeto no Android você precisa alterar as versões de suporte do app no gradle, para isso siga os seguintes passos:

1. Abra o arquivo `build.gradle` dentro da pasta `android/app`

2. Vá até `defaultConfig` e troque o valor dos campos `minSdkVersion` para 23 e do `targetSdkVersion` para 33, dessa forma:
```
    defaultConfig {
        applicationId "br.com.organization.mason"
        minSdkVersion 23
        targetSdkVersion 33
        versionCode flutterVersionCode.toInteger()
        versionName flutterVersionName
    }
```    

## O que falta para concluir o setup?

- No `pubspec.yaml` altere o `name` com o nome do seu projeto
- Será necessário alterar as versões de suporte do iOS, para isso pesquise por `IPHONEOS_DEPLOYMENT_TARGET` dentro de `project.pbxproj` e altere o valor para a versão atual que damos suporte (14). Faça isso nos 3 lugares onde o `IPHONEOS_DEPLOYMENT_TARGET` for chamado
- Preencher o arquivo `Variables` e `Matchfile` para concluir a automação com o Fastlane no iOS
- Alterar o nome e a logo do app