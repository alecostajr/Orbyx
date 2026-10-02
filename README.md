<div align="center">
<img width="1200" height="475" alt="GHBanner" src="https://ai.google.dev/static/site-assets/images/share-ais-513315318.png" />
</div>

## Backend compartilhado e portal web

O backend Node.js serve o site e a API REST no mesmo endereço, persistindo usuários, sessões e demandas em SQLite. Requer Node.js 22.13 ou superior; não precisa instalar pacotes. O site e o app atualizam as demandas compartilhadas enquanto estão conectados. A sincronização cobre contas e campos principais das demandas; checklists, fotos, despesas e equipamentos continuam locais ao app.

Para iniciar em desenvolvimento, em um terminal PowerShell:

```powershell
Set-Location backend
Copy-Item .env.example .env
npm.cmd start
```

Abra `http://localhost:8787`. O usuário local de demonstração é `admin` com senha `123`; as outras contas do app (`mariana`, `lucas`, `carlos` e `juliana`) também são semeadas com senha `123`. Esses dados são apenas para desenvolvimento. O SQLite é criado em `backend/data/orbyx.sqlite`.

No primeiro login de uma conta administradora em uma instalação Android antiga, as contas com senha e as demandas existentes no Room são importadas uma vez. As senhas são gravadas no servidor como hash e apagadas do banco local após a confirmação. O app mantém o Room como cache e sincroniza as alterações quando volta a ter rede.

Execute os testes do backend com `npm.cmd test` dentro de `backend`.

O emulador Android usa por padrão `http://10.0.2.2:8787/api/`. Para um aparelho físico, configure a propriedade Gradle `ORBYX_API_BASE_URL` com o IP da máquina na rede, por exemplo `http://192.168.1.20:8787/api/`, e permita a porta 8787 no firewall local. O build debug aceita HTTP apenas para desenvolvimento. Para `release`, a propriedade é obrigatória e precisa começar com `https://`; configure-a em `%USERPROFILE%\.gradle\gradle.properties`.

Antes de expor o sistema ou usar dados reais: configure `DEMO_MODE=false`, crie `BOOTSTRAP_ADMIN_USERNAME`, `BOOTSTRAP_ADMIN_NAME` e uma `BOOTSTRAP_ADMIN_PASSWORD` forte com ao menos 12 caracteres; configure `ORBYX_API_BASE_URL` com HTTPS; proteja o host com TLS, backup e regras de rede. Não publique o servidor de demonstração: as contas semeadas usam senhas conhecidas.

# Run and deploy your AI Studio app

This contains everything you need to run your app locally.

View your app in AI Studio: https://ai.studio/apps/b4ccdbc0-91bc-451c-b11c-cf1ff53d15e5

## Run Locally

**Prerequisites:**  [Android Studio](https://developer.android.com/studio)


1. Open Android Studio
2. Select **Open** and choose the directory containing this project
3. Allow Android Studio to fix any incompatibilities as it imports the project.
4. Create a file named `.env` in the project directory and set `GEMINI_API_KEY` in that file to your Gemini API key (see `.env.example` for an example)
5. Remove this line from the app's `build.gradle.kts` file: `signingConfig = signingConfigs.getByName("debugConfig")`
6. Run the app on an emulator or physical device
7. If you have already published your app in AI Studio, please [request upload key reset](https://support.google.com/googleplay/android-developer/answer/9842756#zippy=%2Crequest-an-upload-key-reset) in Google Play Console.
