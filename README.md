# android-neo
###Fazer o seu celular Android sair da "matrix".


Ter o root instaldo no telefone
Ter um bom servidor de SSH no telefone (SSHelper)

Acesso o telefone via SSH
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




