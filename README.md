# Sobre o Expo EAS Build

## Sites importantes:

https://expo.dev/

https://expo.dev/eas

https://docs.expo.dev/build/introduction/

https://docs.expo.dev/build/setup/

https://docs.expo.dev/eas-update/introduction/

https://docs.expo.dev/build-reference/apk/

## Formatos de arquivos compilados para as plataformas

- iOS: extensão IPA 

- Android: extensão APK (uso geral) e extensão .AAB (otimizada para loja Play Store)

## Roteiro geral de compilação no EAS

1. Acessar sua conta Expo no site expo.dev
2. Criar um projeto colocando o nome do aplicativo (isso também gera um nome simplificado no campo slug).

Obs: isso criará um IDENTIFICADOR para seu projeto.

3. Instalar o eas-cli: `npm install --global eas-cli`
4. Verificar se está logado usando: `eas whoami`

Obs.: Se estiver logado com a conta errada (ou outra), faça `eas logout`, e em seguida use `eas login` para entrar com suas credenciais.

5. Acesse a pasta do projeto do app que deseja compilar, e execute o comando `eas init --id CÓDIGO-ID-DO-SEU-PROJETO-CRIADO-NO-EXPO-DEV`

6. Instalar o Expo Update: `npx expo install expo-updates`

7. Inicializar o projeto com EAS Update: `eas update:configure`

8. Configurar o Build: `eas build:configure`

9. Configurar Build COM o UPDATE: `eas update:configure`

10. Ajustes no arquivo `eas.json` para compilar em formato **APK**:

Adicione em `preview` o seguinte código:

```json
"developmentClient" : true,
      "android" : {
        "buildType": "apk",
        "gradleCommand": ":app:assembleRelease"
      },
```

11. Iniciar a compilação (build): `eas build --profile preview`

Obs.: escolha a plataforma Android.

**ATENÇÃO!** 

Pode ser que, devido a quantidade de acessos aos servidores do Expo EAS, sua solicitação de compilação entre em uma **fila (queue)** de espera. Neste caso, não tem o que fazer a não ser aguardar.

Ao final do processo, será gerado um QR Code e link para download e instalação.

### Para testes de atualização usando Expo Update

1. Faça algumas modificações no seu projeto (mudança de texto, cor, adição de um componente, mudança de lógica em alguma função etc).

2. Execute um `npm start` apenas para garantir a injeção das mudanças no código-fonte (não é necessário usar o Expo Go). Em seguida, pare (CTRL C)

3. Publique a atualização usando: `eas update --branch preview --message "Pequena descrição das mudanças"`

Para que a atualização entre no app instalado, é necessário fechar e abrir o app no dispositivo pelo menos 2x.

**ATENÇÃO:** esse processo de update via expo nem sempre funciona bem ou para qualquer atualização. Caso não dê certo, a alternativa é executar um novo build do app com `eas build --profile preview`.
