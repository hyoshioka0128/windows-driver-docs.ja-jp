---
title: プロバイダー モジュールのアンロード
description: プロバイダー モジュールのアンロード
ms.assetid: c6dd6552-2923-4091-9bf1-5833c049aa23
keywords:
- プロバイダーのモジュールをアンロード WDK ネットワーク モジュール レジストラー
- ネットワーク モジュールのアンロード
- NmrDeregisterProvider
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 35d5c4af261f78329a54b85370d37013604e5428
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67382100"
---
# <a name="unloading-a-provider-module"></a>プロバイダー モジュールのアンロード


オペレーティング システムをプロバイダー モジュールをアンロードするには、呼び出しのプロバイダー モジュールの[**アンロード**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_unload)関数。 参照してください[の初期化とプロバイダー モジュールを登録する](initializing-and-registering-a-provider-module.md)プロバイダー モジュールを指定する方法の詳細について**アンロード**の初期化中に機能します。

プロバイダー モジュールの[**アンロード**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_unload)関数により、プロバイダー モジュールがシステム メモリからアンロードの直前に、プロバイダー モジュールがネットワーク モジュール レジストラー (NMR) からの登録が解除されます。 プロバイダー モジュールが呼び出すことによって、NMR から登録解除の開始、 [ **NmrDeregisterProvider** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/netioddk/nf-netioddk-nmrderegisterprovider)関数からはその**アンロード**関数。 プロバイダー モジュールから返す必要がありますいないその**アンロード**が完全に登録解除された、NMR から後まで関数。 場合に呼び出し**NmrDeregisterProvider**ステータスを返します\_保留中、プロバイダー モジュールを呼び出す必要があります、 [ **NmrWaitForProviderDeregisterComplete** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/netioddk/nf-netioddk-nmrwaitforproviderderegistercomplete)関数から返す前に完了する登録解除を待機する、**アンロード**関数。

例:

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

プロバイダー モジュールは、複数のプロバイダーとして登録されている場合[ネットワーク プログラミング インターフェイス (NPIs)](network-programming-interface.md)、呼び出す必要があります[ **NmrDeregisterProvider** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/netioddk/nf-netioddk-nmrderegisterprovider)各 NPI のことサポートされています。 ネットワーク モジュールは、プロバイダー モジュールとクライアントのモジュールの両方として登録されている場合 (つまり、これが NPI の 1 つのプロバイダーと別の NPI のクライアント)、どちらも呼び出す必要があります**NmrDeregisterProvider**と[ **NmrDeregisterClient**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/netioddk/nf-netioddk-nmrderegisterclient)します。

ネットワーク モジュールはから戻る前に、登録解除のすべてが完了するまで待機する必要があります、 [**アンロード**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_unload)関数。

プロバイダー モジュールを呼び出す必要はありません[ **NmrDeregisterProvider** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/netioddk/nf-netioddk-nmrderegisterprovider)内からその[**アンロード**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_unload)関数。 たとえば、プロバイダー モジュールが複雑なドライバーのサブコンポーネントが場合、プロバイダー モジュールの登録解除が発生するプロバイダー モジュールのサブコンポーネントが非アクティブ化します。 ただし、このような状況では、ドライバーする必要がありますもことを確認するプロバイダー モジュールが完全に登録解除された、NMR からから戻る前にその**アンロード**関数。

 

 





