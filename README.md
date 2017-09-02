# Android-Neo
### Fazer o seu celular Android sair da "matrix".

### 1. Introduçao
Quando voce compra um celular de operadoras, ele costuma vir com alguns apps que voce nao consegue desinstalar. No meu caso tenho um celular VIVO e quero arrancar aqueles apps que vem pre-instalados sem meu concentimento, afinal sou do mundo UNIX e gosto de controlar minha Vida e meu software.
#### 1.1 Pre-Requisitos
*- Ter o root instaldo no telefone
*- Ter um bom servidor de SSH no telefone (SSHelper)

### 2. Desinstalando as propagandas e apps da VIVO
Acesso o telefone via SSH

Acesse o root:
```bash
su
```

Primeiro voce deve saber quais sao os softwares instalados da vivo em seu celular. Liste todos os softwares e mande o celular o linux (sim seu Android eh um Linux) do seu telefone mostrar tudo que tem 'vivo' na composiçao de seu nome. Use a ferramenta 'pm' (Package Manager) que vem no Android para fazer estas alteraçoes:
```bash
pm list  packages -l |grep vivo
```

```bash
br.com.bemobi.appsclub.vivo
br.com.m4u.recarga.vivo
com.terra.appcreator.downloadsvivo
com.movile.android.appsvivo
```

```bash
pm uninstall br.com.bemobi.appsclub.vivo
pm uninstall br.com.m4u.recarga.vivo
pm uninstall com.terra.appcreator.downloadsvivo
pm uninstall com.movile.android.appsvivo
```

```bash
Failure [DELETE_FAILED_INTERNAL_ERROR]
```

Veja o que restou

```bash
pm list  packages  |grep vivo
```

Arrancando na marra

Veja onde estao os pacotes das aplicaçoes (classes)

```bash
pm list  packages -f |grep vivo
```

```bash
package:/system/priv-app/vivo_apps_club_v92/vivo_apps_club_v92.apk=br.com.bemobi.appsclub.vivo
package:/data/app/br.com.m4u.recarga.vivo-2/base.apk=br.com.m4u.recarga.vivo
package:/system/priv-app/downloadsvivo-1-7-1-0/downloadsvivo-1-7-1-0.apk=com.terra.appcreator.downloadsvivo
package:/system/priv-app/vivo-apps-embedded-2.5.3/vivo-apps-embedded-2.5.3.apk=com.movile.android.appsvivo
```

Remonte system com permissao de escrita

```bash
mount -o remount,rw /system
```

```bash
cd /system/priv-app
```

```bash
rm -rf vivo-apps-embedded-2.5.3
rm -r vivo_apps_club_v92
rm -r downloadsvivo-1-7-1-0
```




