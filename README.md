# Android-Neo
### Fazer o seu celular Android sair da "matrix".

### 1. Introduçao
Quando voce compra um celular de operadoras, ele costuma vir com alguns apps que voce nao consegue desinstalar. No meu caso tenho um celular VIVO e quero arrancar aqueles apps que vem pre-instalados sem meu concentimento, afinal sou do mundo UNIX e gosto de controlar minha Vida e meu software.
#### 1.1 Pre-Requisitos
* - Ter o root instaldo no telefone
* - Ter um bom servidor de SSH no telefone (SSHelper)

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

# Fritando pacotes de coleta de informaçoes da SAMSUNG

Claro, voce ja deve suspeitar, seu smartphone coleta informaçoes de uso e encaminha para terceiros, no caso, SAMSUNG.
Caso voce queira uma amostra do que ela coleta de uma olhada no log do serviço `usagestats` destes pacotes **intelligenceservice** e **intelligenceservice2** conclua se a SAMSUNG tem boas intençoes com o usuario.
```
  user=0 
    In-memory daily stats
    timeRange="03/09/2017 21:00 – 23:15" 
      packages
        package=com.sec.android.providers.mapcon totalTime="00:00" lastTime="31/12/1969 21:00" lastTimeSystem="03/09/2017 23:11" inactiveTime="03:43" 
        package=com.google.android.youtube totalTime="00:17" lastTime="03/09/2017 23:02" lastTimeSystem="03/09/2017 23:02" inactiveTime="03:17" 
        package=com.samsung.android.app.cocktailbarservice totalTime="00:00" lastTime="31/12/1969 21:00" lastTimeSystem="03/09/2017 23:13" inactiveTime="02:59" 
        package=com.android.providers.telephony totalTime="00:00" lastTime="31/12/1969 21:00" lastTimeSystem="03/09/2017 23:11" inactiveTime="03:43" 
        package=com.sec.android.providers.iwlansettings totalTime="00:00" lastTime="31/12/1969 21:00" lastTimeSystem="03/09/2017 23:11" inactiveTime="03:43" 
        package=com.google.android.googlequicksearchbox totalTime="00:00" lastTime="03/09/2017 23:13" lastTimeSystem="03/09/2017 23:13" inactiveTime="02:40" 
        package=com.arachnoid.sshelper totalTime="01:24" lastTime="03/09/2017 23:13" lastTimeSystem="03/09/2017 23:13" inactiveTime="02:29" 
        package=com.android.providers.media totalTime="00:00" lastTime="31/12/1969 21:00" lastTimeSystem="03/09/2017 23:13" inactiveTime="02:27" 
        package=com.sec.android.app.wfdbroker totalTime="00:00" lastTime="31/12/1969 21:00" lastTimeSystem="03/09/2017 23:11" inactiveTime="03:40" 
        package=org.simalliance.openmobileapi.service totalTime="00:00" lastTime="31/12/1969 21:00" lastTimeSystem="03/09/2017 23:11" inactiveTime="03:42" 
        package=com.whatsapp totalTime="02:20" lastTime="03/09/2017 22:21" lastTimeSystem="03/09/2017 23:12" inactiveTime="03:07" 
        package=com.android.providers.downloads totalTime="00:00" lastTime="31/12/1969 21:00" lastTimeSystem="03/09/2017 23:13" inactiveTime="02:27" 
        package=com.samsung.android.qconnect totalTime="00:00" lastTime="31/12/1969 21:00" lastTimeSystem="03/09/2017 23:13" inactiveTime="02:59" 
        package=com.samsung.ucs.agent.boot totalTime="00:00" lastTime="31/12/1969 21:00" lastTimeSystem="03/09/2017 23:11" inactiveTime="03:43" 
        package=com.wsomacp totalTime="00:00" lastTime="31/12/1969 21:00" lastTimeSystem="03/09/2017 23:11" inactiveTime="03:21" 
        package=com.samsung.faceservice totalTime="00:00" lastTime="31/12/1969 21:00" lastTimeSystem="03/09/2017 23:13" inactiveTime="02:58" 
        package=com.samsung.android.email.provider totalTime="00:33" lastTime="03/09/2017 21:32" lastTimeSystem="03/09/2017 23:12" inactiveTime="03:07" 
        package=com.sec.android.emergencymode.service totalTime="00:00" lastTime="31/12/1969 21:00" lastTimeSystem="03/09/2017 23:12" inactiveTime="03:04" 
        package=com.sec.android.daemonapp totalTime="00:00" lastTime="31/12/1969 21:00" lastTimeSystem="03/09/2017 23:12" inactiveTime="03:19" 
        package=com.android.vending totalTime="00:00" lastTime="31/12/1969 21:00" lastTimeSystem="03/09/2017 23:13" inactiveTime="02:58" 
        package=com.microsoft.skydrive totalTime="00:00" lastTime="31/12/1969 21:00" lastTimeSystem="03/09/2017 23:13" inactiveTime="03:03" 
        package=com.sec.android.provider.badge totalTime="00:00" lastTime="31/12/1969 21:00" lastTimeSystem="03/09/2017 23:13" inactiveTime="02:20" 
        package=com.samsung.android.communicationservice totalTime="00:00" lastTime="31/12/1969 21:00" lastTimeSystem="03/09/2017 23:13" inactiveTime="02:55" 
        package=com.samsung.cmh totalTime="00:00" lastTime="31/12/1969 21:00" lastTimeSystem="03/09/2017 23:13" inactiveTime="02:58" 
        package=android totalTime="00:08" lastTime="03/09/2017 23:11" lastTimeSystem="03/09/2017 23:11" inactiveTime="03:28" 
        package=com.samsung.hs20provider totalTime="00:00" lastTime="31/12/1969 21:00" lastTimeSystem="03/09/2017 23:12" inactiveTime="03:13" 
        package=com.android.mms totalTime="00:16" lastTime="03/09/2017 23:13" lastTimeSystem="03/09/2017 23:13" inactiveTime="02:40" 
        package=com.android.nfc totalTime="00:00" lastTime="31/12/1969 21:00" lastTimeSystem="03/09/2017 23:11" inactiveTime="03:43" 
        package=com.google.android.gm totalTime="00:00" lastTime="31/12/1969 21:00" lastTimeSystem="03/09/2017 23:12" inactiveTime="03:07" 
        package=com.samsung.android.providers.context totalTime="00:00" lastTime="31/12/1969 21:00" lastTimeSystem="03/09/2017 23:11" inactiveTime="03:40" 
        package=com.android.printspooler totalTime="00:00" lastTime="31/12/1969 21:00" lastTimeSystem="03/09/2017 23:11" inactiveTime="03:43" 
        package=com.samsung.storyservice totalTime="00:00" lastTime="31/12/1969 21:00" lastTimeSystem="03/09/2017 23:13" inactiveTime="02:58" 
        package=com.samsung.android.service.peoplestripe totalTime="00:00" lastTime="31/12/1969 21:00" lastTimeSystem="03/09/2017 23:11" inactiveTime="03:46" 
        package=com.sec.smartcard.manager totalTime="00:00" lastTime="31/12/1969 21:00" lastTimeSystem="03/09/2017 23:11" inactiveTime="03:43" 
        package=br.com.bb.android totalTime="00:05" lastTime="03/09/2017 23:01" lastTimeSystem="03/09/2017 23:01" inactiveTime="03:40" 
        package=com.samsung.android.app.taskedge totalTime="00:00" lastTime="31/12/1969 21:00" lastTimeSystem="03/09/2017 23:12" inactiveTime="03:17" 
        package=com.sec.android.inputmethod totalTime="00:00" lastTime="31/12/1969 21:00" lastTimeSystem="03/09/2017 23:04" inactiveTime="01:22" 
        package=com.samsung.android.app.catchfavorites totalTime="00:00" lastTime="31/12/1969 21:00" lastTimeSystem="03/09/2017 23:11" inactiveTime="03:46" 
        package=com.google.android.syncadapters.contacts totalTime="00:00" lastTime="31/12/1969 21:00" lastTimeSystem="03/09/2017 23:12" inactiveTime="03:07" 
        package=com.android.keychain totalTime="00:00" lastTime="31/12/1969 21:00" lastTimeSystem="03/09/2017 23:12" inactiveTime="03:05" 
        package=com.samsung.android.themecenter totalTime="00:00" lastTime="31/12/1969 21:00" lastTimeSystem="03/09/2017 23:12" inactiveTime="03:03" 
        package=com.google.android.gms totalTime="00:00" lastTime="31/12/1969 21:00" lastTimeSystem="03/09/2017 23:14" inactiveTime="02:01" 
        package=com.google.android.gsf totalTime="00:00" lastTime="31/12/1969 21:00" lastTimeSystem="03/09/2017 23:14" inactiveTime="01:58" 
        package=com.gopro.smarty totalTime="00:00" lastTime="31/12/1969 21:00" lastTimeSystem="03/09/2017 22:15" inactiveTime="05:05" 
        package=com.sec.android.app.launcher totalTime="02:04" lastTime="03/09/2017 23:13" lastTimeSystem="03/09/2017 23:13" inactiveTime="02:29" 
        package=com.facebook.katana totalTime="00:00" lastTime="31/12/1969 21:00" lastTimeSystem="03/09/2017 22:15" inactiveTime="05:05" 
        package=com.samsung.enhanceservice totalTime="00:00" lastTime="31/12/1969 21:00" lastTimeSystem="03/09/2017 23:13" inactiveTime="02:58" 
        package=com.samsung.android.beaconmanager totalTime="00:00" lastTime="31/12/1969 21:00" lastTimeSystem="03/09/2017 23:13" inactiveTime="02:59" 
        package=com.samsung.ucs.ucspinpad totalTime="00:00" lastTime="31/12/1969 21:00" lastTimeSystem="03/09/2017 23:11" inactiveTime="03:40" 
        package=com.sec.phone totalTime="00:00" lastTime="31/12/1969 21:00" lastTimeSystem="03/09/2017 23:12" inactiveTime="03:14" 
        package=com.samsung.android.scloud totalTime="00:00" lastTime="31/12/1969 21:00" lastTimeSystem="03/09/2017 23:12" inactiveTime="03:07" 
        package=com.samsung.android.spayfw totalTime="00:00" lastTime="31/12/1969 21:00" lastTimeSystem="03/09/2017 23:15" inactiveTime="00:49" 
        package=com.samsung.android.spay totalTime="00:00" lastTime="31/12/1969 21:00" lastTimeSystem="03/09/2017 23:12" inactiveTime="03:07" 
        package=com.samsung.android.sm.policy totalTime="00:00" lastTime="31/12/1969 21:00" lastTimeSystem="03/09/2017 23:12" inactiveTime="03:14" 
        package=com.wssnps totalTime="00:00" lastTime="31/12/1969 21:00" lastTimeSystem="03/09/2017 23:12" inactiveTime="03:08" 
        package=eu.chainfire.supersu totalTime="00:00" lastTime="31/12/1969 21:00" lastTimeSystem="03/09/2017 23:14" inactiveTime="01:17" 
        package=com.samsung.dcmservice totalTime="00:00" lastTime="31/12/1969 21:00" lastTimeSystem="03/09/2017 23:13" inactiveTime="02:58" 
        package=com.android.phone totalTime="00:00" lastTime="31/12/1969 21:00" lastTimeSystem="03/09/2017 23:11" inactiveTime="03:43" 
        package=com.android.providers.userdictionary totalTime="00:00" lastTime="31/12/1969 21:00" lastTimeSystem="03/09/2017 23:13" inactiveTime="02:54" 
        package=com.samsung.android.sm.provider totalTime="00:00" lastTime="31/12/1969 21:00" lastTimeSystem="03/09/2017 23:12" inactiveTime="03:15" 
        package=com.android.systemui totalTime="00:05" lastTime="03/09/2017 23:02" lastTimeSystem="03/09/2017 23:11" inactiveTime="03:46" 
        package=com.sec.android.app.SamsungContentsAgent totalTime="00:00" lastTime="31/12/1969 21:00" lastTimeSystem="03/09/2017 23:11" inactiveTime="03:40" 
        package=com.sec.android.provider.emergencymode totalTime="00:00" lastTime="31/12/1969 21:00" lastTimeSystem="03/09/2017 23:11" inactiveTime="03:46" 
        package=com.samsung.android.fingerprint.service totalTime="00:00" lastTime="31/12/1969 21:00" lastTimeSystem="03/09/2017 23:11" inactiveTime="03:32" 
        package=com.android.bluetooth totalTime="00:00" lastTime="31/12/1969 21:00" lastTimeSystem="03/09/2017 23:11" inactiveTime="03:40" 
        package=com.android.providers.contacts totalTime="00:00" lastTime="31/12/1969 21:00" lastTimeSystem="03/09/2017 23:13" inactiveTime="02:54" 
        package=com.samsung.ipservice totalTime="00:00" lastTime="31/12/1969 21:00" lastTimeSystem="03/09/2017 23:13" inactiveTime="02:58" 
        package=com.samsung.android.coreapps totalTime="00:00" lastTime="31/12/1969 21:00" lastTimeSystem="03/09/2017 23:13" inactiveTime="03:01" 
      configurations
        config=pt-rBR-ldltr-sw411dp-w411dp-h707dp-normal-long-notround-port-night-560dpi-notouch-keysexposed-nokeys-navhidden-nonav-v23 totalTime="00:00" lastTime="03/09/2017 23:11" count=1 
        config=pt-rBR-ldltr-sw411dp-w411dp-h707dp-normal-long-notround-port-560dpi-notouch-keysexposed-nokeys-navhidden-nonav-v23 totalTime="00:00" lastTime="03/09/2017 23:11" count=1 
        config=pt-rBR-ldltr-sw411dp-w411dp-h731dp-normal-long-notround-port-560dpi-notouch-keysexposed-nokeys-navhidden-nonav-v23 totalTime="00:00" lastTime="03/09/2017 23:11" count=1 
        config=pt-rBR-ldltr-sw411dp-w411dp-h707dp-normal-long-notround-port-night-560dpi-finger-keysexposed-nokeys-navhidden-nonav-v23 totalTime="00:05" lastTime="03/09/2017 23:11" count=1 
        config=pt-rBR-ldltr-sw411dp-w411dp-h707dp-normal-long-notround-port-night-560dpi-finger-keysexposed-nokeys-navhidden-nonav-v23 totalTime="00:10" lastTime="03/09/2017 23:11" count=1 
        config=mcc724-mnc10-pt-rBR-ldltr-sw411dp-w411dp-h707dp-normal-long-notround-port-night-560dpi-finger-keysexposed-nokeys-navhidden-nonav-v23 totalTime="00:00" lastTime="03/09/2017 23:11" count=1 
      events
        time="03/09/2017 21:18" type=USER_INTERACTION package=com.whatsapp 
        time="03/09/2017 21:18" type=MOVE_TO_FOREGROUND package=com.sec.android.app.launcher class=com.android.launcher2.Launcher 
        time="03/09/2017 21:18" type=MOVE_TO_BACKGROUND package=com.sec.android.app.launcher class=com.android.launcher2.Launcher 
        time="03/09/2017 21:18" type=MOVE_TO_FOREGROUND package=com.whatsapp class=com.whatsapp.Conversation 
        time="03/09/2017 21:18" type=MOVE_TO_BACKGROUND package=com.whatsapp class=com.whatsapp.Conversation 
        time="03/09/2017 21:18" type=MOVE_TO_FOREGROUND package=com.whatsapp class=com.whatsapp.HomeActivity 
        time="03/09/2017 21:18" type=MOVE_TO_BACKGROUND package=com.whatsapp class=com.whatsapp.HomeActivity 
        time="03/09/2017 21:18" type=MOVE_TO_FOREGROUND package=com.sec.android.app.launcher class=com.android.launcher2.Launcher 
        time="03/09/2017 21:19" type=MOVE_TO_BACKGROUND package=com.sec.android.app.launcher class=com.android.launcher2.Launcher 
        time="03/09/2017 21:19" type=MOVE_TO_FOREGROUND package=com.samsung.android.email.provider class=com.samsung.android.email.ui.activity.MessageListXL 
        time="03/09/2017 21:19" type=MOVE_TO_BACKGROUND package=com.samsung.android.email.provider class=com.samsung.android.email.ui.activity.MessageListXL 
        time="03/09/2017 21:19" type=MOVE_TO_FOREGROUND package=com.samsung.android.email.provider class=com.samsung.android.email.ui.activity.setup.AccountSetupSelectAccount 
        time="03/09/2017 21:19" type=MOVE_TO_BACKGROUND package=com.samsung.android.email.provider class=com.samsung.android.email.ui.activity.setup.AccountSetupSelectAccount 
        time="03/09/2017 21:30" type=USER_INTERACTION package=com.whatsapp 
        time="03/09/2017 21:30" type=MOVE_TO_FOREGROUND package=com.samsung.android.email.provider class=com.samsung.android.email.ui.activity.setup.AccountSetupSelectAccount 
        time="03/09/2017 21:30" type=MOVE_TO_BACKGROUND package=com.samsung.android.email.provider class=com.samsung.android.email.ui.activity.setup.AccountSetupSelectAccount 
        time="03/09/2017 21:30" type=MOVE_TO_FOREGROUND package=com.whatsapp class=com.whatsapp.HomeActivity 
        time="03/09/2017 21:30" type=MOVE_TO_BACKGROUND package=com.whatsapp class=com.whatsapp.HomeActivity 
        time="03/09/2017 21:30" type=MOVE_TO_FOREGROUND package=com.whatsapp class=com.whatsapp.Conversation 
        time="03/09/2017 21:30" type=MOVE_TO_BACKGROUND package=com.whatsapp class=com.whatsapp.Conversation 
        time="03/09/2017 21:30" type=MOVE_TO_FOREGROUND package=com.whatsapp class=com.whatsapp.MediaView 
        time="03/09/2017 21:30" type=MOVE_TO_BACKGROUND package=com.whatsapp class=com.whatsapp.MediaView 
        time="03/09/2017 21:30" type=MOVE_TO_FOREGROUND package=com.whatsapp class=com.whatsapp.Conversation 
        time="03/09/2017 21:30" type=MOVE_TO_BACKGROUND package=com.whatsapp class=com.whatsapp.Conversation 
        time="03/09/2017 21:30" type=MOVE_TO_FOREGROUND package=com.whatsapp class=com.whatsapp.MediaView 
        time="03/09/2017 21:31" type=MOVE_TO_BACKGROUND package=com.whatsapp class=com.whatsapp.MediaView 
        time="03/09/2017 21:31" type=MOVE_TO_FOREGROUND package=com.whatsapp class=com.whatsapp.Conversation 
        time="03/09/2017 21:31" type=MOVE_TO_BACKGROUND package=com.whatsapp class=com.whatsapp.Conversation 
        time="03/09/2017 21:31" type=MOVE_TO_FOREGROUND package=com.whatsapp class=com.whatsapp.MediaView 
        time="03/09/2017 21:31" type=MOVE_TO_BACKGROUND package=com.whatsapp class=com.whatsapp.MediaView 
        time="03/09/2017 21:31" type=MOVE_TO_FOREGROUND package=com.whatsapp class=com.whatsapp.Conversation 
        time="03/09/2017 21:31" type=MOVE_TO_BACKGROUND package=com.whatsapp class=com.whatsapp.Conversation 
        time="03/09/2017 21:31" type=MOVE_TO_FOREGROUND package=com.whatsapp class=com.whatsapp.ContactPicker 
        time="03/09/2017 21:32" type=MOVE_TO_BACKGROUND package=com.whatsapp class=com.whatsapp.ContactPicker 
        time="03/09/2017 21:32" type=MOVE_TO_FOREGROUND package=com.whatsapp class=com.whatsapp.Conversation 
        time="03/09/2017 21:32" type=MOVE_TO_BACKGROUND package=com.whatsapp class=com.whatsapp.Conversation 
        time="03/09/2017 21:32" type=MOVE_TO_FOREGROUND package=com.whatsapp class=com.whatsapp.HomeActivity 
        time="03/09/2017 21:32" type=MOVE_TO_BACKGROUND package=com.whatsapp class=com.whatsapp.HomeActivity 
        time="03/09/2017 21:32" type=MOVE_TO_FOREGROUND package=com.whatsapp class=com.whatsapp.Conversation 
        time="03/09/2017 21:32" type=MOVE_TO_BACKGROUND package=com.whatsapp class=com.whatsapp.Conversation 
        time="03/09/2017 21:32" type=MOVE_TO_FOREGROUND package=com.whatsapp class=com.whatsapp.HomeActivity 
        time="03/09/2017 21:32" type=MOVE_TO_BACKGROUND package=com.whatsapp class=com.whatsapp.HomeActivity 
        time="03/09/2017 21:32" type=MOVE_TO_FOREGROUND package=com.whatsapp class=com.whatsapp.Conversation 
        time="03/09/2017 21:32" type=MOVE_TO_BACKGROUND package=com.whatsapp class=com.whatsapp.Conversation 
        time="03/09/2017 21:32" type=MOVE_TO_FOREGROUND package=com.whatsapp class=com.whatsapp.HomeActivity 
        time="03/09/2017 21:32" type=MOVE_TO_BACKGROUND package=com.whatsapp class=com.whatsapp.HomeActivity 
        time="03/09/2017 21:32" type=MOVE_TO_FOREGROUND package=com.whatsapp class=com.whatsapp.Conversation 
        time="03/09/2017 21:32" type=MOVE_TO_BACKGROUND package=com.whatsapp class=com.whatsapp.Conversation 
        time="03/09/2017 21:32" type=MOVE_TO_FOREGROUND package=com.whatsapp class=com.whatsapp.HomeActivity 
        time="03/09/2017 21:32" type=MOVE_TO_BACKGROUND package=com.whatsapp class=com.whatsapp.HomeActivity 
        time="03/09/2017 21:32" type=MOVE_TO_FOREGROUND package=com.samsung.android.email.provider class=com.samsung.android.email.ui.activity.setup.AccountSetupSelectAccount 
        time="03/09/2017 21:32" type=MOVE_TO_BACKGROUND package=com.samsung.android.email.provider class=com.samsung.android.email.ui.activity.setup.AccountSetupSelectAccount 
        time="03/09/2017 21:32" type=MOVE_TO_FOREGROUND package=com.sec.android.app.launcher class=com.android.launcher2.Launcher 
        time="03/09/2017 21:32" type=MOVE_TO_BACKGROUND package=com.sec.android.app.launcher class=com.android.launcher2.Launcher 
        time="03/09/2017 22:21" type=USER_INTERACTION package=com.whatsapp 
        time="03/09/2017 22:21" type=MOVE_TO_FOREGROUND package=com.sec.android.app.launcher class=com.android.launcher2.Launcher 
        time="03/09/2017 22:21" type=MOVE_TO_BACKGROUND package=com.sec.android.app.launcher class=com.android.launcher2.Launcher 
        time="03/09/2017 22:21" type=MOVE_TO_FOREGROUND package=com.whatsapp class=com.whatsapp.HomeActivity 
        time="03/09/2017 22:21" type=MOVE_TO_BACKGROUND package=com.whatsapp class=com.whatsapp.HomeActivity 
        time="03/09/2017 22:21" type=MOVE_TO_FOREGROUND package=com.whatsapp class=com.whatsapp.Conversation 
        time="03/09/2017 22:21" type=MOVE_TO_BACKGROUND package=com.whatsapp class=com.whatsapp.Conversation 
        time="03/09/2017 22:21" type=MOVE_TO_FOREGROUND package=com.whatsapp class=com.whatsapp.HomeActivity 
        time="03/09/2017 22:21" type=MOVE_TO_BACKGROUND package=com.whatsapp class=com.whatsapp.HomeActivity 
        time="03/09/2017 22:21" type=MOVE_TO_FOREGROUND package=com.whatsapp class=com.whatsapp.Conversation 
        time="03/09/2017 22:21" type=MOVE_TO_BACKGROUND package=com.whatsapp class=com.whatsapp.Conversation 
        time="03/09/2017 22:21" type=MOVE_TO_FOREGROUND package=com.whatsapp class=com.whatsapp.HomeActivity 
        time="03/09/2017 22:21" type=MOVE_TO_BACKGROUND package=com.whatsapp class=com.whatsapp.HomeActivity 
        time="03/09/2017 22:21" type=MOVE_TO_FOREGROUND package=com.sec.android.app.launcher class=com.android.launcher2.Launcher 
        time="03/09/2017 22:22" type=MOVE_TO_BACKGROUND package=com.sec.android.app.launcher class=com.android.launcher2.Launcher 
        time="03/09/2017 23:01" type=USER_INTERACTION package=com.google.android.googlequicksearchbox 
        time="03/09/2017 23:01" type=MOVE_TO_FOREGROUND package=com.sec.android.app.launcher class=com.android.launcher2.Launcher 
        time="03/09/2017 23:01" type=MOVE_TO_BACKGROUND package=com.sec.android.app.launcher class=com.android.launcher2.Launcher 
        time="03/09/2017 23:01" type=MOVE_TO_FOREGROUND package=br.com.bb.android class=br.com.bb.android.StartActivity 
        time="03/09/2017 23:01" type=MOVE_TO_BACKGROUND package=br.com.bb.android class=br.com.bb.android.StartActivity 
        time="03/09/2017 23:01" type=MOVE_TO_FOREGROUND package=br.com.bb.android class=br.com.bb.android.appscontainer.smartphone.AppsContainerActivitySmartphone 
        time="03/09/2017 23:01" type=MOVE_TO_BACKGROUND package=br.com.bb.android class=br.com.bb.android.appscontainer.smartphone.AppsContainerActivitySmartphone 
        time="03/09/2017 23:01" type=MOVE_TO_FOREGROUND package=com.sec.android.app.launcher class=com.android.launcher2.Launcher 
        time="03/09/2017 23:01" type=MOVE_TO_BACKGROUND package=com.sec.android.app.launcher class=com.android.launcher2.Launcher 
        time="03/09/2017 23:01" type=MOVE_TO_FOREGROUND package=com.google.android.youtube class=com.google.android.youtube.app.honeycomb.Shell$HomeActivity 
        time="03/09/2017 23:01" type=MOVE_TO_BACKGROUND package=com.google.android.youtube class=com.google.android.youtube.app.honeycomb.Shell$HomeActivity 
        time="03/09/2017 23:01" type=MOVE_TO_FOREGROUND package=com.google.android.youtube class=com.google.android.apps.youtube.app.WatchWhileActivity 
        time="03/09/2017 23:02" type=MOVE_TO_BACKGROUND package=com.google.android.youtube class=com.google.android.apps.youtube.app.WatchWhileActivity 
        time="03/09/2017 23:02" type=MOVE_TO_FOREGROUND package=com.sec.android.app.launcher class=com.android.launcher2.Launcher 
        time="03/09/2017 23:02" type=MOVE_TO_BACKGROUND package=com.sec.android.app.launcher class=com.android.launcher2.Launcher 
        time="03/09/2017 23:02" type=MOVE_TO_FOREGROUND package=com.android.systemui class=com.android.systemui.recents.SeparatedRecentsActivity 
        time="03/09/2017 23:02" type=MOVE_TO_BACKGROUND package=com.android.systemui class=com.android.systemui.recents.SeparatedRecentsActivity 
        time="03/09/2017 23:02" type=MOVE_TO_FOREGROUND package=android class=com.android.internal.app.ResolverActivity 
        time="03/09/2017 23:02" type=MOVE_TO_BACKGROUND package=android class=com.android.internal.app.ResolverActivity 
        time="03/09/2017 23:02" type=MOVE_TO_FOREGROUND package=com.sec.android.app.launcher class=com.android.launcher2.Launcher 
        time="03/09/2017 23:02" type=MOVE_TO_BACKGROUND package=com.sec.android.app.launcher class=com.android.launcher2.Launcher 
        time="03/09/2017 23:02" type=MOVE_TO_FOREGROUND package=com.arachnoid.sshelper class=com.arachnoid.sshelper.SSHelperActivity 
        time="03/09/2017 23:02" type=MOVE_TO_BACKGROUND package=com.arachnoid.sshelper class=com.arachnoid.sshelper.SSHelperActivity 
        time="03/09/2017 23:02" type=MOVE_TO_FOREGROUND package=com.android.systemui class=com.android.systemui.recents.SeparatedRecentsActivity 
        time="03/09/2017 23:02" type=MOVE_TO_BACKGROUND package=com.android.systemui class=com.android.systemui.recents.SeparatedRecentsActivity 
        time="03/09/2017 23:02" type=MOVE_TO_FOREGROUND package=com.arachnoid.sshelper class=com.arachnoid.sshelper.SSHelperActivity 
        time="03/09/2017 23:02" type=MOVE_TO_BACKGROUND package=com.arachnoid.sshelper class=com.arachnoid.sshelper.SSHelperActivity 
        time="03/09/2017 23:02" type=MOVE_TO_FOREGROUND package=com.android.systemui class=com.android.systemui.recents.SeparatedRecentsActivity 
        time="03/09/2017 23:02" type=MOVE_TO_BACKGROUND package=com.android.systemui class=com.android.systemui.recents.SeparatedRecentsActivity 
        time="03/09/2017 23:02" type=MOVE_TO_FOREGROUND package=android class=com.android.internal.app.ResolverActivity 
        time="03/09/2017 23:02" type=MOVE_TO_BACKGROUND package=android class=com.android.internal.app.ResolverActivity 
        time="03/09/2017 23:02" type=MOVE_TO_FOREGROUND package=com.sec.android.app.launcher class=com.android.launcher2.Launcher 
        time="03/09/2017 23:02" type=MOVE_TO_BACKGROUND package=com.sec.android.app.launcher class=com.android.launcher2.Launcher 
        time="03/09/2017 23:02" type=MOVE_TO_FOREGROUND package=com.arachnoid.sshelper class=com.arachnoid.sshelper.SSHelperActivity 
        time="03/09/2017 23:03" type=MOVE_TO_BACKGROUND package=com.arachnoid.sshelper class=com.arachnoid.sshelper.SSHelperActivity 
        time="03/09/2017 23:03" type=MOVE_TO_FOREGROUND package=com.sec.android.app.launcher class=com.android.launcher2.Launcher 
        time="03/09/2017 23:03" type=MOVE_TO_BACKGROUND package=com.sec.android.app.launcher class=com.android.launcher2.Launcher 
        time="03/09/2017 23:03" type=MOVE_TO_FOREGROUND package=com.arachnoid.sshelper class=com.arachnoid.sshelper.SSHelperActivity 
        time="03/09/2017 23:03" type=MOVE_TO_BACKGROUND package=com.arachnoid.sshelper class=com.arachnoid.sshelper.SSHelperActivity 
        time="03/09/2017 23:03" type=MOVE_TO_FOREGROUND package=com.sec.android.app.launcher class=com.android.launcher2.Launcher 
        time="03/09/2017 23:03" type=MOVE_TO_BACKGROUND package=com.sec.android.app.launcher class=com.android.launcher2.Launcher 
        time="03/09/2017 23:03" type=MOVE_TO_FOREGROUND package=com.arachnoid.sshelper class=com.arachnoid.sshelper.SSHelperActivity 
        time="03/09/2017 23:11" type=CONFIGURATION_CHANGE package=android config=pt-rBR-ldltr-sw411dp-w411dp-h731dp-normal-long-notround-port-560dpi-notouch-keysexposed-nokeys-navhidden-nonav-v23 
        time="03/09/2017 23:11" type=CONFIGURATION_CHANGE package=android config=h707dp-v23 
        time="03/09/2017 23:11" type=CONFIGURATION_CHANGE package=android config=night-v23 
        time="03/09/2017 23:11" type=CONFIGURATION_CHANGE package=android config=finger-v23 
        time="03/09/2017 23:11" type=MOVE_TO_FOREGROUND package=android class=com.android.internal.app.ResolverActivity 
        time="03/09/2017 23:11" type=CONFIGURATION_CHANGE package=android config=v23 
        time="03/09/2017 23:11" type=MOVE_TO_BACKGROUND package=android class=com.android.internal.app.ResolverActivity 
        time="03/09/2017 23:11" type=MOVE_TO_FOREGROUND package=android class=com.android.internal.app.ResolverActivity 
        time="03/09/2017 23:11" type=MOVE_TO_BACKGROUND package=android class=com.android.internal.app.ResolverActivity 
        time="03/09/2017 23:11" type=MOVE_TO_FOREGROUND package=android class=com.android.internal.app.ResolverActivity 
        time="03/09/2017 23:11" type=MOVE_TO_BACKGROUND package=android class=com.android.internal.app.ResolverActivity 
        time="03/09/2017 23:11" type=MOVE_TO_FOREGROUND package=android class=com.android.internal.app.ResolverActivity 
        time="03/09/2017 23:11" type=MOVE_TO_BACKGROUND package=android class=com.android.internal.app.ResolverActivity 
        time="03/09/2017 23:11" type=MOVE_TO_FOREGROUND package=android class=com.android.internal.app.ResolverActivity 
        time="03/09/2017 23:11" type=MOVE_TO_BACKGROUND package=android class=com.android.internal.app.ResolverActivity 
        time="03/09/2017 23:11" type=MOVE_TO_FOREGROUND package=android class=com.android.internal.app.ResolverActivity 
        time="03/09/2017 23:11" type=MOVE_TO_BACKGROUND package=android class=com.android.internal.app.ResolverActivity 
        time="03/09/2017 23:11" type=MOVE_TO_FOREGROUND package=android class=com.android.internal.app.ResolverActivity 
        time="03/09/2017 23:11" type=MOVE_TO_BACKGROUND package=android class=com.android.internal.app.ResolverActivity 
        time="03/09/2017 23:11" type=MOVE_TO_FOREGROUND package=android class=com.android.internal.app.ResolverActivity 
        time="03/09/2017 23:11" type=MOVE_TO_BACKGROUND package=android class=com.android.internal.app.ResolverActivity 
        time="03/09/2017 23:11" type=MOVE_TO_FOREGROUND package=android class=com.android.internal.app.ResolverActivity 
        time="03/09/2017 23:11" type=MOVE_TO_BACKGROUND package=android class=com.android.internal.app.ResolverActivity 
        time="03/09/2017 23:11" type=MOVE_TO_FOREGROUND package=android class=com.android.internal.app.ResolverActivity 
        time="03/09/2017 23:11" type=MOVE_TO_BACKGROUND package=android class=com.android.internal.app.ResolverActivity 
        time="03/09/2017 23:11" type=MOVE_TO_FOREGROUND package=android class=com.android.internal.app.ResolverActivity 
        time="03/09/2017 23:11" type=MOVE_TO_BACKGROUND package=android class=com.android.internal.app.ResolverActivity 
        time="03/09/2017 23:11" type=MOVE_TO_FOREGROUND package=android class=com.android.internal.app.ResolverActivity 
        time="03/09/2017 23:11" type=MOVE_TO_BACKGROUND package=android class=com.android.internal.app.ResolverActivity 
        time="03/09/2017 23:11" type=MOVE_TO_FOREGROUND package=android class=com.android.internal.app.ResolverActivity 
        time="03/09/2017 23:11" type=MOVE_TO_BACKGROUND package=android class=com.android.internal.app.ResolverActivity 
        time="03/09/2017 23:11" type=CONFIGURATION_CHANGE package=android config=mcc724-mnc10-v23 
        time="03/09/2017 23:11" type=MOVE_TO_FOREGROUND package=android class=com.android.internal.app.ResolverActivity 
        time="03/09/2017 23:11" type=MOVE_TO_BACKGROUND package=android class=com.android.internal.app.ResolverActivity 
        time="03/09/2017 23:11" type=MOVE_TO_FOREGROUND package=android class=com.android.internal.app.ResolverActivity 
        time="03/09/2017 23:11" type=MOVE_TO_BACKGROUND package=android class=com.android.internal.app.ResolverActivity 
        time="03/09/2017 23:11" type=MOVE_TO_FOREGROUND package=android class=com.android.internal.app.ResolverActivity 
        time="03/09/2017 23:11" type=MOVE_TO_BACKGROUND package=android class=com.android.internal.app.ResolverActivity 
        time="03/09/2017 23:11" type=MOVE_TO_FOREGROUND package=android class=com.android.internal.app.ResolverActivity 
        time="03/09/2017 23:11" type=MOVE_TO_BACKGROUND package=android class=com.android.internal.app.ResolverActivity 
        time="03/09/2017 23:11" type=MOVE_TO_FOREGROUND package=android class=com.android.internal.app.ResolverActivity 
        time="03/09/2017 23:11" type=MOVE_TO_BACKGROUND package=android class=com.android.internal.app.ResolverActivity 
        time="03/09/2017 23:11" type=MOVE_TO_FOREGROUND package=android class=com.android.internal.app.ResolverActivity 
        time="03/09/2017 23:11" type=MOVE_TO_BACKGROUND package=android class=com.android.internal.app.ResolverActivity 
        time="03/09/2017 23:11" type=MOVE_TO_FOREGROUND package=android class=com.android.internal.app.ResolverActivity 
        time="03/09/2017 23:11" type=MOVE_TO_BACKGROUND package=android class=com.android.internal.app.ResolverActivity 
        time="03/09/2017 23:11" type=MOVE_TO_FOREGROUND package=android class=com.android.internal.app.ResolverActivity 
        time="03/09/2017 23:11" type=MOVE_TO_BACKGROUND package=android class=com.android.internal.app.ResolverActivity 
        time="03/09/2017 23:11" type=MOVE_TO_FOREGROUND package=android class=com.android.internal.app.ResolverActivity 
        time="03/09/2017 23:11" type=MOVE_TO_BACKGROUND package=android class=com.android.internal.app.ResolverActivity 
        time="03/09/2017 23:11" type=MOVE_TO_FOREGROUND package=android class=com.android.internal.app.ResolverActivity 
        time="03/09/2017 23:11" type=MOVE_TO_BACKGROUND package=android class=com.android.internal.app.ResolverActivity 
        time="03/09/2017 23:11" type=MOVE_TO_FOREGROUND package=android class=com.android.internal.app.ResolverActivity 
        time="03/09/2017 23:11" type=MOVE_TO_BACKGROUND package=android class=com.android.internal.app.ResolverActivity 
        time="03/09/2017 23:11" type=MOVE_TO_FOREGROUND package=com.sec.android.app.launcher class=com.android.launcher2.Launcher 
        time="03/09/2017 23:11" type=MOVE_TO_BACKGROUND package=com.sec.android.app.launcher class=com.android.launcher2.Launcher 
        time="03/09/2017 23:11" type=MOVE_TO_FOREGROUND package=com.android.mms class=com.android.mms.ui.ConversationComposer 
        time="03/09/2017 23:11" type=MOVE_TO_BACKGROUND package=com.android.mms class=com.android.mms.ui.ConversationComposer 
        time="03/09/2017 23:11" type=MOVE_TO_FOREGROUND package=com.sec.android.app.launcher class=com.android.launcher2.Launcher 
        time="03/09/2017 23:12" type=MOVE_TO_BACKGROUND package=com.sec.android.app.launcher class=com.android.launcher2.Launcher 
        time="03/09/2017 23:13" type=USER_INTERACTION package=com.google.android.googlequicksearchbox 
        time="03/09/2017 23:13" type=MOVE_TO_FOREGROUND package=com.sec.android.app.launcher class=com.android.launcher2.Launcher 
        time="03/09/2017 23:13" type=USER_INTERACTION package=com.android.mms 
        time="03/09/2017 23:13" type=MOVE_TO_BACKGROUND package=com.sec.android.app.launcher class=com.android.launcher2.Launcher 
        time="03/09/2017 23:13" type=MOVE_TO_FOREGROUND package=com.android.mms class=com.android.mms.ui.ConversationComposer 
        time="03/09/2017 23:13" type=MOVE_TO_BACKGROUND package=com.android.mms class=com.android.mms.ui.ConversationComposer 
        time="03/09/2017 23:13" type=MOVE_TO_FOREGROUND package=com.sec.android.app.launcher class=com.android.launcher2.Launcher 
        time="03/09/2017 23:13" type=MOVE_TO_BACKGROUND package=com.sec.android.app.launcher class=com.android.launcher2.Launcher 
        time="03/09/2017 23:13" type=MOVE_TO_FOREGROUND package=com.arachnoid.sshelper class=com.arachnoid.sshelper.SSHelperActivity 
    In-memory weekly stats
    timeRange="30/08/2017 21:00 - 03/09/2017 23:15" 
      packages
        package=com.samsung.android.provider.filterprovider totalTime="00:00" lastTime="31/12/1969 21:00" lastTimeSystem="02/09/2017 19:20" inactiveTime="7:52:32" 
        package=com.sec.android.providers.mapcon totalTime="00:00" lastTime="31/12/1969 21:00" lastTimeSystem="03/09/2017 23:11" inactiveTime="03:43" 
        package=com.google.android.youtube totalTime="5:38:36" lastTime="03/09/2017 23:02" lastTimeSystem="03/09/2017 23:02" inactiveTime="03:17" 
        package=com.samsung.android.app.cocktailbarservice totalTime="00:00" lastTime="31/12/1969 21:00" lastTimeSystem="03/09/2017 23:13" inactiveTime="02:59" 
        package=com.android.providers.telephony totalTime="00:00" lastTime="31/12/1969 21:00" lastTimeSystem="03/09/2017 23:11" inactiveTime="03:43" 
        package=com.sec.android.providers.iwlansettings totalTime="00:00" lastTime="31/12/1969 21:00" lastTimeSystem="03/09/2017 23:11" inactiveTime="03:43" 
        package=com.google.android.googlequicksearchbox totalTime="09:59" lastTime="03/09/2017 23:13" lastTimeSystem="03/09/2017 23:13" inactiveTime="02:40" 
        package=com.arachnoid.sshelper totalTime="12:40" lastTime="03/09/2017 23:13" lastTimeSystem="03/09/2017 23:13" inactiveTime="02:29" 
        package=com.android.providers.calendar totalTime="00:00" lastTime="31/12/1969 21:00" lastTimeSystem="03/09/2017 20:20" inactiveTime="27:52" 
        package=com.osp.app.signin totalTime="00:00" lastTime="31/12/1969 21:00" lastTimeSystem="02/09/2017 11:51" inactiveTime="9:18:17" 
        package=com.android.providers.media totalTime="00:00" lastTime="31/12/1969 21:00" lastTimeSystem="03/09/2017 23:13" inactiveTime="02:27" 
        package=com.google.android.apps.docs.editors.docs totalTime="00:54" lastTime="03/09/2017 13:47" lastTimeSystem="03/09/2017 13:47" inactiveTime="5:03:00" 
        package=com.samsung.android.provider.shootingmodeprovider totalTime="00:00" lastTime="31/12/1969 21:00" lastTimeSystem="03/09/2017 16:53" inactiveTime="3:12:59" 
        package=com.sec.android.app.wfdbroker totalTime="00:00" lastTime="31/12/1969 21:00" lastTimeSystem="03/09/2017 23:11" inactiveTime="03:40" 
        package=org.simalliance.openmobileapi.service totalTime="00:00" lastTime="31/12/1969 21:00" lastTimeSystem="03/09/2017 23:11" inactiveTime="03:42" 
        package=com.samsung.android.easysetup totalTime="00:00" lastTime="31/12/1969 21:00" lastTimeSystem="03/09/2017 15:41" inactiveTime="4:22:32" 
        package=com.whatsapp totalTime="2:23:59" lastTime="03/09/2017 22:21" lastTimeSystem="03/09/2017 23:12" inactiveTime="03:07" 
        package=com.android.mms.service totalTime="00:00" lastTime="31/12/1969 21:00" lastTimeSystem="01/09/2017 08:52" inactiveTime="13:45:13" 
        package=com.android.providers.downloads totalTime="00:00" lastTime="03/09/2017 15:20" lastTimeSystem="03/09/2017 23:13" inactiveTime="02:27" 
        package=com.samsung.android.qconnect totalTime="00:18" lastTime="03/09/2017 03:15" lastTimeSystem="03/09/2017 23:13" inactiveTime="02:59" 
        package=com.samsung.ucs.agent.boot totalTime="00:00" lastTime="31/12/1969 21:00" lastTimeSystem="03/09/2017 23:11" inactiveTime="03:43" 
        package=com.wsomacp totalTime="00:00" lastTime="31/12/1969 21:00" lastTimeSystem="03/09/2017 23:11" inactiveTime="03:21" 
        package=br.com.gabba.Caixa totalTime="03:59" lastTime="03/09/2017 19:44" lastTimeSystem="03/09/2017 19:44" inactiveTime="1:03:51" 
        package=com.sec.android.Kies totalTime="00:00" lastTime="31/12/1969 21:00" lastTimeSystem="03/09/2017 10:16" inactiveTime="6:00:01" 
        package=com.samsung.faceservice totalTime="00:00" lastTime="31/12/1969 21:00" lastTimeSystem="03/09/2017 23:13" inactiveTime="02:58" 
        package=br.gov.serpro.planejamento.contracheque totalTime="01:15" lastTime="03/09/2017 19:30" lastTimeSystem="03/09/2017 19:30" inactiveTime="1:12:39" 
        package=com.samsung.android.email.provider totalTime="00:33" lastTime="03/09/2017 21:32" lastTimeSystem="03/09/2017 23:12" inactiveTime="03:07" 
        package=com.sec.android.emergencymode.service totalTime="00:00" lastTime="31/12/1969 21:00" lastTimeSystem="03/09/2017 23:12" inactiveTime="03:04" 
        package=com.android.defcontainer totalTime="00:00" lastTime="31/12/1969 21:00" lastTimeSystem="03/09/2017 12:40" inactiveTime="5:46:55" 
        package=com.sec.android.daemonapp totalTime="00:00" lastTime="31/12/1969 21:00" lastTimeSystem="03/09/2017 23:12" inactiveTime="03:19" 
        package=com.samsung.android.slinkcloud totalTime="00:00" lastTime="31/12/1969 21:00" lastTimeSystem="01/09/2017 00:39" inactiveTime="14:36:11" 
        package=com.android.vending totalTime="00:00" lastTime="03/09/2017 10:56" lastTimeSystem="03/09/2017 23:13" inactiveTime="02:58" 
        package=com.microsoft.skydrive totalTime="00:00" lastTime="31/12/1969 21:00" lastTimeSystem="03/09/2017 23:13" inactiveTime="03:03" 
        package=com.sec.android.provider.badge totalTime="00:00" lastTime="31/12/1969 21:00" lastTimeSystem="03/09/2017 23:13" inactiveTime="02:20" 
        package=com.samsung.android.communicationservice totalTime="00:00" lastTime="31/12/1969 21:00" lastTimeSystem="03/09/2017 23:13" inactiveTime="02:55" 
        package=com.samsung.SMT totalTime="00:00" lastTime="01/09/2017 23:54" lastTimeSystem="03/09/2017 18:53" inactiveTime="1:49:21" 
        package=com.samsung.cmh totalTime="00:00" lastTime="31/12/1969 21:00" lastTimeSystem="03/09/2017 23:13" inactiveTime="02:58" 
        package=android totalTime="07:54" lastTime="03/09/2017 23:11" lastTimeSystem="03/09/2017 23:11" inactiveTime="03:28" 
        package=com.android.contacts totalTime="01:33" lastTime="03/09/2017 12:41" lastTimeSystem="03/09/2017 12:41" inactiveTime="5:45:51" 
        package=com.samsung.hs20provider totalTime="00:00" lastTime="31/12/1969 21:00" lastTimeSystem="03/09/2017 23:12" inactiveTime="03:13" 
        package=com.samsung.android.sm.devicesecurity totalTime="00:00" lastTime="31/12/1969 21:00" lastTimeSystem="02/09/2017 18:42" inactiveTime="8:05:08" 
        package=com.ventel.android.radardroid2 totalTime="02:01" lastTime="02/09/2017 00:56" lastTimeSystem="02/09/2017 00:56" inactiveTime="10:08:26" 
        package=br.com.zap.imoveis totalTime="00:00" lastTime="01/09/2017 16:10" lastTimeSystem="01/09/2017 16:10" inactiveTime="12:06:10" 
        package=com.android.mms totalTime="03:21" lastTime="03/09/2017 23:13" lastTimeSystem="03/09/2017 23:13" inactiveTime="02:40" 
        package=com.android.nfc totalTime="00:00" lastTime="31/12/1969 21:00" lastTimeSystem="03/09/2017 23:11" inactiveTime="03:43" 
        package=com.android.stk totalTime="00:00" lastTime="31/12/1969 21:00" lastTimeSystem="01/09/2017 08:52" inactiveTime="13:45:13" 
        package=com.instagram.android totalTime="27:03" lastTime="03/09/2017 20:04" lastTimeSystem="03/09/2017 20:04" inactiveTime="44:00" 
        package=com.samsung.android.app.memo totalTime="00:55" lastTime="02/09/2017 15:47" lastTimeSystem="03/09/2017 12:24" inactiveTime="5:47:26" 
        package=com.pinterest totalTime="00:04" lastTime="03/09/2017 11:40" lastTimeSystem="03/09/2017 11:40" inactiveTime="5:57:55" 
        package=com.google.android.gm totalTime="00:52" lastTime="03/09/2017 13:16" lastTimeSystem="03/09/2017 23:12" inactiveTime="03:07" 
        package=com.android.calendar totalTime="00:55" lastTime="01/09/2017 18:52" lastTimeSystem="01/09/2017 18:52" inactiveTime="11:19:56" 
        package=com.samsung.android.providers.context totalTime="00:00" lastTime="31/12/1969 21:00" lastTimeSystem="03/09/2017 23:11" inactiveTime="03:40" 
        package=com.sec.android.gallery3d totalTime="05:12" lastTime="03/09/2017 16:53" lastTimeSystem="03/09/2017 16:53" inactiveTime="3:12:59" 
        package=pl.moniusoft.showmyip totalTime="00:03" lastTime="02/09/2017 10:41" lastTimeSystem="02/09/2017 10:41" inactiveTime="9:34:35" 
        package=com.google.android.music totalTime="00:00" lastTime="31/12/1969 21:00" lastTimeSystem="03/09/2017 02:14" inactiveTime="7:05:12" 
        package=com.android.printspooler totalTime="00:00" lastTime="31/12/1969 21:00" lastTimeSystem="03/09/2017 23:11" inactiveTime="03:43" 
        package=com.samsung.storyservice totalTime="00:00" lastTime="31/12/1969 21:00" lastTimeSystem="03/09/2017 23:13" inactiveTime="02:58" 
        package=com.android.incallui totalTime="04:20" lastTime="03/09/2017 12:41" lastTimeSystem="03/09/2017 12:41" inactiveTime="5:46:08" 
        package=com.sec.app.samsungprintservice totalTime="00:00" lastTime="31/12/1969 21:00" lastTimeSystem="03/09/2017 03:15" inactiveTime="6:04:21" 
        package=com.estrongs.android.pop totalTime="01:09" lastTime="03/09/2017 18:07" lastTimeSystem="03/09/2017 18:07" inactiveTime="2:19:02" 
        package=com.samsung.android.service.peoplestripe totalTime="00:00" lastTime="31/12/1969 21:00" lastTimeSystem="03/09/2017 23:11" inactiveTime="03:46" 
        package=com.sec.smartcard.manager totalTime="00:00" lastTime="31/12/1969 21:00" lastTimeSystem="03/09/2017 23:11" inactiveTime="03:43" 
        package=com.twitter.android totalTime="00:03" lastTime="03/09/2017 15:23" lastTimeSystem="03/09/2017 15:23" inactiveTime="4:40:19" 
        package=br.com.mobills.consultaplaca totalTime="00:00" lastTime="30/08/2017 21:50" lastTimeSystem="30/08/2017 21:50" inactiveTime="17:37:57" 
        package=br.com.bb.android totalTime="05:34" lastTime="03/09/2017 23:01" lastTimeSystem="03/09/2017 23:01" inactiveTime="03:40" 
        package=com.google.android.apps.maps totalTime="1:27:43" lastTime="03/09/2017 13:50" lastTimeSystem="03/09/2017 13:50" inactiveTime="4:59:03" 
        package=com.google.android.apps.plus totalTime="00:00" lastTime="01/09/2017 23:11" lastTimeSystem="01/09/2017 23:11" inactiveTime="10:17:26" 
        package=com.samsung.android.app.taskedge totalTime="00:00" lastTime="31/12/1969 21:00" lastTimeSystem="03/09/2017 23:12" inactiveTime="03:17" 
        package=org.fdroid.fdroid totalTime="00:00" lastTime="31/08/2017 02:38" lastTimeSystem="31/08/2017 02:38" inactiveTime="16:22:01" 
        package=com.sec.android.inputmethod totalTime="00:00" lastTime="31/12/1969 21:00" lastTimeSystem="03/09/2017 23:04" inactiveTime="01:22" 
        package=com.sec.android.app.clockpackage totalTime="01:35" lastTime="01/09/2017 07:00" lastTimeSystem="01/09/2017 07:00" inactiveTime="14:22:34" 
        package=com.sec.android.app.simsettingmgr totalTime="00:00" lastTime="31/12/1969 21:00" lastTimeSystem="01/09/2017 08:52" inactiveTime="13:45:13" 
        package=com.samsung.android.app.catchfavorites totalTime="00:00" lastTime="31/12/1969 21:00" lastTimeSystem="03/09/2017 23:11" inactiveTime="03:46" 
        package=com.android.server.telecom totalTime="00:00" lastTime="03/09/2017 10:15" lastTimeSystem="03/09/2017 10:15" inactiveTime="6:00:45" 
        package=com.google.android.syncadapters.contacts totalTime="00:00" lastTime="31/12/1969 21:00" lastTimeSystem="03/09/2017 23:12" inactiveTime="03:07" 
        package=com.android.keychain totalTime="00:00" lastTime="31/12/1969 21:00" lastTimeSystem="03/09/2017 23:12" inactiveTime="03:05" 
        package=com.samsung.android.themecenter totalTime="00:00" lastTime="31/12/1969 21:00" lastTimeSystem="03/09/2017 23:12" inactiveTime="03:03" 
        package=com.samsung.android.sm totalTime="00:20" lastTime="03/09/2017 02:21" lastTimeSystem="03/09/2017 02:21" inactiveTime="6:57:56" 
        package=com.google.android.gms totalTime="00:37" lastTime="02/09/2017 14:17" lastTimeSystem="03/09/2017 23:14" inactiveTime="02:01" 
        package=com.google.android.gsf totalTime="00:00" lastTime="31/12/1969 21:00" lastTimeSystem="03/09/2017 23:14" inactiveTime="01:58" 
        package=com.google.android.tts totalTime="00:00" lastTime="01/09/2017 23:54" lastTimeSystem="03/09/2017 00:01" inactiveTime="7:43:07" 
        package=com.google.android.partnersetup totalTime="00:00" lastTime="31/12/1969 21:00" lastTimeSystem="03/09/2017 10:15" inactiveTime="6:00:39" 
        package=com.android.packageinstaller totalTime="00:17" lastTime="02/09/2017 02:11" lastTimeSystem="02/09/2017 02:11" inactiveTime="9:53:29" 
        package=com.sec.spp.push totalTime="00:00" lastTime="31/12/1969 21:00" lastTimeSystem="03/09/2017 19:54" inactiveTime="54:40" 
        package=com.sec.android.app.myfiles totalTime="00:16" lastTime="01/09/2017 00:40" lastTimeSystem="01/09/2017 00:40" inactiveTime="14:35:56" 
        package=com.gopro.smarty totalTime="00:00" lastTime="31/12/1969 21:00" lastTimeSystem="03/09/2017 22:15" inactiveTime="05:05" 
        package=com.samsung.android.allshare.service.fileshare totalTime="00:00" lastTime="31/12/1969 21:00" lastTimeSystem="03/09/2017 03:15" inactiveTime="6:04:19" 
        package=com.sec.android.mimage.photoretouching totalTime="00:31" lastTime="02/09/2017 19:21" lastTimeSystem="02/09/2017 19:21" inactiveTime="7:51:03" 
        package=com.sec.android.app.launcher totalTime="48:01" lastTime="03/09/2017 23:13" lastTimeSystem="03/09/2017 23:13" inactiveTime="02:29" 
        package=com.sec.android.app.sns3 totalTime="00:00" lastTime="31/12/1969 21:00" lastTimeSystem="02/09/2017 19:14" inactiveTime="7:53:17" 
        package=flipboard.boxer.app totalTime="00:28" lastTime="01/09/2017 13:24" lastTimeSystem="01/09/2017 13:24" inactiveTime="12:45:10" 
        package=com.spotify.music totalTime="04:58" lastTime="31/08/2017 00:45" lastTimeSystem="31/08/2017 00:45" inactiveTime="17:03:05" 
        package=com.sec.android.app.sbrowser totalTime="1:41:45" lastTime="03/09/2017 20:01" lastTimeSystem="03/09/2017 20:01" inactiveTime="47:40" 
        package=com.facebook.katana totalTime="1:16:03" lastTime="03/09/2017 20:39" lastTimeSystem="03/09/2017 22:15" inactiveTime="05:05" 
        package=com.samsung.enhanceservice totalTime="00:00" lastTime="31/12/1969 21:00" lastTimeSystem="03/09/2017 23:13" inactiveTime="02:58" 
        package=com.samsung.android.beaconmanager totalTime="00:00" lastTime="31/12/1969 21:00" lastTimeSystem="03/09/2017 23:13" inactiveTime="02:59" 
        package=com.sec.enterprise.mdm.services.simpin totalTime="00:00" lastTime="31/12/1969 21:00" lastTimeSystem="01/09/2017 08:52" inactiveTime="13:45:13" 
        package=com.samsung.ucs.ucspinpad totalTime="00:00" lastTime="31/12/1969 21:00" lastTimeSystem="03/09/2017 23:11" inactiveTime="03:40" 
        package=com.facebook.orca totalTime="02:37" lastTime="03/09/2017 00:39" lastTimeSystem="03/09/2017 20:28" inactiveTime="20:27" 
        package=jackpal.androidterm totalTime="1:27:17" lastTime="03/09/2017 01:46" lastTimeSystem="03/09/2017 01:46" inactiveTime="7:08:21" 
        package=com.sec.android.app.shealth totalTime="00:01" lastTime="01/09/2017 18:14" lastTimeSystem="01/09/2017 18:14" inactiveTime="11:36:06" 
        package=com.sec.phone totalTime="00:00" lastTime="31/12/1969 21:00" lastTimeSystem="03/09/2017 23:12" inactiveTime="03:14" 
        package=br.ceptro.simet.client.android totalTime="02:26" lastTime="02/09/2017 15:44" lastTimeSystem="02/09/2017 15:44" inactiveTime="8:10:43" 
        package=com.google.android.apps.translate totalTime="01:06" lastTime="01/09/2017 08:41" lastTimeSystem="01/09/2017 08:41" inactiveTime="13:56:22" 
        package=com.samsung.android.app.scrollcapture totalTime="00:04" lastTime="02/09/2017 19:20" lastTimeSystem="02/09/2017 19:20" inactiveTime="7:52:35" 
        package=com.samsung.android.scloud totalTime="00:00" lastTime="31/12/1969 21:00" lastTimeSystem="03/09/2017 23:12" inactiveTime="03:07" 
        package=com.samsung.android.spayfw totalTime="00:00" lastTime="31/12/1969 21:00" lastTimeSystem="03/09/2017 23:15" inactiveTime="00:49" 
        package=cx.ring totalTime="00:40" lastTime="03/09/2017 16:53" lastTimeSystem="03/09/2017 16:53" inactiveTime="3:12:50" 
        package=com.linkedin.android totalTime="08:04" lastTime="02/09/2017 12:28" lastTimeSystem="02/09/2017 12:28" inactiveTime="9:14:13" 
        package=com.android.settings totalTime="20:02" lastTime="03/09/2017 12:00" lastTimeSystem="03/09/2017 12:00" inactiveTime="5:55:15" 
        package=com.samsung.android.spay totalTime="00:05" lastTime="02/09/2017 11:51" lastTimeSystem="03/09/2017 23:12" inactiveTime="03:07" 
        package=com.sec.android.app.bluetoothtest totalTime="00:00" lastTime="31/12/1969 21:00" lastTimeSystem="01/09/2017 08:52" inactiveTime="13:45:13" 
        package=com.samsung.android.sm.policy totalTime="00:00" lastTime="31/12/1969 21:00" lastTimeSystem="03/09/2017 23:12" inactiveTime="03:14" 
        package=com.wssnps totalTime="00:00" lastTime="31/12/1969 21:00" lastTimeSystem="03/09/2017 23:12" inactiveTime="03:08" 
        package=com.sec.android.app.snsimagecache totalTime="00:00" lastTime="31/12/1969 21:00" lastTimeSystem="03/09/2017 12:41" inactiveTime="5:45:54" 
        package=com.movile.android.appsvivo totalTime="00:04" lastTime="01/09/2017 13:36" lastTimeSystem="01/09/2017 13:36" inactiveTime="12:41:11" 
        package=eu.chainfire.supersu totalTime="00:04" lastTime="02/09/2017 10:42" lastTimeSystem="03/09/2017 23:14" inactiveTime="01:17" 
        package=com.samsung.dcmservice totalTime="00:00" lastTime="31/12/1969 21:00" lastTimeSystem="03/09/2017 23:13" inactiveTime="02:58" 
        package=com.android.phone totalTime="00:00" lastTime="31/12/1969 21:00" lastTimeSystem="03/09/2017 23:11" inactiveTime="03:43" 
        package=com.android.providers.userdictionary totalTime="00:00" lastTime="31/12/1969 21:00" lastTimeSystem="03/09/2017 23:13" inactiveTime="02:54" 
        package=com.samsung.android.sm.provider totalTime="00:00" lastTime="31/12/1969 21:00" lastTimeSystem="03/09/2017 23:12" inactiveTime="03:15" 
        package=com.android.systemui totalTime="04:30" lastTime="03/09/2017 23:02" lastTimeSystem="03/09/2017 23:11" inactiveTime="03:46" 
        package=com.facebook.appmanager totalTime="00:00" lastTime="31/12/1969 21:00" lastTimeSystem="03/09/2017 12:02" inactiveTime="5:54:11" 
        package=com.sec.android.app.SamsungContentsAgent totalTime="00:00" lastTime="31/12/1969 21:00" lastTimeSystem="03/09/2017 23:11" inactiveTime="03:40" 
        package=com.samsung.android.allshare.service.mediashare totalTime="00:00" lastTime="31/12/1969 21:00" lastTimeSystem="03/09/2017 16:53" inactiveTime="3:13:29" 
        package=com.sec.android.provider.emergencymode totalTime="00:00" lastTime="31/12/1969 21:00" lastTimeSystem="03/09/2017 23:11" inactiveTime="03:46" 
        package=com.samsung.android.fingerprint.service totalTime="00:00" lastTime="31/12/1969 21:00" lastTimeSystem="03/09/2017 23:11" inactiveTime="03:32" 
        package=com.sec.android.app.camera totalTime="01:09" lastTime="03/09/2017 16:53" lastTimeSystem="03/09/2017 16:53" inactiveTime="3:12:58" 
        package=com.google.android.apps.magazines totalTime="00:07" lastTime="03/09/2017 16:20" lastTimeSystem="03/09/2017 16:20" inactiveTime="3:46:11" 
        package=com.android.bluetooth totalTime="00:00" lastTime="31/12/1969 21:00" lastTimeSystem="03/09/2017 23:11" inactiveTime="03:40" 
        package=com.android.providers.contacts totalTime="00:00" lastTime="31/12/1969 21:00" lastTimeSystem="03/09/2017 23:13" inactiveTime="02:54" 
        package=com.samsung.ipservice totalTime="00:00" lastTime="31/12/1969 21:00" lastTimeSystem="03/09/2017 23:13" inactiveTime="02:58" 
        package=com.samsung.sec.android.application.csc totalTime="00:00" lastTime="31/12/1969 21:00" lastTimeSystem="01/09/2017 08:52" inactiveTime="13:45:13" 
        package=com.android.captiveportallogin totalTime="03:03" lastTime="03/09/2017 01:35" lastTimeSystem="03/09/2017 01:35" inactiveTime="7:19:09" 
        package=com.samsung.android.coreapps totalTime="00:00" lastTime="31/12/1969 21:00" lastTimeSystem="03/09/2017 23:13" inactiveTime="03:01" 
        package=com.samsung.android.video totalTime="01:34" lastTime="03/09/2017 02:26" lastTimeSystem="03/09/2017 02:26" inactiveTime="6:53:15" 
      configurations
        config=pt-rBR-ldltr-sw411dp-w411dp-h707dp-normal-long-notround-port-night-560dpi-notouch-keysexposed-nokeys-navhidden-nonav-v23 totalTime="00:00" lastTime="03/09/2017 10:14" count=1 
        config=pt-rBR-ldltr-sw411dp-w411dp-h707dp-normal-long-notround-port-night-560dpi-notouch-keysexposed-nokeys-navhidden-nonav-v23 totalTime="00:00" lastTime="03/09/2017 23:11" count=1 
        config=pt-rBR-ldltr-sw411dp-w411dp-h707dp-normal-long-notround-port-560dpi-notouch-keysexposed-nokeys-navhidden-nonav-v23 totalTime="00:00" lastTime="03/09/2017 10:14" count=1 
        config=pt-rBR-ldltr-sw411dp-w411dp-h707dp-normal-long-notround-port-560dpi-notouch-keysexposed-nokeys-navhidden-nonav-v23 totalTime="00:00" lastTime="03/09/2017 23:11" count=1 
        config=pt-rBR-ldltr-sw411dp-w411dp-h731dp-normal-long-notround-port-560dpi-notouch-keysexposed-nokeys-navhidden-nonav-v23 totalTime="00:00" lastTime="03/09/2017 10:14" count=1 
        config=pt-rBR-ldltr-sw411dp-w411dp-h731dp-normal-long-notround-port-560dpi-notouch-keysexposed-nokeys-navhidden-nonav-v23 totalTime="00:00" lastTime="03/09/2017 23:11" count=1 
        config=mcc724-mnc10-pt-rBR-ldltr-sw411dp-w731dp-h387dp-normal-long-notround-land-night-560dpi-finger-keysexposed-nokeys-navhidden-nonav-v23 totalTime="1:11:24" lastTime="03/09/2017 19:55" count=13 
        config=pt-rBR-ldltr-sw411dp-w411dp-h707dp-normal-long-notround-port-night-560dpi-finger-keysexposed-nokeys-navhidden-nonav-v23 totalTime="00:10" lastTime="03/09/2017 10:15" count=1 
        config=pt-rBR-ldltr-sw411dp-w411dp-h707dp-normal-long-notround-port-night-560dpi-finger-keysexposed-nokeys-navhidden-nonav-v23 totalTime="00:05" lastTime="03/09/2017 23:11" count=1 
        config=pt-rBR-ldltr-sw411dp-w411dp-h707dp-normal-long-notround-port-night-560dpi-finger-keysexposed-nokeys-navhidden-nonav-v23 totalTime="00:10" lastTime="03/09/2017 23:11" count=1 
        config=mcc724-mnc10-pt-rBR-ldltr-sw411dp-w411dp-h707dp-normal-long-notround-port-night-560dpi-finger-keysexposed-nokeys-navhidden-nonav-v23 totalTime="11:44:56" lastTime="03/09/2017 23:11" count=14 
        config=mcc724-mnc10-pt-rBR-ldltr-sw411dp-w411dp-h707dp-normal-long-notround-port-night-560dpi-finger-keysexposed-nokeys-navhidden-nonav-v23 totalTime="00:00" lastTime="03/09/2017 23:11" count=1 
        config=pt-rBR-ldltr-sw411dp-w411dp-h707dp-normal-long-notround-port-560dpi-finger-keysexposed-nokeys-navhidden-nonav-v23 totalTime="00:00" lastTime="01/09/2017 09:19" count=1 
      events
    In-memory monthly stats
    timeRange="21/08/2017 21:00 - 03/09/2017 23:15" 
      packages
        package=com.samsung.android.provider.filterprovider totalTime="00:00" lastTime="31/12/1969 21:00" lastTimeSystem="02/09/2017 19:20" inactiveTime="7:52:32" 
        package=com.sec.android.providers.mapcon totalTime="00:00" lastTime="31/12/1969 21:00" lastTimeSystem="03/09/2017 23:11" inactiveTime="03:43" 
        package=com.google.android.youtube totalTime="20:55:09" lastTime="03/09/2017 23:02" lastTimeSystem="03/09/2017 23:02" inactiveTime="03:17" 
        package=stericson.busybox totalTime="07:41" lastTime="30/08/2017 16:43" lastTimeSystem="30/08/2017 16:43" inactiveTime="18:47:22" 
        package=com.sec.android.app.chromecustomizations totalTime="00:00" lastTime="31/12/1969 21:00" lastTimeSystem="24/08/2017 16:54" inactiveTime="44:18:01" 
        package=com.samsung.android.app.cocktailbarservice totalTime="00:00" lastTime="31/12/1969 21:00" lastTimeSystem="03/09/2017 23:13" inactiveTime="02:59" 
        package=com.android.providers.telephony totalTime="00:00" lastTime="31/12/1969 21:00" lastTimeSystem="03/09/2017 23:11" inactiveTime="03:43" 
        package=com.sec.android.providers.iwlansettings totalTime="00:00" lastTime="31/12/1969 21:00" lastTimeSystem="03/09/2017 23:11" inactiveTime="03:43" 
        package=com.google.android.googlequicksearchbox totalTime="09:59" lastTime="03/09/2017 23:13" lastTimeSystem="03/09/2017 23:13" inactiveTime="02:40" 
        package=com.arachnoid.sshelper totalTime="12:40" lastTime="03/09/2017 23:13" lastTimeSystem="03/09/2017 23:13" inactiveTime="02:29" 
        package=com.android.providers.calendar totalTime="00:00" lastTime="31/12/1969 21:00" lastTimeSystem="03/09/2017 20:20" inactiveTime="27:52" 
        package=com.osp.app.signin totalTime="00:00" lastTime="31/12/1969 21:00" lastTimeSystem="02/09/2017 11:51" inactiveTime="9:18:17" 
        package=org.telegram.messenger totalTime="00:00" lastTime="23/08/2017 23:16" lastTimeSystem="23/08/2017 23:16" inactiveTime="46:52:45" 
        package=com.android.providers.media totalTime="00:00" lastTime="31/12/1969 21:00" lastTimeSystem="03/09/2017 23:13" inactiveTime="02:27" 
        package=com.google.android.apps.docs.editors.docs totalTime="01:18" lastTime="03/09/2017 13:47" lastTimeSystem="03/09/2017 13:47" inactiveTime="5:03:00" 
        package=com.samsung.android.provider.shootingmodeprovider totalTime="00:00" lastTime="31/12/1969 21:00" lastTimeSystem="03/09/2017 16:53" inactiveTime="3:12:59" 
        package=com.sec.android.app.wfdbroker totalTime="00:00" lastTime="31/12/1969 21:00" lastTimeSystem="03/09/2017 23:11" inactiveTime="03:40" 
        package=it.colucciweb.sstpvpnclient totalTime="00:00" lastTime="30/08/2017 16:43" lastTimeSystem="30/08/2017 16:43" inactiveTime="18:47:24" 
        package=gpsplus.rtkgps totalTime="01:53" lastTime="25/08/2017 14:50" lastTimeSystem="25/08/2017 14:50" inactiveTime="40:04:06" 
        package=org.simalliance.openmobileapi.service totalTime="00:00" lastTime="31/12/1969 21:00" lastTimeSystem="03/09/2017 23:11" inactiveTime="03:42" 
        package=com.samsung.android.easysetup totalTime="00:00" lastTime="31/12/1969 21:00" lastTimeSystem="03/09/2017 15:41" inactiveTime="4:22:32" 
        package=com.whatsapp totalTime="11:05:50" lastTime="03/09/2017 22:21" lastTimeSystem="03/09/2017 23:12" inactiveTime="03:07" 
        package=com.android.mms.service totalTime="00:00" lastTime="31/12/1969 21:00" lastTimeSystem="01/09/2017 08:52" inactiveTime="13:45:13" 
        package=com.android.providers.downloads totalTime="00:00" lastTime="03/09/2017 15:20" lastTimeSystem="03/09/2017 23:13" inactiveTime="02:27" 
        package=com.samsung.android.qconnect totalTime="00:18" lastTime="03/09/2017 03:15" lastTimeSystem="03/09/2017 23:13" inactiveTime="02:59" 
        package=com.samsung.ucs.agent.boot totalTime="00:00" lastTime="31/12/1969 21:00" lastTimeSystem="03/09/2017 23:11" inactiveTime="03:43" 
        package=com.wsomacp totalTime="00:00" lastTime="31/12/1969 21:00" lastTimeSystem="03/09/2017 23:11" inactiveTime="03:21" 
        package=br.com.gabba.Caixa totalTime="06:13" lastTime="03/09/2017 19:44" lastTimeSystem="03/09/2017 19:44" inactiveTime="1:03:51" 
        package=com.sec.android.Kies totalTime="00:00" lastTime="31/12/1969 21:00" lastTimeSystem="03/09/2017 10:16" inactiveTime="6:00:01" 
        package=com.samsung.faceservice totalTime="00:00" lastTime="31/12/1969 21:00" lastTimeSystem="03/09/2017 23:13" inactiveTime="02:58" 
        package=br.gov.serpro.planejamento.contracheque totalTime="02:02" lastTime="03/09/2017 19:30" lastTimeSystem="03/09/2017 19:30" inactiveTime="1:12:39" 
        package=com.sec.android.app.easylauncher totalTime="00:03" lastTime="24/08/2017 21:24" lastTimeSystem="24/08/2017 21:24" inactiveTime="43:42:19" 
        package=com.sec.android.widgetapp.easymodecontactswidget totalTime="00:00" lastTime="31/12/1969 21:00" lastTimeSystem="25/08/2017 18:24" inactiveTime="38:51:50" 
        package=com.samsung.android.email.provider totalTime="00:33" lastTime="03/09/2017 21:32" lastTimeSystem="03/09/2017 23:12" inactiveTime="03:07" 
        package=com.samsung.android.MtpApplication totalTime="00:32" lastTime="25/08/2017 14:28" lastTimeSystem="25/08/2017 14:28" inactiveTime="40:20:29" 
        package=com.sec.android.app.samsungapps totalTime="00:05" lastTime="29/08/2017 02:46" lastTimeSystem="29/08/2017 02:46" inactiveTime="23:49:30" 
        package=com.sec.android.emergencymode.service totalTime="00:00" lastTime="31/12/1969 21:00" lastTimeSystem="03/09/2017 23:12" inactiveTime="03:04" 
        package=com.android.defcontainer totalTime="00:00" lastTime="31/12/1969 21:00" lastTimeSystem="03/09/2017 12:40" inactiveTime="5:46:55" 
        package=com.sec.android.daemonapp totalTime="00:00" lastTime="31/12/1969 21:00" lastTimeSystem="03/09/2017 23:12" inactiveTime="03:19" 
        package=com.samsung.android.slinkcloud totalTime="00:00" lastTime="31/12/1969 21:00" lastTimeSystem="01/09/2017 00:39" inactiveTime="14:36:11" 
        package=com.android.vending totalTime="01:43" lastTime="03/09/2017 10:56" lastTimeSystem="03/09/2017 23:13" inactiveTime="02:58" 
        package=com.microsoft.skydrive totalTime="00:00" lastTime="31/12/1969 21:00" lastTimeSystem="03/09/2017 23:13" inactiveTime="03:03" 
        package=com.sec.android.provider.badge totalTime="00:00" lastTime="31/12/1969 21:00" lastTimeSystem="03/09/2017 23:13" inactiveTime="02:20" 
        package=com.lefebure.ntripclient totalTime="05:40" lastTime="28/08/2017 19:34" lastTimeSystem="28/08/2017 19:34" inactiveTime="25:25:55" 
        package=com.samsung.android.communicationservice totalTime="00:00" lastTime="31/12/1969 21:00" lastTimeSystem="03/09/2017 23:13" inactiveTime="02:55" 
        package=com.samsung.SMT totalTime="00:00" lastTime="01/09/2017 23:54" lastTimeSystem="03/09/2017 18:53" inactiveTime="1:49:21" 
        package=com.samsung.cmh totalTime="00:00" lastTime="31/12/1969 21:00" lastTimeSystem="03/09/2017 23:13" inactiveTime="02:58" 
        package=android totalTime="21:29" lastTime="03/09/2017 23:11" lastTimeSystem="03/09/2017 23:11" inactiveTime="03:28" 
        package=com.android.contacts totalTime="17:03" lastTime="03/09/2017 12:41" lastTimeSystem="03/09/2017 12:41" inactiveTime="5:45:51" 
        package=com.samsung.hs20provider totalTime="00:00" lastTime="31/12/1969 21:00" lastTimeSystem="03/09/2017 23:12" inactiveTime="03:13" 
        package=com.samsung.android.sm.devicesecurity totalTime="00:00" lastTime="31/12/1969 21:00" lastTimeSystem="02/09/2017 18:42" inactiveTime="8:05:08" 
        package=com.gameloft.android.GloftKLMF totalTime="00:00" lastTime="31/12/1969 21:00" lastTimeSystem="29/08/2017 22:20" inactiveTime="20:49:49" 
        package=com.gameloft.android.GloftSMIM totalTime="00:00" lastTime="31/12/1969 21:00" lastTimeSystem="29/08/2017 22:20" inactiveTime="20:49:50" 
        package=com.ventel.android.radardroid2 totalTime="02:01" lastTime="02/09/2017 00:56" lastTimeSystem="02/09/2017 00:56" inactiveTime="10:08:26" 
        package=br.com.zap.imoveis totalTime="00:00" lastTime="01/09/2017 16:10" lastTimeSystem="01/09/2017 16:10" inactiveTime="12:06:10" 
        package=com.android.mms totalTime="04:37" lastTime="03/09/2017 23:13" lastTimeSystem="03/09/2017 23:13" inactiveTime="02:40" 
        package=com.android.nfc totalTime="00:00" lastTime="31/12/1969 21:00" lastTimeSystem="03/09/2017 23:11" inactiveTime="03:43" 
        package=com.android.stk totalTime="00:04" lastTime="23/08/2017 19:51" lastTimeSystem="01/09/2017 08:52" inactiveTime="13:45:13" 
        package=com.instagram.android totalTime="56:59" lastTime="03/09/2017 20:04" lastTimeSystem="03/09/2017 20:04" inactiveTime="44:00" 
        package=com.waze totalTime="04:00" lastTime="24/08/2017 01:49" lastTimeSystem="24/08/2017 01:49" inactiveTime="46:45:56" 
        package=com.samsung.android.app.memo totalTime="14:39" lastTime="02/09/2017 15:47" lastTimeSystem="03/09/2017 12:24" inactiveTime="5:47:26" 
        package=com.studiobluelime.ecommerceapp totalTime="00:56" lastTime="27/08/2017 14:11" lastTimeSystem="27/08/2017 14:11" inactiveTime="31:55:40" 
        package=com.pinterest totalTime="00:04" lastTime="03/09/2017 11:40" lastTimeSystem="03/09/2017 11:40" inactiveTime="5:57:55" 
        package=org.pocketworkstation.pckeyboard totalTime="01:03" lastTime="23/08/2017 10:25" lastTimeSystem="23/08/2017 10:25" inactiveTime="49:23:25" 
        package=chat.tox.antox totalTime="11:37" lastTime="22/08/2017 17:34" lastTimeSystem="22/08/2017 17:34" inactiveTime="52:39:51" 
        package=com.google.android.gm totalTime="11:26" lastTime="03/09/2017 13:16" lastTimeSystem="03/09/2017 23:12" inactiveTime="03:07" 
        package=com.android.calendar totalTime="00:55" lastTime="01/09/2017 18:52" lastTimeSystem="01/09/2017 18:52" inactiveTime="11:19:56" 
        package=com.google.zxing.client.android totalTime="00:02" lastTime="22/08/2017 15:07" lastTimeSystem="22/08/2017 15:07" inactiveTime="53:10:13" 
        package=com.samsung.android.providers.context totalTime="00:00" lastTime="31/12/1969 21:00" lastTimeSystem="03/09/2017 23:11" inactiveTime="03:40" 
        package=com.sec.android.usermanual totalTime="00:00" lastTime="28/08/2017 15:00" lastTimeSystem="28/08/2017 15:00" inactiveTime="28:21:29" 
        package=com.sec.android.gallery3d totalTime="11:15" lastTime="03/09/2017 16:53" lastTimeSystem="03/09/2017 16:53" inactiveTime="3:12:59" 
        package=pl.moniusoft.showmyip totalTime="00:13" lastTime="02/09/2017 10:41" lastTimeSystem="02/09/2017 10:41" inactiveTime="9:34:35" 
        package=com.google.android.music totalTime="00:00" lastTime="31/12/1969 21:00" lastTimeSystem="03/09/2017 02:14" inactiveTime="7:05:12" 
        package=com.android.printspooler totalTime="00:00" lastTime="31/12/1969 21:00" lastTimeSystem="03/09/2017 23:11" inactiveTime="03:43" 
        package=com.samsung.storyservice totalTime="00:00" lastTime="31/12/1969 21:00" lastTimeSystem="03/09/2017 23:13" inactiveTime="02:58" 
        package=com.sec.android.app.music totalTime="00:02" lastTime="24/08/2017 21:25" lastTimeSystem="24/08/2017 21:25" inactiveTime="43:42:17" 
        package=com.ingresso.cinemas totalTime="01:14" lastTime="27/08/2017 15:13" lastTimeSystem="27/08/2017 15:13" inactiveTime="31:11:42" 
        package=com.android.incallui totalTime="22:01" lastTime="03/09/2017 12:41" lastTimeSystem="03/09/2017 12:41" inactiveTime="5:46:08" 
        package=com.sec.app.samsungprintservice totalTime="00:00" lastTime="31/12/1969 21:00" lastTimeSystem="03/09/2017 03:15" inactiveTime="6:04:21" 
        package=com.estrongs.android.pop totalTime="03:18" lastTime="03/09/2017 18:07" lastTimeSystem="03/09/2017 18:07" inactiveTime="2:19:02" 
        package=com.samsung.android.service.peoplestripe totalTime="00:00" lastTime="31/12/1969 21:00" lastTimeSystem="03/09/2017 23:11" inactiveTime="03:46" 
        package=com.sec.smartcard.manager totalTime="00:00" lastTime="31/12/1969 21:00" lastTimeSystem="03/09/2017 23:11" inactiveTime="03:43" 
        package=com.dropbox.android totalTime="00:01" lastTime="30/08/2017 15:06" lastTimeSystem="30/08/2017 15:06" inactiveTime="18:53:52" 
        package=com.twitter.android totalTime="00:15" lastTime="03/09/2017 15:23" lastTimeSystem="03/09/2017 15:23" inactiveTime="4:40:19" 
        package=br.com.mobills.consultaplaca totalTime="00:00" lastTime="30/08/2017 21:50" lastTimeSystem="30/08/2017 21:50" inactiveTime="17:37:57" 
        package=br.com.bb.android totalTime="07:11" lastTime="03/09/2017 23:01" lastTimeSystem="03/09/2017 23:01" inactiveTime="03:40" 
        package=com.google.android.apps.docs totalTime="00:00" lastTime="31/12/1969 21:00" lastTimeSystem="30/08/2017 16:04" inactiveTime="18:48:41" 
        package=com.google.android.apps.maps totalTime="2:16:48" lastTime="03/09/2017 13:50" lastTimeSystem="03/09/2017 13:50" inactiveTime="4:59:03" 
        package=com.google.android.apps.plus totalTime="00:02" lastTime="01/09/2017 23:11" lastTimeSystem="01/09/2017 23:11" inactiveTime="10:17:26" 
        package=com.samsung.android.weather totalTime="00:00" lastTime="24/08/2017 21:22" lastTimeSystem="24/08/2017 21:22" inactiveTime="43:43:47" 
        package=com.samsung.android.app.taskedge totalTime="00:00" lastTime="31/12/1969 21:00" lastTimeSystem="03/09/2017 23:12" inactiveTime="03:17" 
        package=org.fdroid.fdroid totalTime="00:00" lastTime="31/08/2017 02:38" lastTimeSystem="31/08/2017 02:38" inactiveTime="16:22:01" 
        package=com.sec.android.inputmethod totalTime="00:01" lastTime="25/08/2017 19:36" lastTimeSystem="03/09/2017 23:04" inactiveTime="01:22" 
        package=com.sec.android.app.clockpackage totalTime="16:44" lastTime="01/09/2017 07:00" lastTimeSystem="01/09/2017 07:00" inactiveTime="14:22:34" 
        package=com.sec.android.app.simsettingmgr totalTime="00:00" lastTime="31/12/1969 21:00" lastTimeSystem="01/09/2017 08:52" inactiveTime="13:45:13" 
        package=com.samsung.android.app.catchfavorites totalTime="00:00" lastTime="31/12/1969 21:00" lastTimeSystem="03/09/2017 23:11" inactiveTime="03:46" 
        package=com.android.server.telecom totalTime="00:00" lastTime="03/09/2017 10:15" lastTimeSystem="03/09/2017 10:15" inactiveTime="6:00:45" 
        package=com.google.android.syncadapters.contacts totalTime="00:00" lastTime="31/12/1969 21:00" lastTimeSystem="03/09/2017 23:12" inactiveTime="03:07" 
        package=com.android.keychain totalTime="00:00" lastTime="31/12/1969 21:00" lastTimeSystem="03/09/2017 23:12" inactiveTime="03:05" 
        package=com.android.chrome totalTime="00:35" lastTime="24/08/2017 16:54" lastTimeSystem="24/08/2017 16:54" inactiveTime="44:17:38" 
        package=com.samsung.android.themecenter totalTime="00:00" lastTime="31/12/1969 21:00" lastTimeSystem="03/09/2017 23:12" inactiveTime="03:03" 
        package=com.samsung.android.sm totalTime="00:20" lastTime="03/09/2017 02:21" lastTimeSystem="03/09/2017 02:21" inactiveTime="6:57:56" 
        package=com.google.android.gms totalTime="02:35" lastTime="02/09/2017 14:17" lastTimeSystem="03/09/2017 23:14" inactiveTime="02:01" 
        package=com.google.android.gsf totalTime="00:00" lastTime="31/12/1969 21:00" lastTimeSystem="03/09/2017 23:14" inactiveTime="01:58" 
        package=com.google.android.tts totalTime="00:00" lastTime="01/09/2017 23:54" lastTimeSystem="03/09/2017 00:01" inactiveTime="7:43:07" 
        package=com.google.android.partnersetup totalTime="00:00" lastTime="31/12/1969 21:00" lastTimeSystem="03/09/2017 10:15" inactiveTime="6:00:39" 
        package=com.android.packageinstaller totalTime="00:32" lastTime="02/09/2017 02:11" lastTimeSystem="02/09/2017 02:11" inactiveTime="9:53:29" 
        package=com.sec.spp.push totalTime="00:00" lastTime="26/08/2017 20:19" lastTimeSystem="03/09/2017 19:54" inactiveTime="54:40" 
        package=com.sec.android.app.myfiles totalTime="06:37" lastTime="01/09/2017 00:40" lastTimeSystem="01/09/2017 00:40" inactiveTime="14:35:56" 
        package=com.gopro.smarty totalTime="00:00" lastTime="31/12/1969 21:00" lastTimeSystem="03/09/2017 22:15" inactiveTime="05:05" 
        package=com.samsung.android.allshare.service.fileshare totalTime="00:00" lastTime="31/12/1969 21:00" lastTimeSystem="03/09/2017 03:15" inactiveTime="6:04:19" 
        package=com.sec.android.mimage.photoretouching totalTime="00:58" lastTime="02/09/2017 19:21" lastTimeSystem="02/09/2017 19:21" inactiveTime="7:51:03" 
        package=com.sec.android.app.launcher totalTime="2:57:05" lastTime="03/09/2017 23:13" lastTimeSystem="03/09/2017 23:13" inactiveTime="02:29" 
        package=com.sec.android.app.sns3 totalTime="00:00" lastTime="31/12/1969 21:00" lastTimeSystem="02/09/2017 19:14" inactiveTime="7:53:17" 
        package=flipboard.boxer.app totalTime="00:32" lastTime="01/09/2017 13:24" lastTimeSystem="01/09/2017 13:24" inactiveTime="12:45:10" 
        package=com.spotify.music totalTime="04:58" lastTime="31/08/2017 00:45" lastTimeSystem="31/08/2017 00:45" inactiveTime="17:03:05" 
        package=com.sec.android.app.sbrowser totalTime="9:42:07" lastTime="03/09/2017 20:01" lastTimeSystem="03/09/2017 20:01" inactiveTime="47:40" 
        package=com.facebook.katana totalTime="8:19:01" lastTime="03/09/2017 20:39" lastTimeSystem="03/09/2017 22:15" inactiveTime="05:05" 
        package=com.samsung.enhanceservice totalTime="00:00" lastTime="31/12/1969 21:00" lastTimeSystem="03/09/2017 23:13" inactiveTime="02:58" 
        package=com.gameloft.android.LATAM.GloftCRSM totalTime="00:02" lastTime="29/08/2017 22:20" lastTimeSystem="29/08/2017 22:20" inactiveTime="20:49:48" 
        package=com.android.providers.partnerbookmarks totalTime="00:00" lastTime="31/12/1969 21:00" lastTimeSystem="24/08/2017 16:54" inactiveTime="44:18:15" 
        package=com.samsung.android.beaconmanager totalTime="00:00" lastTime="31/12/1969 21:00" lastTimeSystem="03/09/2017 23:13" inactiveTime="02:59" 
        package=com.airbnb.android totalTime="00:11" lastTime="30/08/2017 00:44" lastTimeSystem="30/08/2017 00:44" inactiveTime="20:11:21" 
        package=com.sec.enterprise.mdm.services.simpin totalTime="00:00" lastTime="31/12/1969 21:00" lastTimeSystem="01/09/2017 08:52" inactiveTime="13:45:13" 
        package=com.samsung.ucs.ucspinpad totalTime="00:00" lastTime="31/12/1969 21:00" lastTimeSystem="03/09/2017 23:11" inactiveTime="03:40" 
        package=com.facebook.orca totalTime="03:38" lastTime="03/09/2017 00:39" lastTimeSystem="03/09/2017 20:28" inactiveTime="20:27" 
        package=org.mozilla.firefox totalTime="02:09" lastTime="30/08/2017 07:16" lastTimeSystem="30/08/2017 07:16" inactiveTime="19:56:00" 
        package=jackpal.androidterm totalTime="2:55:54" lastTime="03/09/2017 01:46" lastTimeSystem="03/09/2017 01:46" inactiveTime="7:08:21" 
        package=com.sec.android.app.shealth totalTime="00:01" lastTime="01/09/2017 18:14" lastTimeSystem="01/09/2017 18:14" inactiveTime="11:36:06" 
        package=com.sec.phone totalTime="00:00" lastTime="31/12/1969 21:00" lastTimeSystem="03/09/2017 23:12" inactiveTime="03:14" 
        package=br.ceptro.simet.client.android totalTime="02:26" lastTime="02/09/2017 15:44" lastTimeSystem="02/09/2017 15:44" inactiveTime="8:10:43" 
        package=com.google.android.apps.translate totalTime="02:45" lastTime="01/09/2017 08:41" lastTimeSystem="01/09/2017 08:41" inactiveTime="13:56:22" 
        package=com.samsung.android.app.scrollcapture totalTime="00:26" lastTime="02/09/2017 19:20" lastTimeSystem="02/09/2017 19:20" inactiveTime="7:52:35" 
        package=com.adobe.reader totalTime="03:01" lastTime="28/08/2017 15:00" lastTimeSystem="28/08/2017 15:00" inactiveTime="28:21:27" 
        package=com.samsung.android.scloud totalTime="00:00" lastTime="31/12/1969 21:00" lastTimeSystem="03/09/2017 23:12" inactiveTime="03:07" 
        package=com.samsung.android.spayfw totalTime="00:00" lastTime="31/12/1969 21:00" lastTimeSystem="03/09/2017 23:15" inactiveTime="00:49" 
        package=cx.ring totalTime="04:50" lastTime="03/09/2017 16:53" lastTimeSystem="03/09/2017 16:53" inactiveTime="3:12:50" 
        package=com.linkedin.android totalTime="10:40" lastTime="02/09/2017 12:28" lastTimeSystem="02/09/2017 12:28" inactiveTime="9:14:13" 
        package=com.android.settings totalTime="28:13" lastTime="03/09/2017 12:00" lastTimeSystem="03/09/2017 12:00" inactiveTime="5:55:15" 
        package=com.samsung.android.spay totalTime="00:05" lastTime="02/09/2017 11:51" lastTimeSystem="03/09/2017 23:12" inactiveTime="03:07" 
        package=com.sec.android.app.bluetoothtest totalTime="00:00" lastTime="31/12/1969 21:00" lastTimeSystem="01/09/2017 08:52" inactiveTime="13:45:13" 
        package=com.samsung.android.sm.policy totalTime="00:00" lastTime="31/12/1969 21:00" lastTimeSystem="03/09/2017 23:12" inactiveTime="03:14" 
        package=com.wssnps totalTime="00:00" lastTime="31/12/1969 21:00" lastTimeSystem="03/09/2017 23:12" inactiveTime="03:08" 
        package=com.sec.android.app.snsimagecache totalTime="00:00" lastTime="31/12/1969 21:00" lastTimeSystem="03/09/2017 12:41" inactiveTime="5:45:54" 
        package=com.movile.android.appsvivo totalTime="00:04" lastTime="01/09/2017 13:36" lastTimeSystem="01/09/2017 13:36" inactiveTime="12:41:11" 
        package=eu.chainfire.supersu totalTime="00:10" lastTime="02/09/2017 10:42" lastTimeSystem="03/09/2017 23:14" inactiveTime="01:17" 
        package=com.samsung.dcmservice totalTime="00:00" lastTime="31/12/1969 21:00" lastTimeSystem="03/09/2017 23:13" inactiveTime="02:58" 
        package=com.android.phone totalTime="00:00" lastTime="31/12/1969 21:00" lastTimeSystem="03/09/2017 23:11" inactiveTime="03:43" 
        package=com.android.providers.userdictionary totalTime="00:00" lastTime="31/12/1969 21:00" lastTimeSystem="03/09/2017 23:13" inactiveTime="02:54" 
        package=com.samsung.android.sm.provider totalTime="00:00" lastTime="31/12/1969 21:00" lastTimeSystem="03/09/2017 23:12" inactiveTime="03:15" 
        package=org.daduke.realmar.dhcpv6client totalTime="07:36" lastTime="29/08/2017 09:33" lastTimeSystem="29/08/2017 09:33" inactiveTime="23:04:09" 
        package=com.android.systemui totalTime="13:04" lastTime="03/09/2017 23:02" lastTimeSystem="03/09/2017 23:11" inactiveTime="03:46" 
        package=com.facebook.appmanager totalTime="00:00" lastTime="31/12/1969 21:00" lastTimeSystem="03/09/2017 12:02" inactiveTime="5:54:11" 
        package=com.sec.android.app.SamsungContentsAgent totalTime="00:00" lastTime="31/12/1969 21:00" lastTimeSystem="03/09/2017 23:11" inactiveTime="03:40" 
        package=com.samsung.android.allshare.service.mediashare totalTime="00:00" lastTime="31/12/1969 21:00" lastTimeSystem="03/09/2017 16:53" inactiveTime="3:13:29" 
        package=android_serialport_api.sample totalTime="00:19" lastTime="25/08/2017 14:51" lastTimeSystem="25/08/2017 14:51" inactiveTime="40:03:34" 
        package=com.sec.android.provider.emergencymode totalTime="00:00" lastTime="31/12/1969 21:00" lastTimeSystem="03/09/2017 23:11" inactiveTime="03:46" 
        package=com.samsung.android.fingerprint.service totalTime="00:00" lastTime="31/12/1969 21:00" lastTimeSystem="03/09/2017 23:11" inactiveTime="03:32" 
        package=com.sec.android.app.camera totalTime="03:14" lastTime="03/09/2017 16:53" lastTimeSystem="03/09/2017 16:53" inactiveTime="3:12:58" 
        package=com.google.android.apps.magazines totalTime="00:22" lastTime="03/09/2017 16:20" lastTimeSystem="03/09/2017 16:20" inactiveTime="3:46:11" 
        package=com.android.bluetooth totalTime="00:00" lastTime="31/12/1969 21:00" lastTimeSystem="03/09/2017 23:11" inactiveTime="03:40" 
        package=com.android.providers.contacts totalTime="00:00" lastTime="31/12/1969 21:00" lastTimeSystem="03/09/2017 23:13" inactiveTime="02:54" 
        package=com.samsung.ipservice totalTime="00:00" lastTime="31/12/1969 21:00" lastTimeSystem="03/09/2017 23:13" inactiveTime="02:58" 
        package=com.samsung.sec.android.application.csc totalTime="00:00" lastTime="31/12/1969 21:00" lastTimeSystem="01/09/2017 08:52" inactiveTime="13:45:13" 
        package=com.android.captiveportallogin totalTime="04:07" lastTime="03/09/2017 01:35" lastTimeSystem="03/09/2017 01:35" inactiveTime="7:19:09" 
        package=com.samsung.android.coreapps totalTime="00:00" lastTime="31/12/1969 21:00" lastTimeSystem="03/09/2017 23:13" inactiveTime="03:01" 
        package=com.samsung.android.video totalTime="06:56" lastTime="03/09/2017 02:26" lastTimeSystem="03/09/2017 02:26" inactiveTime="6:53:15" 
      configurations
        config=pt-rBR-ldltr-sw411dp-w411dp-h707dp-normal-long-notround-port-night-560dpi-notouch-keysexposed-nokeys-navhidden-nonav-v23 totalTime="00:00" lastTime="03/09/2017 10:14" count=1 
        config=pt-rBR-ldltr-sw411dp-w411dp-h707dp-normal-long-notround-port-night-560dpi-notouch-keysexposed-nokeys-navhidden-nonav-v23 totalTime="00:00" lastTime="03/09/2017 23:11" count=1 
        config=pt-rBR-ldltr-sw411dp-w411dp-h707dp-normal-long-notround-port-560dpi-notouch-keysexposed-nokeys-navhidden-nonav-v23 totalTime="00:00" lastTime="03/09/2017 10:14" count=1 
        config=pt-rBR-ldltr-sw411dp-w411dp-h707dp-normal-long-notround-port-560dpi-notouch-keysexposed-nokeys-navhidden-nonav-v23 totalTime="00:00" lastTime="03/09/2017 23:11" count=1 
        config=pt-rBR-ldltr-sw411dp-w411dp-h731dp-normal-long-notround-port-560dpi-notouch-keysexposed-nokeys-navhidden-nonav-v23 totalTime="00:00" lastTime="03/09/2017 10:14" count=1 
        config=pt-rBR-ldltr-sw411dp-w411dp-h731dp-normal-long-notround-port-560dpi-notouch-keysexposed-nokeys-navhidden-nonav-v23 totalTime="00:00" lastTime="03/09/2017 23:11" count=1 
        config=mcc724-mnc10-pt-rBR-ldltr-sw411dp-w731dp-h387dp-normal-long-notround-land-night-560dpi-finger-keysexposed-nokeys-navhidden-nonav-v23 totalTime="1:11:24" lastTime="03/09/2017 19:55" count=13 
        config=pt-rBR-ldltr-sw411dp-w411dp-h707dp-normal-long-notround-port-night-560dpi-finger-keysexposed-nokeys-navhidden-nonav-v23 totalTime="00:10" lastTime="03/09/2017 10:15" count=1 
        config=pt-rBR-ldltr-sw411dp-w411dp-h707dp-normal-long-notround-port-night-560dpi-finger-keysexposed-nokeys-navhidden-nonav-v23 totalTime="00:05" lastTime="03/09/2017 23:11" count=1 
        config=pt-rBR-ldltr-sw411dp-w411dp-h707dp-normal-long-notround-port-night-560dpi-finger-keysexposed-nokeys-navhidden-nonav-v23 totalTime="00:10" lastTime="03/09/2017 23:11" count=1 
        config=mcc724-mnc10-pt-rBR-ldltr-sw411dp-w411dp-h707dp-normal-long-notround-port-night-560dpi-finger-keysexposed-nokeys-navhidden-nonav-v23 totalTime="11:44:56" lastTime="03/09/2017 23:11" count=14 
        config=mcc724-mnc10-pt-rBR-ldltr-sw411dp-w411dp-h707dp-normal-long-notround-port-night-560dpi-finger-keysexposed-nokeys-navhidden-nonav-v23 totalTime="00:00" lastTime="03/09/2017 23:11" count=1 
        config=pt-rBR-ldltr-sw411dp-w411dp-h707dp-normal-long-notround-port-560dpi-finger-keysexposed-nokeys-navhidden-nonav-v23 totalTime="00:00" lastTime="01/09/2017 09:19" count=1 
      events
    In-memory yearly stats
    timeRange="19/12/2016 22:00 - 03/09/2017 23:15" 
      packages
        package=com.samsung.android.provider.filterprovider totalTime="00:00" lastTime="31/12/1969 21:00" lastTimeSystem="02/09/2017 19:20" inactiveTime="7:52:32" 
        package=gr.stasta.mobiletopographer totalTime="03:20" lastTime="19/05/2017 13:17" lastTimeSystem="19/05/2017 13:17" inactiveTime="433:44:34" 
        package=com.sec.android.providers.mapcon totalTime="00:00" lastTime="31/12/1969 21:00" lastTimeSystem="03/09/2017 23:11" inactiveTime="03:43" 
        package=com.skype.raider totalTime="00:04" lastTime="14/03/2017 18:57" lastTimeSystem="06/07/2017 22:06" inactiveTime="239:35:37" 
        package=com.google.android.youtube totalTime="195:42:03" lastTime="03/09/2017 23:02" lastTimeSystem="03/09/2017 23:02" inactiveTime="03:17" 
        package=stericson.busybox totalTime="07:49" lastTime="30/08/2017 16:43" lastTimeSystem="30/08/2017 16:43" inactiveTime="18:47:22" 
        package=com.samsung.android.themestore totalTime="00:01" lastTime="19/05/2017 12:57" lastTimeSystem="19/05/2017 12:57" inactiveTime="433:47:28" 
        package=com.sec.android.app.chromecustomizations totalTime="00:00" lastTime="31/12/1969 21:00" lastTimeSystem="24/08/2017 16:54" inactiveTime="44:18:01" 
        package=com.samsung.android.app.cocktailbarservice totalTime="00:00" lastTime="31/12/1969 21:00" lastTimeSystem="03/09/2017 23:13" inactiveTime="02:59" 
        package=com.android.providers.telephony totalTime="00:00" lastTime="31/12/1969 21:00" lastTimeSystem="03/09/2017 23:11" inactiveTime="03:43" 
        package=com.sec.android.app.parser totalTime="00:00" lastTime="31/12/1969 21:00" lastTimeSystem="04/06/2017 21:48" inactiveTime="366:19:55" 
        package=com.samsung.svoice.sync totalTime="00:00" lastTime="31/12/1969 21:00" lastTimeSystem="06/03/2017 09:29" inactiveTime="738:26:24" 
        package=com.sec.android.providers.iwlansettings totalTime="00:00" lastTime="31/12/1969 21:00" lastTimeSystem="03/09/2017 23:11" inactiveTime="03:43" 
        package=com.google.android.googlequicksearchbox totalTime="12:44" lastTime="03/09/2017 23:13" lastTimeSystem="03/09/2017 23:13" inactiveTime="02:40" 
        package=com.arachnoid.sshelper totalTime="12:55" lastTime="03/09/2017 23:13" lastTimeSystem="03/09/2017 23:13" inactiveTime="02:29" 
        package=la.droid.qr.services totalTime="00:11" lastTime="02/01/2017 14:43" lastTimeSystem="02/01/2017 14:43" inactiveTime="990:51:27" 
        package=com.android.providers.calendar totalTime="00:00" lastTime="31/12/1969 21:00" lastTimeSystem="03/09/2017 20:20" inactiveTime="27:52" 
        package=com.osp.app.signin totalTime="00:00" lastTime="11/07/2017 13:53" lastTimeSystem="02/09/2017 11:51" inactiveTime="9:18:17" 
        package=org.telegram.messenger totalTime="01:41" lastTime="23/08/2017 23:16" lastTimeSystem="23/08/2017 23:16" inactiveTime="46:52:45" 
        package=com.android.providers.media totalTime="00:07" lastTime="08/06/2017 17:24" lastTimeSystem="03/09/2017 23:13" inactiveTime="02:27" 
        package=com.google.android.apps.docs.editors.docs totalTime="06:57" lastTime="03/09/2017 13:47" lastTimeSystem="03/09/2017 13:47" inactiveTime="5:03:00" 
        package=com.ntrack.tuner totalTime="02:49" lastTime="07/06/2017 11:21" lastTimeSystem="07/06/2017 11:21" inactiveTime="355:35:10" 
        package=com.sec.android.app.vefull totalTime="01:15" lastTime="16/06/2017 11:16" lastTimeSystem="16/06/2017 11:16" inactiveTime="323:05:35" 
        package=com.samsung.android.provider.shootingmodeprovider totalTime="00:00" lastTime="31/12/1969 21:00" lastTimeSystem="03/09/2017 16:53" inactiveTime="3:12:59" 
        package=com.sec.android.app.wfdbroker totalTime="00:00" lastTime="31/12/1969 21:00" lastTimeSystem="03/09/2017 23:11" inactiveTime="03:40" 
        package=it.colucciweb.sstpvpnclient totalTime="01:57" lastTime="30/08/2017 16:43" lastTimeSystem="30/08/2017 16:43" inactiveTime="18:47:24" 
        package=com.symantec.mobilesecurity totalTime="09:27" lastTime="21/06/2017 22:15" lastTimeSystem="21/06/2017 22:15" inactiveTime="300:37:47" 
        package=gpsplus.rtkgps totalTime="07:20" lastTime="25/08/2017 14:50" lastTimeSystem="25/08/2017 14:50" inactiveTime="40:04:06" 
        package=de.schildbach.wallet totalTime="00:24" lastTime="01/08/2017 21:35" lastTimeSystem="01/08/2017 21:35" inactiveTime="133:29:52" 
        package=org.simalliance.openmobileapi.service totalTime="00:00" lastTime="31/12/1969 21:00" lastTimeSystem="03/09/2017 23:11" inactiveTime="03:42" 
        package=com.samsung.android.easysetup totalTime="00:00" lastTime="31/12/1969 21:00" lastTimeSystem="03/09/2017 15:41" inactiveTime="4:22:32" 
        package=com.android.documentsui totalTime="06:59" lastTime="11/08/2017 23:36" lastTimeSystem="11/08/2017 23:36" inactiveTime="89:49:02" 
        package=com.android.externalstorage totalTime="00:00" lastTime="31/12/1969 21:00" lastTimeSystem="11/08/2017 23:35" inactiveTime="89:49:12" 
        package=org.keenteam.pingpongroot totalTime="00:25" lastTime="16/08/2017 00:18" lastTimeSystem="16/08/2017 00:18" inactiveTime="76:40:44" 
        package=com.whatsapp totalTime="175:30:14" lastTime="03/09/2017 22:21" lastTimeSystem="03/09/2017 23:12" inactiveTime="03:07" 
        package=com.android.mms.service totalTime="00:00" lastTime="31/12/1969 21:00" lastTimeSystem="01/09/2017 08:52" inactiveTime="13:45:13" 
        package=com.google.android.apps.docs.editors.slides totalTime="1:02:48" lastTime="24/05/2017 00:02" lastTimeSystem="24/05/2017 00:02" inactiveTime="413:28:10" 
        package=processing.test.kirlian_device totalTime="00:31" lastTime="27/03/2017 16:21" lastTimeSystem="27/03/2017 16:21" inactiveTime="646:12:53" 
        package=com.android.providers.downloads totalTime="00:00" lastTime="03/09/2017 15:20" lastTimeSystem="03/09/2017 23:13" inactiveTime="02:27" 
        package=com.samsung.android.qconnect totalTime="05:35" lastTime="03/09/2017 03:15" lastTimeSystem="03/09/2017 23:13" inactiveTime="02:59" 
        package=com.samsung.ucs.agent.boot totalTime="00:00" lastTime="31/12/1969 21:00" lastTimeSystem="03/09/2017 23:11" inactiveTime="03:43" 
        package=com.wsomacp totalTime="00:00" lastTime="31/12/1969 21:00" lastTimeSystem="03/09/2017 23:11" inactiveTime="03:21" 
        package=br.com.gabba.Caixa totalTime="9:12:12" lastTime="03/09/2017 19:44" lastTimeSystem="03/09/2017 19:44" inactiveTime="1:03:51" 
        package=com.sec.android.Kies totalTime="00:00" lastTime="31/12/1969 21:00" lastTimeSystem="03/09/2017 10:16" inactiveTime="6:00:01" 
        package=com.samsung.faceservice totalTime="00:00" lastTime="31/12/1969 21:00" lastTimeSystem="03/09/2017 23:13" inactiveTime="02:58" 
        package=com.accor.appli.hybrid totalTime="06:02" lastTime="31/07/2017 12:34" lastTimeSystem="31/07/2017 12:34" inactiveTime="140:03:53" 
        package=br.gov.serpro.planejamento.contracheque totalTime="32:50" lastTime="03/09/2017 19:30" lastTimeSystem="03/09/2017 19:30" inactiveTime="1:12:39" 
        package=com.sec.android.app.voicenote totalTime="09:38" lastTime="03/08/2017 16:15" lastTimeSystem="03/08/2017 16:15" inactiveTime="126:28:46" 
        package=com.mwdroide.videodownloader totalTime="00:16" lastTime="13/04/2017 13:11" lastTimeSystem="13/04/2017 13:11" inactiveTime="579:22:07" 
        package=com.dq.fotometro totalTime="00:09" lastTime="12/08/2017 23:47" lastTimeSystem="12/08/2017 23:47" inactiveTime="87:26:46" 
        package=com.sec.android.app.easylauncher totalTime="06:32" lastTime="24/08/2017 21:24" lastTimeSystem="24/08/2017 21:24" inactiveTime="43:42:19" 
        package=com.sec.android.widgetapp.easymodecontactswidget totalTime="00:00" lastTime="31/12/1969 21:00" lastTimeSystem="25/08/2017 18:24" inactiveTime="38:51:50" 
        package=com.samsung.android.email.provider totalTime="00:43" lastTime="03/09/2017 21:32" lastTimeSystem="03/09/2017 23:12" inactiveTime="03:07" 
        package=com.samsung.android.MtpApplication totalTime="5:18:48" lastTime="25/08/2017 14:28" lastTimeSystem="25/08/2017 14:28" inactiveTime="40:20:29" 
        package=com.sec.android.app.samsungapps totalTime="06:33" lastTime="29/08/2017 02:46" lastTimeSystem="29/08/2017 02:46" inactiveTime="23:49:30" 
        package=com.sec.android.emergencymode.service totalTime="00:00" lastTime="31/12/1969 21:00" lastTimeSystem="03/09/2017 23:12" inactiveTime="03:04" 
        package=com.google.android.configupdater totalTime="00:00" lastTime="31/12/1969 21:00" lastTimeSystem="11/08/2017 13:07" inactiveTime="91:46:20" 
        package=com.android.defcontainer totalTime="00:00" lastTime="31/12/1969 21:00" lastTimeSystem="03/09/2017 12:40" inactiveTime="5:46:55" 
        package=io.github.data4all totalTime="00:01" lastTime="09/05/2017 20:27" lastTimeSystem="09/05/2017 20:27" inactiveTime="469:28:41" 
        package=com.sec.android.daemonapp totalTime="00:00" lastTime="31/12/1969 21:00" lastTimeSystem="03/09/2017 23:12" inactiveTime="03:19" 
        package=com.samsung.android.slinkcloud totalTime="00:00" lastTime="31/12/1969 21:00" lastTimeSystem="01/09/2017 00:39" inactiveTime="14:36:11" 
        package=com.android.vending totalTime="1:01:36" lastTime="03/09/2017 10:56" lastTimeSystem="03/09/2017 23:13" inactiveTime="02:58" 
        package=com.joeykrim.rootcheck totalTime="00:12" lastTime="16/08/2017 17:30" lastTimeSystem="16/08/2017 17:30" inactiveTime="74:44:00" 
        package=com.microsoft.skydrive totalTime="00:00" lastTime="31/12/1969 21:00" lastTimeSystem="03/09/2017 23:13" inactiveTime="03:03" 
        package=com.sec.android.providers.security totalTime="00:00" lastTime="31/12/1969 21:00" lastTimeSystem="16/08/2017 11:50" inactiveTime="75:39:18" 
        package=com.sec.android.provider.badge totalTime="00:00" lastTime="31/12/1969 21:00" lastTimeSystem="03/09/2017 23:13" inactiveTime="02:20" 
        package=com.lefebure.ntripclient totalTime="05:51" lastTime="28/08/2017 19:34" lastTimeSystem="28/08/2017 19:34" inactiveTime="25:25:55" 
        package=com.samsung.android.app.watchmanager totalTime="00:02" lastTime="02/08/2017 11:00" lastTimeSystem="02/08/2017 11:00" inactiveTime="131:22:48" 
        package=com.oduzhar.galaxycallrecorder totalTime="00:04" lastTime="18/08/2017 18:29" lastTimeSystem="18/08/2017 18:29" inactiveTime="67:39:28" 
        package=com.samsung.android.communicationservice totalTime="00:00" lastTime="31/12/1969 21:00" lastTimeSystem="03/09/2017 23:13" inactiveTime="02:55" 
        package=com.samsung.SMT totalTime="00:06" lastTime="01/09/2017 23:54" lastTimeSystem="03/09/2017 18:53" inactiveTime="1:49:21" 
        package=com.samsung.cmh totalTime="00:00" lastTime="31/12/1969 21:00" lastTimeSystem="03/09/2017 23:13" inactiveTime="02:58" 
        package=android totalTime="7:03:34" lastTime="03/09/2017 23:11" lastTimeSystem="03/09/2017 23:11" inactiveTime="03:28" 
        package=com.android.contacts totalTime="10:38:18" lastTime="03/09/2017 12:41" lastTimeSystem="03/09/2017 12:41" inactiveTime="5:45:51" 
        package=com.samsung.hs20provider totalTime="00:00" lastTime="31/12/1969 21:00" lastTimeSystem="03/09/2017 23:12" inactiveTime="03:13" 
        package=com.samsung.android.sm.devicesecurity totalTime="00:00" lastTime="31/12/1969 21:00" lastTimeSystem="02/09/2017 18:42" inactiveTime="8:05:08" 
        package=com.ftw_and_co.happn totalTime="07:05" lastTime="14/05/2017 08:12" lastTimeSystem="14/05/2017 08:12" inactiveTime="451:12:33" 
        package=com.cinemark totalTime="06:51" lastTime="18/07/2017 20:20" lastTimeSystem="18/07/2017 20:20" inactiveTime="187:45:53" 
        package=com.gameloft.android.GloftKLMF totalTime="00:13" lastTime="17/08/2017 03:28" lastTimeSystem="29/08/2017 22:20" inactiveTime="20:49:49" 
        package=com.gameloft.android.GloftSMIM totalTime="00:00" lastTime="31/12/1969 21:00" lastTimeSystem="29/08/2017 22:20" inactiveTime="20:49:50" 
        package=com.ventel.android.radardroid2 totalTime="3:04:41" lastTime="02/09/2017 00:56" lastTimeSystem="02/09/2017 00:56" inactiveTime="10:08:26" 
        package=br.com.zap.imoveis totalTime="00:12" lastTime="01/09/2017 16:10" lastTimeSystem="01/09/2017 16:10" inactiveTime="12:06:10" 
        package=com.android.mms totalTime="3:30:32" lastTime="03/09/2017 23:13" lastTimeSystem="03/09/2017 23:13" inactiveTime="02:40" 
        package=com.android.nfc totalTime="00:00" lastTime="31/12/1969 21:00" lastTimeSystem="03/09/2017 23:11" inactiveTime="03:43" 
        package=com.android.stk totalTime="6:05:13" lastTime="23/08/2017 19:51" lastTimeSystem="01/09/2017 08:52" inactiveTime="13:45:13" 
        package=com.microsoft.rdc.android totalTime="15:59" lastTime="14/08/2017 01:59" lastTimeSystem="14/08/2017 01:59" inactiveTime="83:49:45" 
        package=com.instagram.android totalTime="38:51:08" lastTime="03/09/2017 20:04" lastTimeSystem="03/09/2017 20:04" inactiveTime="44:00" 
        package=com.MEye totalTime="00:03" lastTime="23/05/2017 22:31" lastTimeSystem="23/05/2017 22:31" inactiveTime="414:38:07" 
        package=com.waze totalTime="25:53" lastTime="24/08/2017 01:49" lastTimeSystem="24/08/2017 01:49" inactiveTime="46:45:56" 
        package=com.samsung.android.app.memo totalTime="1:54:24" lastTime="02/09/2017 15:47" lastTimeSystem="03/09/2017 12:24" inactiveTime="5:47:26" 
        package=com.studiobluelime.ecommerceapp totalTime="09:11" lastTime="27/08/2017 14:11" lastTimeSystem="27/08/2017 14:11" inactiveTime="31:55:40" 
        package=com.pinterest totalTime="01:41" lastTime="03/09/2017 11:40" lastTimeSystem="03/09/2017 11:40" inactiveTime="5:57:55" 
        package=org.coursera.android totalTime="59:12" lastTime="10/06/2017 16:47" lastTimeSystem="10/06/2017 16:47" inactiveTime="346:35:02" 
        package=org.pocketworkstation.pckeyboard totalTime="01:03" lastTime="23/08/2017 10:25" lastTimeSystem="23/08/2017 10:25" inactiveTime="49:23:25" 
        package=chat.tox.antox totalTime="11:37" lastTime="22/08/2017 17:34" lastTimeSystem="22/08/2017 17:34" inactiveTime="52:39:51" 
        package=com.instagram.layout totalTime="43:11" lastTime="24/06/2017 13:17" lastTimeSystem="24/06/2017 13:17" inactiveTime="288:54:06" 
        package=com.intsig.notes totalTime="00:39" lastTime="22/07/2017 23:19" lastTimeSystem="22/07/2017 23:19" inactiveTime="171:34:13" 
        package=com.google.android.gm totalTime="8:19:56" lastTime="03/09/2017 13:16" lastTimeSystem="03/09/2017 23:12" inactiveTime="03:07" 
        package=com.vaultmicro.camerafi2 totalTime="17:14" lastTime="12/08/2017 16:37" lastTimeSystem="12/08/2017 16:37" inactiveTime="87:59:10" 
        package=com.google.android.apps.tachyon totalTime="00:12" lastTime="27/06/2017 14:23" lastTimeSystem="17/08/2017 10:10" inactiveTime="73:50:25" 
        package=com.bradesco.exclusive totalTime="02:19" lastTime="21/12/2016 03:38" lastTimeSystem="21/12/2016 03:38" inactiveTime="1042:22:20" 
        package=org.thialfihar.android.apg totalTime="01:00" lastTime="19/06/2017 09:22" lastTimeSystem="19/06/2017 09:22" inactiveTime="311:08:06" 
        package=org.thoughtcrime.securesms totalTime="00:04" lastTime="12/08/2017 09:08" lastTimeSystem="12/08/2017 09:08" inactiveTime="89:28:55" 
        package=com.android.calendar totalTime="38:01" lastTime="01/09/2017 18:52" lastTimeSystem="01/09/2017 18:52" inactiveTime="11:19:56" 
        package=com.dlp.birdsongs totalTime="13:28" lastTime="09/05/2017 23:26" lastTimeSystem="09/05/2017 23:26" inactiveTime="467:29:59" 
        package=com.sec.android.app.wallpaperchooser totalTime="00:01" lastTime="19/05/2017 12:57" lastTimeSystem="19/05/2017 12:57" inactiveTime="433:47:34" 
        package=com.google.zxing.client.android totalTime="00:02" lastTime="22/08/2017 15:07" lastTimeSystem="22/08/2017 15:07" inactiveTime="53:10:13" 
        package=com.samsung.android.providers.context totalTime="00:00" lastTime="31/12/1969 21:00" lastTimeSystem="03/09/2017 23:11" inactiveTime="03:40" 
        package=la.droid.qr totalTime="00:35" lastTime="19/07/2017 13:42" lastTimeSystem="19/07/2017 13:42" inactiveTime="184:57:38" 
        package=com.mendhak.gpslogger totalTime="04:11" lastTime="22/06/2017 09:40" lastTimeSystem="22/06/2017 09:40" inactiveTime="298:27:00" 
        package=com.sec.android.usermanual totalTime="00:00" lastTime="28/08/2017 15:00" lastTimeSystem="28/08/2017 15:00" inactiveTime="28:21:29" 
        package=com.sec.android.gallery3d totalTime="5:57:10" lastTime="03/09/2017 16:53" lastTimeSystem="03/09/2017 16:53" inactiveTime="3:12:59" 
        package=pl.moniusoft.showmyip totalTime="04:51" lastTime="02/09/2017 10:41" lastTimeSystem="02/09/2017 10:41" inactiveTime="9:34:35" 
        package=com.android.providers.settings totalTime="00:00" lastTime="31/12/1969 21:00" lastTimeSystem="16/08/2017 11:50" inactiveTime="75:39:18" 
        package=com.google.android.music totalTime="00:00" lastTime="31/12/1969 21:00" lastTimeSystem="03/09/2017 02:14" inactiveTime="7:05:12" 
        package=com.android.printspooler totalTime="00:02" lastTime="04/08/2017 10:46" lastTimeSystem="03/09/2017 23:11" inactiveTime="03:43" 
        package=com.taxis99 totalTime="00:28" lastTime="10/07/2017 02:02" lastTimeSystem="10/07/2017 02:02" inactiveTime="222:48:30" 
        package=com.samsung.storyservice totalTime="00:00" lastTime="31/12/1969 21:00" lastTimeSystem="03/09/2017 23:13" inactiveTime="02:58" 
        package=com.sec.android.app.bcocr totalTime="00:00" lastTime="21/03/2017 10:45" lastTimeSystem="21/03/2017 10:45" inactiveTime="672:49:47" 
        package=com.sec.android.app.music totalTime="00:22" lastTime="24/08/2017 21:25" lastTimeSystem="24/08/2017 21:25" inactiveTime="43:42:17" 
        package=br.gov.ibge totalTime="02:44" lastTime="23/12/2016 19:24" lastTimeSystem="23/12/2016 19:24" inactiveTime="1035:52:22" 
        package=com.ingresso.cinemas totalTime="12:45" lastTime="27/08/2017 15:13" lastTimeSystem="27/08/2017 15:13" inactiveTime="31:11:42" 
        package=com.android.incallui totalTime="12:23:37" lastTime="03/09/2017 12:41" lastTimeSystem="03/09/2017 12:41" inactiveTime="5:46:08" 
        package=com.sec.app.samsungprintservice totalTime="00:00" lastTime="21/03/2017 17:41" lastTimeSystem="03/09/2017 03:15" inactiveTime="6:04:21" 
        package=com.estrongs.android.pop totalTime="09:36" lastTime="03/09/2017 18:07" lastTimeSystem="03/09/2017 18:07" inactiveTime="2:19:02" 
        package=com.samsung.android.service.peoplestripe totalTime="00:00" lastTime="31/12/1969 21:00" lastTimeSystem="03/09/2017 23:11" inactiveTime="03:46" 
        package=com.sec.smartcard.manager totalTime="00:00" lastTime="31/12/1969 21:00" lastTimeSystem="03/09/2017 23:11" inactiveTime="03:43" 
        package=com.dropbox.android totalTime="00:48" lastTime="30/08/2017 15:06" lastTimeSystem="30/08/2017 15:06" inactiveTime="18:53:52" 
        package=com.twitter.android totalTime="20:33" lastTime="03/09/2017 15:23" lastTimeSystem="03/09/2017 15:23" inactiveTime="4:40:19" 
        package=com.samsung.app.slowmotion totalTime="00:12" lastTime="10/07/2017 22:31" lastTimeSystem="10/07/2017 22:31" inactiveTime="220:04:15" 
        package=br.com.mobills.consultaplaca totalTime="01:19" lastTime="30/08/2017 21:50" lastTimeSystem="30/08/2017 21:50" inactiveTime="17:37:57" 
        package=br.com.bb.android totalTime="3:56:11" lastTime="03/09/2017 23:01" lastTimeSystem="03/09/2017 23:01" inactiveTime="03:40" 
        package=com.google.android.apps.docs totalTime="12:47" lastTime="18/05/2017 17:18" lastTimeSystem="30/08/2017 16:04" inactiveTime="18:48:41" 
        package=com.google.android.apps.maps totalTime="15:12:28" lastTime="03/09/2017 13:50" lastTimeSystem="03/09/2017 13:50" inactiveTime="4:59:03" 
        package=com.google.android.apps.plus totalTime="04:47" lastTime="01/09/2017 23:11" lastTimeSystem="01/09/2017 23:11" inactiveTime="10:17:26" 
        package=com.samsung.android.weather totalTime="05:26" lastTime="24/08/2017 21:22" lastTimeSystem="24/08/2017 21:22" inactiveTime="43:43:47" 
        package=com.samsung.android.app.taskedge totalTime="00:00" lastTime="31/12/1969 21:00" lastTimeSystem="03/09/2017 23:12" inactiveTime="03:17" 
        package=org.fdroid.fdroid totalTime="00:06" lastTime="31/08/2017 02:38" lastTimeSystem="31/08/2017 02:38" inactiveTime="16:22:01" 
        package=com.hudu.huvu totalTime="00:42" lastTime="21/02/2017 00:59" lastTimeSystem="21/02/2017 00:59" inactiveTime="800:19:59" 
        package=com.sec.android.inputmethod totalTime="00:01" lastTime="25/08/2017 19:36" lastTimeSystem="03/09/2017 23:04" inactiveTime="01:22" 
        package=com.sec.android.app.clockpackage totalTime="9:01:07" lastTime="01/09/2017 07:00" lastTimeSystem="01/09/2017 07:00" inactiveTime="14:22:34" 
        package=com.sec.android.app.simsettingmgr totalTime="00:00" lastTime="31/12/1969 21:00" lastTimeSystem="01/09/2017 08:52" inactiveTime="13:45:13" 
        package=com.samsung.android.app.catchfavorites totalTime="02:54" lastTime="09/05/2017 12:12" lastTimeSystem="03/09/2017 23:11" inactiveTime="03:46" 
        package=com.alephzain.framaroot totalTime="00:06" lastTime="16/08/2017 00:37" lastTimeSystem="16/08/2017 00:37" inactiveTime="76:21:49" 
        package=com.android.server.telecom totalTime="00:01" lastTime="03/09/2017 10:15" lastTimeSystem="03/09/2017 10:15" inactiveTime="6:00:45" 
        package=com.google.android.syncadapters.contacts totalTime="00:00" lastTime="31/12/1969 21:00" lastTimeSystem="03/09/2017 23:12" inactiveTime="03:07" 
        package=com.samsung.android.clipboarduiservice totalTime="00:00" lastTime="31/12/1969 21:00" lastTimeSystem="20/08/2017 22:05" inactiveTime="57:37:23" 
        package=com.android.keychain totalTime="00:00" lastTime="31/12/1969 21:00" lastTimeSystem="03/09/2017 23:12" inactiveTime="03:05" 
        package=com.android.chrome totalTime="15:54" lastTime="24/08/2017 16:54" lastTimeSystem="24/08/2017 16:54" inactiveTime="44:17:38" 
        package=com.surpax.ledflashlight.panel totalTime="10:02" lastTime="15/08/2017 04:03" lastTimeSystem="15/08/2017 04:03" inactiveTime="80:14:35" 
        package=br.gov.caixa.habitacao totalTime="1:10:38" lastTime="21/03/2017 19:26" lastTimeSystem="21/03/2017 19:26" inactiveTime="670:35:44" 
        package=com.oanda.currencyconverter totalTime="02:04" lastTime="15/07/2017 13:01" lastTimeSystem="15/07/2017 13:01" inactiveTime="199:00:30" 
        package=com.samsung.android.themecenter totalTime="00:00" lastTime="31/12/1969 21:00" lastTimeSystem="03/09/2017 23:12" inactiveTime="03:03" 
        package=com.samsung.android.sm totalTime="04:42" lastTime="03/09/2017 02:21" lastTimeSystem="03/09/2017 02:21" inactiveTime="6:57:56" 
        package=com.google.android.gms totalTime="06:33" lastTime="02/09/2017 14:17" lastTimeSystem="03/09/2017 23:14" inactiveTime="02:01" 
        package=com.google.android.gsf totalTime="00:00" lastTime="31/12/1969 21:00" lastTimeSystem="03/09/2017 23:14" inactiveTime="01:58" 
        package=com.google.android.tts totalTime="00:06" lastTime="01/09/2017 23:54" lastTimeSystem="03/09/2017 00:01" inactiveTime="7:43:07" 
        package=com.google.android.partnersetup totalTime="00:00" lastTime="31/12/1969 21:00" lastTimeSystem="03/09/2017 10:15" inactiveTime="6:00:39" 
        package=com.android.packageinstaller totalTime="04:19" lastTime="02/09/2017 02:11" lastTimeSystem="02/09/2017 02:11" inactiveTime="9:53:29" 
        package=com.google.android.videos totalTime="00:00" lastTime="31/12/1969 21:00" lastTimeSystem="16/07/2017 11:53" inactiveTime="195:45:24" 
        package=br.com.quintoandar.inquilinos totalTime="00:01" lastTime="21/02/2017 22:35" lastTimeSystem="21/02/2017 22:35" inactiveTime="796:22:41" 
        package=com.sec.spp.push totalTime="00:00" lastTime="26/08/2017 20:19" lastTimeSystem="03/09/2017 19:54" inactiveTime="54:40" 
        package=com.dsi.ant.server totalTime="00:00" lastTime="31/12/1969 21:00" lastTimeSystem="16/08/2017 11:50" inactiveTime="75:39:18" 
        package=com.sec.android.app.myfiles totalTime="43:29" lastTime="01/09/2017 00:40" lastTimeSystem="01/09/2017 00:40" inactiveTime="14:35:56" 
        package=com.gopro.smarty totalTime="1:04:25" lastTime="14/06/2017 12:34" lastTimeSystem="03/09/2017 22:15" inactiveTime="05:05" 
        package=com.samsung.android.allshare.service.fileshare totalTime="00:00" lastTime="31/12/1969 21:00" lastTimeSystem="03/09/2017 03:15" inactiveTime="6:04:19" 
        package=com.sec.android.mimage.photoretouching totalTime="32:41" lastTime="02/09/2017 19:21" lastTimeSystem="02/09/2017 19:21" inactiveTime="7:51:03" 
        package=com.sec.android.app.launcher totalTime="53:09:21" lastTime="03/09/2017 23:13" lastTimeSystem="03/09/2017 23:13" inactiveTime="02:29" 
        package=com.lmn.Arbiter_Android totalTime="01:23" lastTime="12/08/2017 19:05" lastTimeSystem="12/08/2017 19:05" inactiveTime="87:39:28" 
        package=com.sec.android.app.sns3 totalTime="00:00" lastTime="04/06/2017 13:34" lastTimeSystem="02/09/2017 19:14" inactiveTime="7:53:17" 
        package=flipboard.boxer.app totalTime="41:54" lastTime="01/09/2017 13:24" lastTimeSystem="01/09/2017 13:24" inactiveTime="12:45:10" 
        package=com.google.android.apps.photos totalTime="00:03" lastTime="19/02/2017 19:45" lastTimeSystem="10/06/2017 02:34" inactiveTime="347:32:56" 
        package=com.samsung.smartviewad totalTime="00:59" lastTime="30/06/2017 13:59" lastTimeSystem="30/06/2017 13:59" inactiveTime="270:15:01" 
        package=app.mapillary totalTime="03:31" lastTime="08/06/2017 17:08" lastTimeSystem="08/06/2017 17:08" inactiveTime="351:25:58" 
        package=com.google.android.calendar totalTime="00:21" lastTime="20/08/2017 10:44" lastTimeSystem="20/08/2017 10:44" inactiveTime="60:40:30" 
        package=com.spotify.music totalTime="46:52" lastTime="31/08/2017 00:45" lastTimeSystem="31/08/2017 00:45" inactiveTime="17:03:05" 
        package=org.thoughtcrime.redphone totalTime="00:01" lastTime="15/05/2017 23:07" lastTimeSystem="15/05/2017 23:07" inactiveTime="444:14:29" 
        package=com.ubercab totalTime="50:51" lastTime="14/08/2017 18:44" lastTimeSystem="14/08/2017 18:44" inactiveTime="81:58:55" 
        package=com.sec.android.app.sbrowser totalTime="108:34:09" lastTime="03/09/2017 20:01" lastTimeSystem="03/09/2017 20:01" inactiveTime="47:40" 
        package=br.gov.sp.detran.consultas totalTime="10:50" lastTime="07/08/2017 18:11" lastTimeSystem="07/08/2017 18:11" inactiveTime="110:04:02" 
        package=com.acr.androiddownloadmanager totalTime="00:49" lastTime="08/07/2017 11:25" lastTimeSystem="08/07/2017 11:25" inactiveTime="231:14:45" 
        package=com.facebook.katana totalTime="294:04:35" lastTime="03/09/2017 20:39" lastTimeSystem="03/09/2017 22:15" inactiveTime="05:05" 
        package=com.samsung.app.highlightplayer totalTime="00:00" lastTime="31/12/1969 21:00" lastTimeSystem="09/05/2017 23:39" inactiveTime="467:16:33" 
        package=com.samsung.enhanceservice totalTime="00:00" lastTime="31/12/1969 21:00" lastTimeSystem="03/09/2017 23:13" inactiveTime="02:58" 
        package=com.sec.android.app.vepreload totalTime="00:33" lastTime="16/06/2017 11:16" lastTimeSystem="16/06/2017 11:16" inactiveTime="323:05:31" 
        package=com.gameloft.android.LATAM.GloftCRSM totalTime="00:24" lastTime="29/08/2017 22:20" lastTimeSystem="29/08/2017 22:20" inactiveTime="20:49:48" 
        package=com.gameloft.android.LATAM.GloftDBMF totalTime="00:06" lastTime="28/03/2017 01:37" lastTimeSystem="28/03/2017 01:37" inactiveTime="644:55:57" 
        package=com.android.providers.partnerbookmarks totalTime="00:00" lastTime="31/12/1969 21:00" lastTimeSystem="24/08/2017 16:54" inactiveTime="44:18:15" 
        package=com.sonelli.juicessh totalTime="03:02" lastTime="29/05/2017 16:08" lastTimeSystem="29/05/2017 16:08" inactiveTime="390:15:58" 
        package=br.com.sitemercado.app totalTime="00:29" lastTime="09/05/2017 20:21" lastTimeSystem="09/05/2017 20:21" inactiveTime="469:33:03" 
        package=com.cleanmaster.sdk totalTime="00:00" lastTime="31/12/1969 21:00" lastTimeSystem="27/06/2017 10:27" inactiveTime="283:42:24" 
        package=com.samsung.android.beaconmanager totalTime="00:00" lastTime="31/12/1969 21:00" lastTimeSystem="03/09/2017 23:13" inactiveTime="02:59" 
        package=com.airbnb.android totalTime="00:11" lastTime="30/08/2017 00:44" lastTimeSystem="30/08/2017 00:44" inactiveTime="20:11:21" 
        package=com.sec.enterprise.mdm.services.simpin totalTime="00:00" lastTime="31/12/1969 21:00" lastTimeSystem="01/09/2017 08:52" inactiveTime="13:45:13" 
        package=com.samsung.ucs.ucspinpad totalTime="00:00" lastTime="31/12/1969 21:00" lastTimeSystem="03/09/2017 23:11" inactiveTime="03:40" 
        package=br.eti.faces.ingresso totalTime="27:55" lastTime="29/07/2017 20:19" lastTimeSystem="29/07/2017 20:19" inactiveTime="146:13:27" 
        package=com.facebook.orca totalTime="1:51:45" lastTime="03/09/2017 00:39" lastTimeSystem="03/09/2017 20:28" inactiveTime="20:27" 
        package=com.sec.android.app.popupcalculator totalTime="31:37" lastTime="31/07/2017 14:57" lastTimeSystem="31/07/2017 14:57" inactiveTime="139:19:50" 
        package=org.mozilla.firefox totalTime="3:07:28" lastTime="30/08/2017 07:16" lastTimeSystem="30/08/2017 07:16" inactiveTime="19:56:00" 
        package=jackpal.androidterm totalTime="4:20:56" lastTime="03/09/2017 01:46" lastTimeSystem="03/09/2017 01:46" inactiveTime="7:08:21" 
        package=com.sec.android.app.shealth totalTime="00:05" lastTime="01/09/2017 18:14" lastTimeSystem="01/09/2017 18:14" inactiveTime="11:36:06" 
        package=com.sec.phone totalTime="00:00" lastTime="31/12/1969 21:00" lastTimeSystem="03/09/2017 23:12" inactiveTime="03:14" 
        package=br.ceptro.simet.client.android totalTime="32:38" lastTime="02/09/2017 15:44" lastTimeSystem="02/09/2017 15:44" inactiveTime="8:10:43" 
        package=com.google.android.apps.translate totalTime="21:11" lastTime="01/09/2017 08:41" lastTimeSystem="01/09/2017 08:41" inactiveTime="13:56:22" 
        package=com.samsung.android.app.scrollcapture totalTime="01:35" lastTime="02/09/2017 19:20" lastTimeSystem="02/09/2017 19:20" inactiveTime="7:52:35" 
        package=com.adobe.reader totalTime="3:41:42" lastTime="28/08/2017 15:00" lastTimeSystem="28/08/2017 15:00" inactiveTime="28:21:27" 
        package=es.fastappstudio.whatsbackup totalTime="04:45" lastTime="08/08/2017 23:03" lastTimeSystem="08/08/2017 23:03" inactiveTime="105:08:39" 
        package=com.areatec.Digipare totalTime="38:12" lastTime="09/05/2017 21:14" lastTimeSystem="09/05/2017 21:14" inactiveTime="468:46:18" 
        package=com.samsung.android.scloud totalTime="00:00" lastTime="31/12/1969 21:00" lastTimeSystem="03/09/2017 23:12" inactiveTime="03:07" 
        package=com.samsung.android.app.soundpicker totalTime="00:14" lastTime="08/06/2017 17:24" lastTimeSystem="08/06/2017 17:24" inactiveTime="351:21:36" 
        package=com.samsung.android.spayfw totalTime="00:00" lastTime="31/12/1969 21:00" lastTimeSystem="03/09/2017 23:15" inactiveTime="00:49" 
        package=cx.ring totalTime="04:50" lastTime="03/09/2017 16:53" lastTimeSystem="03/09/2017 16:53" inactiveTime="3:12:50" 
        package=com.linkedin.android totalTime="3:23:45" lastTime="02/09/2017 12:28" lastTimeSystem="02/09/2017 12:28" inactiveTime="9:14:13" 
        package=com.android.settings totalTime="5:50:16" lastTime="03/09/2017 12:00" lastTimeSystem="03/09/2017 12:00" inactiveTime="5:55:15" 
        package=com.samsung.android.spay totalTime="00:28" lastTime="02/09/2017 11:51" lastTimeSystem="03/09/2017 23:12" inactiveTime="03:07" 
        package=com.sec.android.app.bluetoothtest totalTime="00:00" lastTime="31/12/1969 21:00" lastTimeSystem="01/09/2017 08:52" inactiveTime="13:45:13" 
        package=com.samsung.android.sm.policy totalTime="00:00" lastTime="31/12/1969 21:00" lastTimeSystem="03/09/2017 23:12" inactiveTime="03:14" 
        package=br.com.devmedia totalTime="00:01" lastTime="10/03/2017 16:34" lastTimeSystem="10/03/2017 16:34" inactiveTime="723:43:16" 
        package=com.google.android.apps.books totalTime="02:40" lastTime="23/06/2017 13:05" lastTimeSystem="16/07/2017 11:53" inactiveTime="195:45:24" 
        package=br.com.guiabolso totalTime="00:02" lastTime="10/04/2017 11:37" lastTimeSystem="10/04/2017 11:37" inactiveTime="592:12:33" 
        package=com.wssnps totalTime="00:00" lastTime="31/12/1969 21:00" lastTimeSystem="03/09/2017 23:12" inactiveTime="03:08" 
        package=com.enhance.gameservice totalTime="00:00" lastTime="07/06/2017 09:32" lastTimeSystem="07/06/2017 09:32" inactiveTime="356:29:12" 
        package=com.sec.android.app.snsimagecache totalTime="00:00" lastTime="31/12/1969 21:00" lastTimeSystem="03/09/2017 12:41" inactiveTime="5:45:54" 
        package=com.android.vpndialogs totalTime="00:04" lastTime="24/01/2017 08:05" lastTimeSystem="24/01/2017 08:05" inactiveTime="905:42:28" 
        package=com.movile.android.appsvivo totalTime="00:05" lastTime="01/09/2017 13:36" lastTimeSystem="01/09/2017 13:36" inactiveTime="12:41:11" 
        package=com.google.android.talk totalTime="14:35" lastTime="17/08/2017 13:55" lastTimeSystem="17/08/2017 13:55" inactiveTime="73:50:11" 
        package=eu.chainfire.supersu totalTime="04:30" lastTime="02/09/2017 10:42" lastTimeSystem="03/09/2017 23:14" inactiveTime="01:17" 
        package=com.samsung.dcmservice totalTime="00:00" lastTime="31/12/1969 21:00" lastTimeSystem="03/09/2017 23:13" inactiveTime="02:58" 
        package=com.android.phone totalTime="01:53" lastTime="14/08/2017 11:20" lastTimeSystem="03/09/2017 23:11" inactiveTime="03:43" 
        package=com.android.shell totalTime="00:00" lastTime="31/12/1969 21:00" lastTimeSystem="11/08/2017 23:34" inactiveTime="89:50:41" 
        package=com.here.app.maps totalTime="00:55" lastTime="01/08/2017 18:14" lastTimeSystem="01/08/2017 18:14" inactiveTime="133:52:04" 
        package=com.android.providers.userdictionary totalTime="00:00" lastTime="31/12/1969 21:00" lastTimeSystem="03/09/2017 23:13" inactiveTime="02:54" 
        package=com.mictale.gpsessentials totalTime="00:03" lastTime="06/04/2017 23:44" lastTimeSystem="06/04/2017 23:44" inactiveTime="608:13:41" 
        package=com.intsig.camscanner totalTime="42:09" lastTime="11/08/2017 15:06" lastTimeSystem="11/08/2017 15:06" inactiveTime="91:16:00" 
        package=com.samsung.android.sm.provider totalTime="00:00" lastTime="31/12/1969 21:00" lastTimeSystem="03/09/2017 23:12" inactiveTime="03:15" 
        package=com.samsung.groupcast totalTime="00:57" lastTime="08/04/2017 00:26" lastTimeSystem="08/04/2017 00:26" inactiveTime="605:00:05" 
        package=org.daduke.realmar.dhcpv6client totalTime="08:25" lastTime="29/08/2017 09:33" lastTimeSystem="29/08/2017 09:33" inactiveTime="23:04:09" 
        package=com.android.systemui totalTime="3:53:12" lastTime="03/09/2017 23:02" lastTimeSystem="03/09/2017 23:11" inactiveTime="03:46" 
        package=com.facebook.appmanager totalTime="00:00" lastTime="18/05/2017 02:28" lastTimeSystem="03/09/2017 12:02" inactiveTime="5:54:11" 
        package=com.google.android.apps.emergencyassist totalTime="00:59" lastTime="23/12/2016 15:46" lastTimeSystem="23/12/2016 15:46" inactiveTime="1036:37:13" 
        package=com.parallel30.guiaderodas totalTime="00:09" lastTime="23/06/2017 08:51" lastTimeSystem="23/06/2017 08:51" inactiveTime="291:59:18" 
        package=com.tina.time_lapse totalTime="00:11" lastTime="05/08/2017 11:07" lastTimeSystem="05/08/2017 11:07" inactiveTime="119:56:01" 
        package=com.m4u.vivozuum totalTime="00:05" lastTime="22/04/2017 11:45" lastTimeSystem="22/04/2017 11:45" inactiveTime="541:28:19" 
        package=com.sec.android.app.SamsungContentsAgent totalTime="00:00" lastTime="31/12/1969 21:00" lastTimeSystem="03/09/2017 23:11" inactiveTime="03:40" 
        package=br.com.goleditora.nuvemlivrosvivocel totalTime="01:16" lastTime="30/07/2017 10:30" lastTimeSystem="30/07/2017 10:30" inactiveTime="144:04:09" 
        package=com.samsung.android.allshare.service.mediashare totalTime="00:00" lastTime="31/12/1969 21:00" lastTimeSystem="03/09/2017 16:53" inactiveTime="3:13:29" 
        package=android_serialport_api.sample totalTime="02:07" lastTime="25/08/2017 14:51" lastTimeSystem="25/08/2017 14:51" inactiveTime="40:03:34" 
        package=com.samsung.sidi.sitevivo totalTime="00:00" lastTime="18/08/2017 09:06" lastTimeSystem="18/08/2017 09:06" inactiveTime="69:15:47" 
        package=com.sec.android.provider.emergencymode totalTime="00:00" lastTime="31/12/1969 21:00" lastTimeSystem="03/09/2017 23:11" inactiveTime="03:46" 
        package=com.samsung.android.fingerprint.service totalTime="00:00" lastTime="31/12/1969 21:00" lastTimeSystem="03/09/2017 23:11" inactiveTime="03:32" 
        package=com.sec.android.app.camera totalTime="2:01:35" lastTime="03/09/2017 16:53" lastTimeSystem="03/09/2017 16:53" inactiveTime="3:12:58" 
        package=com.google.android.apps.magazines totalTime="03:41" lastTime="03/09/2017 16:20" lastTimeSystem="03/09/2017 16:20" inactiveTime="3:46:11" 
        package=com.google.android.apps.m4b totalTime="00:01" lastTime="04/07/2017 13:45" lastTimeSystem="04/07/2017 13:45" inactiveTime="249:24:06" 
        package=com.android.bluetooth totalTime="00:00" lastTime="07/08/2017 11:47" lastTimeSystem="03/09/2017 23:11" inactiveTime="03:40" 
        package=com.zombodroid.MemeGenerator totalTime="58:15" lastTime="21/06/2017 01:00" lastTimeSystem="21/06/2017 01:00" inactiveTime="303:24:51" 
        package=com.android.providers.contacts totalTime="00:00" lastTime="31/12/1969 21:00" lastTimeSystem="03/09/2017 23:13" inactiveTime="02:54" 
        package=com.samsung.ipservice totalTime="00:00" lastTime="31/12/1969 21:00" lastTimeSystem="03/09/2017 23:13" inactiveTime="02:58" 
        package=com.samsung.sec.android.application.csc totalTime="00:00" lastTime="31/12/1969 21:00" lastTimeSystem="01/09/2017 08:52" inactiveTime="13:45:13" 
        package=com.android.captiveportallogin totalTime="1:25:41" lastTime="03/09/2017 01:35" lastTimeSystem="03/09/2017 01:35" inactiveTime="7:19:09" 
        package=com.google.earth totalTime="16:04" lastTime="04/07/2017 14:23" lastTimeSystem="04/07/2017 14:23" inactiveTime="249:16:42" 
        package=com.samsung.android.coreapps totalTime="00:07" lastTime="13/02/2017 15:20" lastTimeSystem="03/09/2017 23:13" inactiveTime="03:01" 
        package=com.samsung.android.video totalTime="7:16:17" lastTime="03/09/2017 02:26" lastTimeSystem="03/09/2017 02:26" inactiveTime="6:53:15" 
        package=com.intsig.lic.camscanner totalTime="00:00" lastTime="31/12/1969 21:00" lastTimeSystem="11/08/2017 14:54" inactiveTime="91:27:15" 
      configurations
        config=pt-rBR-ldltr-sw411dp-w411dp-h707dp-normal-long-notround-port-night-560dpi-notouch-keysexposed-nokeys-navhidden-nonav-v23 totalTime="00:00" lastTime="03/09/2017 10:14" count=1 
        config=pt-rBR-ldltr-sw411dp-w411dp-h707dp-normal-long-notround-port-night-560dpi-notouch-keysexposed-nokeys-navhidden-nonav-v23 totalTime="00:00" lastTime="03/09/2017 23:11" count=1 
        config=pt-rBR-ldltr-sw411dp-w411dp-h707dp-normal-long-notround-port-560dpi-notouch-keysexposed-nokeys-navhidden-nonav-v23 totalTime="00:00" lastTime="03/09/2017 10:14" count=1 
        config=pt-rBR-ldltr-sw411dp-w411dp-h707dp-normal-long-notround-port-560dpi-notouch-keysexposed-nokeys-navhidden-nonav-v23 totalTime="00:00" lastTime="03/09/2017 23:11" count=1 
        config=pt-rBR-ldltr-sw411dp-w411dp-h731dp-normal-long-notround-port-560dpi-notouch-keysexposed-nokeys-navhidden-nonav-v23 totalTime="00:00" lastTime="03/09/2017 10:14" count=1 
        config=pt-rBR-ldltr-sw411dp-w411dp-h731dp-normal-long-notround-port-560dpi-notouch-keysexposed-nokeys-navhidden-nonav-v23 totalTime="00:00" lastTime="03/09/2017 23:11" count=1 
        config=mcc724-mnc10-pt-rBR-ldltr-sw411dp-w731dp-h387dp-normal-long-notround-land-night-560dpi-finger-keysexposed-nokeys-navhidden-nonav-v23 totalTime="1:11:24" lastTime="03/09/2017 19:55" count=13 
        config=mcc724-mnc10-pt-rBR-ldltr-sw411dp-w411dp-h707dp-normal-long-notround-port-notnight-560dpi-finger-keysexposed-nokeys-navhidden-nonav-v23 totalTime="00:06" lastTime="14/07/2017 23:06" count=1 
        config=pt-rBR-ldltr-sw411dp-w411dp-h707dp-normal-long-notround-port-night-560dpi-finger-keysexposed-nokeys-navhidden-nonav-v23 totalTime="00:10" lastTime="03/09/2017 10:15" count=1 
        config=pt-rBR-ldltr-sw411dp-w411dp-h707dp-normal-long-notround-port-night-560dpi-finger-keysexposed-nokeys-navhidden-nonav-v23 totalTime="00:05" lastTime="03/09/2017 23:11" count=1 
        config=pt-rBR-ldltr-sw411dp-w411dp-h707dp-normal-long-notround-port-night-560dpi-finger-keysexposed-nokeys-navhidden-nonav-v23 totalTime="00:10" lastTime="03/09/2017 23:11" count=1 
        config=mcc724-mnc10-pt-rBR-ldltr-sw411dp-w411dp-h707dp-normal-long-notround-port-night-560dpi-finger-keysexposed-nokeys-navhidden-nonav-v23 totalTime="11:44:56" lastTime="03/09/2017 23:11" count=14 
        config=mcc724-mnc10-pt-rBR-ldltr-sw411dp-w411dp-h707dp-normal-long-notround-port-night-560dpi-finger-keysexposed-nokeys-navhidden-nonav-v23 totalTime="00:00" lastTime="03/09/2017 23:11" count=1 
        config=pt-rBR-ldltr-sw411dp-w411dp-h707dp-normal-long-notround-port-560dpi-finger-keysexposed-nokeys-navhidden-nonav-v23 totalTime="00:00" lastTime="01/09/2017 09:19" count=1 
      events    

```

Agora, caso voce queira desinstalar estes serviços, amigavelmente, veja o que acontece:

```bash
su
cd /system/priv-app
root@universal7420:/system/priv-app # pm uninstall intelligenceservice
#Failure [DELETE_FAILED_INTERNAL_ERROR]
root@universal7420:/system/priv-app # pm uninstall intelligenceservice2
#Failure [DELETE_FAILED_INTERNAL_ERROR]
```

Entao, nao resta outra opçao a nao ser apelar para ignorancia para os santos poderes do Linux do seu celular:
```bash
# Utilize o root
su
# Remonte a partiçao /system como permissao de escrita
mount -o remount,rw /system
# Entre no diretorio das aplicaçoes privadas
cd /system/priv-app
# decrete a execuçao sumaria dos serviços coleira-eletronica
rm -r intelligenceservice                                                               
rm -r intelligenceservice2 
```
