---
title: Winsock カーネル アプリケーションの登録解除
description: Winsock カーネル アプリケーションの登録解除
ms.assetid: f5d99c10-eeac-499e-8630-6aa188d38d75
keywords:
- Winsock カーネル WDK ネットワーク, 登録
- Winsock カーネルアプリケーションの登録解除
- WSK WDK ネットワーク, 登録
- WskDeregister 解除
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 712c802c6c91451981855328010f0d9785a0b3c2
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72843003"
---
# <a name="unregistering-a-winsock-kernel-application"></a>Winsock カーネル アプリケーションの登録解除


[**Wskregister**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wsk/nf-wsk-wskregister)関数を使用して wsk クライアントとして正常に登録された Winsock カーネル (wsk) アプリケーションでは、ドライバーの[**Unload**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_unload)関数が戻る前に、その呼び出しが返さ[**れたこと**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wsk/nf-wsk-wskderegister)を確認する必要があります. **Wskregister**が正常に呼び出された wsk アプリケーションは、 **wskregister**を呼び出さずにアンロードしないようにする必要があります。これにより、wsk プロバイダー NPI のキャプチャされたすべてのインスタンスがによって[**解放されるまで、wsk クライアントオブジェクトの登録解除が待機されます。WskReleaseProviderNPI**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wsk/nf-wsk-wskreleaseprovidernpi)とすべてのソケットは WSK アプリケーションによって閉じられます。 [**Wsk\_PROVIDER\_DISPATCH**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wsk/ns-wsk-_wsk_provider_dispatch)の関数に渡された保留中の irp がある場合 **、その**保留中の irp が完了するまで待機します。 WSK アプリケーションは、 **WskReleaseProviderNPI**が呼び出された後に、wsk\_PROVIDER\_DISPATCH の関数を呼び出すことはできません。

次に、例を示します。

```C++
// Unload function
VOID
  Unload(
    IN PDRIVER_OBJECT DriverObject
    )
{
  // Unregister the WSK application
  WskDeregister(
    &WskRegistration
    );

}
```

WSK アプリケーションは必ずしも*アンロード*関数内から**wskderegister**を呼び出す必要はありません。 たとえば、WSK アプリケーションが複雑なドライバーのサブコンポーネントである場合、wsk アプリケーションのサブコンポーネントが非アクティブになると、WSK アプリケーションの**Wskderegister**への呼び出しが発生する可能性があります。 このようなシナリオでは、ドライバーが*Unload*関数から戻る前に、wsk アプリケーションが**wskderegister**解除の呼び出しによって正常に登録解除されていることを確認する必要があります。

 

 





