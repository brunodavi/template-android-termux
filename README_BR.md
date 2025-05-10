# Template Android para Termux

Este template foi criado para facilitar a configuração de um ambiente Android dentro do **Termux**. Ele instala automaticamente o SDK do Android ao executar `./gradlew`, tornando o processo simples e portátil para desenvolvimento direto do terminal Android.


## Pré-requisitos

Antes de utilizar o template, é necessário atualizar os pacotes do Termux e instalar as dependências necessárias:

```bash
pkg update
pkg upgrade # opcional
pkg install openjdk-17 aapt2
```

*Certifique-se de ter espaço suficiente em disco e conexão estável para download dos componentes.*


## Execução

Para iniciar a configuração automática do SDK e preparar o ambiente, basta executar:

```bash
./gradlew
```

Na primeira execução, o Gradle irá baixar o SDK do Android e todas as ferramentas necessárias, de acordo com as configurações no `gradle.properties`.


### Como Compilar o APK

Depois que todas as dependências estiverem configuradas, você pode compilar o APK com o comando:

```bash
./gradlew assembleDebug
```

O arquivo APK será gerado no seguinte caminho:

```
app/build/outputs/apk/debug/app-debug.apk
```

Para instalar no seu dispositivo:

1. Copie o APK para a pasta de downloads:

   ```bash
   cp app/build/outputs/apk/debug/app-debug.apk /sdcard/Download/
   ```
2. Abra um gerenciador de arquivos no celular.
3. Vá até a pasta **Download**.
4. Toque no arquivo APK para iniciar a instalação (certifique-se de permitir apps de fontes desconhecidas).


## Configuração via `gradle.properties`

As principais informações e dependências do projeto são definidas no arquivo `gradle.properties`:

```properties
# Informações do App
APP_PACKAGE=com.example.myapp
APP_VERSION=1.0
APP_VERSION_CODE=1
APP_MIN_SDK_VERSION=21
APP_TARGET_SDK_VERSION=33

# Dependências do Android
ANDROID_COMPILE_SDK_VERSION=33
ANDROID_BUILD_TOOLS_VERSION=33.0.2
ANDROID_GRADLE_PLUGIN_VERSION=8.3.0

# Caminho para o aapt2 no Termux
android.aapt2FromMavenOverride=/data/data/com.termux/files/usr/bin/aapt2
# org.gradle.jvmargs=-Xmx512m -XX:MaxPermSize=256m
```

Essas variáveis são automaticamente integradas à configuração do projeto, facilitando personalizações sem alterar diretamente os arquivos de build.


## Configuração de Java

A versão do Java utilizada pelo projeto é definida no arquivo `app/build.gradle`:

```groovy
compileOptions {
    sourceCompatibility JavaVersion.VERSION_17
    targetCompatibility JavaVersion.VERSION_17
}
```

Isso garante compatibilidade com bibliotecas modernas e o correto funcionamento com o OpenJDK 17 instalado no Termux.


## Dica: Limite de Memória no Gradle

Em dispositivos Android com recursos limitados, o uso de memória pode travar o Termux ou o próprio celular. Para evitar isso, é recomendável limitar a RAM usada pelo Gradle. Isso pode ser feito adicionando as seguintes opções ao `gradle.properties`:

```properties
org.gradle.jvmargs=-Xmx512m -XX:MaxPermSize=256m
```

Você pode ajustar o valor conforme a capacidade do seu dispositivo (ex: `-Xmx256m` para dispositivos com menos RAM).


## Contribuição

Sinta-se à vontade para clonar, adaptar e contribuir com este template. Ele foi pensado para quem quer desenvolver apps Android diretamente do celular, sem depender de IDEs pesadas.
