---
title: クライアント モジュールのアンロード
description: クライアント モジュールのアンロード
ms.assetid: 2cca2918-ce0b-4016-b3f2-fbbc06c0b7f7
keywords:
- クライアントモジュール WDK ネットワークモジュールレジストラー、アンロード
- ネットワークモジュールのアンロード
- NmrDeregisterClient
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9f4a80c287c32438b640b83e726e589b3093bfdf
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72843013"
---
# <a name="unloading-a-client-module"></a>クライアント モジュールのアンロード


クライアントモジュールをアンロードするために、オペレーティングシステムはクライアントモジュールの[**unload**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_unload)関数を呼び出します。 初期化中にクライアントモジュールの**Unload**関数を指定する方法の詳細については[、「クライアントモジュールの初期化と登録](initializing-and-registering-a-client-module.md)」を参照してください。

クライアントモジュールの[**Unload**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_unload)関数を使うと、クライアントモジュールがシステムメモリからアンロードされる前に、クライアントモジュールがネットワークモジュールレジストラー (NMR) から登録解除されるようになります。 クライアントモジュールは[**NmrDeregisterClient**](https://docs.microsoft.com/windows-hardware/drivers/ddi/netioddk/nf-netioddk-nmrderegisterclient)関数を呼び出すことによって、NMR から登録解除を開始します。この関数は、通常、**アンロード**関数から呼び出されます。 クライアントモジュールは、NMR から完全に登録解除されるまで、**アンロード**関数から戻ることはできません。 **NmrDeregisterClient**の呼び出しで STATUS\_PENDING が返された場合、クライアントモジュールは、その**アンロード**から戻る前に、登録解除が完了するのを待つために[**NmrWaitForClientDeregisterComplete**](https://docs.microsoft.com/windows-hardware/drivers/ddi/netioddk/nf-netioddk-nmrwaitforclientderegistercomplete)関数を呼び出す必要があります。プロシージャ.

次に、例を示します。

```C++
// Variable containing the handle for the registration
HANDLE ClientHandle;

// Unload function
VOID
  Unload(
    IN PDRIVER_OBJECT DriverObject
    )
{
  NTSTATUS Status;

  // Deregister the client module from the NMR
  Status =
    NmrDeregisterClient(
      ClientHandle
      );

  // Check if pending
  if (Status == STATUS_PENDING)
  {
    // Wait for the deregistration to be completed
    NmrWaitForClientDeregisterComplete(
      ClientHandle
      );
  }

  // An error occurred
  else
  {
    // Handle error
    ...
  }
}
```

クライアントモジュールが複数の[ネットワークプログラミングインターフェイス (NPIs)](network-programming-interface.md)のクライアントとして登録されている場合、サポートされている各 NPI に対して[**NmrDeregisterClient**](https://docs.microsoft.com/windows-hardware/drivers/ddi/netioddk/nf-netioddk-nmrderegisterclient)を呼び出す必要があります。 ネットワークモジュールがクライアントモジュールとプロバイダーモジュールの両方として登録されている場合 (つまり、1つの NPI のクライアントと、別の NPI のプロバイダー)、 **NmrDeregisterClient**と[**NmrDeregisterProvider**](https://docs.microsoft.com/windows-hardware/drivers/ddi/netioddk/nf-netioddk-nmrderegisterprovider)の両方を呼び出す必要があります。

ネットワークモジュールは、[**アンロード**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_unload)関数から戻る前に、すべての登録解除が完了するまで待機する必要があります。

クライアントモジュールは、 [**Unload**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_unload)関数内から[**NmrDeregisterClient**](https://docs.microsoft.com/windows-hardware/drivers/ddi/netioddk/nf-netioddk-nmrderegisterclient)を呼び出す必要はありません。 たとえば、クライアントモジュールが複雑なドライバーのサブコンポーネントである場合、クライアントモジュールのサブコンポーネントを非アクティブ化すると、クライアントモジュールの登録解除が発生する可能性があります。 ただし、このような状況でも、ドライバーは、 **Unload**関数から戻る前に、クライアントモジュールが NMR から完全に登録解除されていることを確認する必要があります。

 

 





