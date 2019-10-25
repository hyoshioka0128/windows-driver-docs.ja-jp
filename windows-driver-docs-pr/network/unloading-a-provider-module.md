---
title: プロバイダー モジュールのアンロード
description: プロバイダー モジュールのアンロード
ms.assetid: c6dd6552-2923-4091-9bf1-5833c049aa23
keywords:
- プロバイダーモジュール WDK ネットワークモジュールレジストラー、アンロード
- ネットワークモジュールのアンロード
- NmrDeregisterProvider
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 399671d6fd57fe8262cd33e22d6c7f3c00d3080b
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72843008"
---
# <a name="unloading-a-provider-module"></a>プロバイダー モジュールのアンロード


プロバイダーモジュールをアンロードするために、オペレーティングシステムはプロバイダーモジュールの[**unload**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_unload)関数を呼び出します。 初期化中にプロバイダーモジュールの**Unload**関数を指定する方法の詳細については[、「プロバイダーモジュールの初期化と登録](initializing-and-registering-a-provider-module.md)」を参照してください。

プロバイダーモジュールの[**Unload**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_unload)関数は、プロバイダーモジュールがシステムメモリからアンロードされる前に、プロバイダーモジュールがネットワークモジュールレジストラー (NMR) から登録解除されることを保証します。 プロバイダーモジュールは[**NmrDeregisterProvider**](https://docs.microsoft.com/windows-hardware/drivers/ddi/netioddk/nf-netioddk-nmrderegisterprovider)関数を呼び出すことによって、NMR から登録解除を開始します。この関数は、通常、**アンロード**関数から呼び出されます。 プロバイダーモジュールは、NMR から完全に登録解除されるまで、**アンロード**関数から戻ることはできません。 **NmrDeregisterProvider**の呼び出しで STATUS\_PENDING が返された場合、プロバイダーモジュールは、その**アンロード**から戻る前に、登録解除が完了するのを待機するために[**NmrWaitForProviderDeregisterComplete**](https://docs.microsoft.com/windows-hardware/drivers/ddi/netioddk/nf-netioddk-nmrwaitforproviderderegistercomplete)関数を呼び出す必要があります。プロシージャ.

次に、例を示します。

```C++
// Variable containing the handle for the registration
HANDLE ProviderHandle;

// Unload function
VOID
  Unload(
    IN PDRIVER_OBJECT DriverObject
    )
{
  NTSTATUS Status;

  // Deregister the provider module from the NMR
  Status =
    NmrDeregisterProvider(
      ProviderHandle
      );

  // Check if pending
  if (Status == STATUS_PENDING)
  {
    // Wait for the deregistration to be completed
    NmrWaitForProviderDeregisterComplete(
      ProviderHandle
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

プロバイダーモジュールが複数の[ネットワークプログラミングインターフェイス (NPIs)](network-programming-interface.md)のプロバイダーとして登録されている場合、サポートされている各 NPI に対して[**NmrDeregisterProvider**](https://docs.microsoft.com/windows-hardware/drivers/ddi/netioddk/nf-netioddk-nmrderegisterprovider)を呼び出す必要があります。 ネットワークモジュールがプロバイダーモジュールとクライアントモジュールの両方として登録されている場合 (つまり、1つの NPI のプロバイダーと別の NPI のクライアントである場合)、 **NmrDeregisterProvider**と[**NmrDeregisterClient**](https://docs.microsoft.com/windows-hardware/drivers/ddi/netioddk/nf-netioddk-nmrderegisterclient)の両方を呼び出す必要があります。

ネットワークモジュールは、[**アンロード**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_unload)関数から戻る前に、すべての登録解除が完了するまで待機する必要があります。

プロバイダーモジュールは、 [**Unload**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_unload)関数内から[**NmrDeregisterProvider**](https://docs.microsoft.com/windows-hardware/drivers/ddi/netioddk/nf-netioddk-nmrderegisterprovider)を呼び出す必要はありません。 たとえば、プロバイダーモジュールが複雑なドライバーのサブコンポーネントである場合、プロバイダーモジュールのサブコンポーネントが非アクティブ化されると、プロバイダーモジュールの登録解除が発生する可能性があります。 ただし、このような状況でも、ドライバーは、**アンロード**関数から戻る前に、プロバイダーモジュールが NMR から完全に登録解除されていることを確認する必要があります。

 

 





