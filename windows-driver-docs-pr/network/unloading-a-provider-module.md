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
ms.openlocfilehash: 38b9a99993b2c8fc20d9c322c319ff487cc6454a
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63366134"
---
# <a name="unloading-a-provider-module"></a>プロバイダー モジュールのアンロード


オペレーティング システムをプロバイダー モジュールをアンロードするには、呼び出しのプロバイダー モジュールの[**アンロード**](https://msdn.microsoft.com/library/windows/hardware/ff564886)関数。 参照してください[の初期化とプロバイダー モジュールを登録する](initializing-and-registering-a-provider-module.md)プロバイダー モジュールを指定する方法の詳細について**アンロード**の初期化中に機能します。

プロバイダー モジュールの[**アンロード**](https://msdn.microsoft.com/library/windows/hardware/ff564886)関数により、プロバイダー モジュールがシステム メモリからアンロードの直前に、プロバイダー モジュールがネットワーク モジュール レジストラー (NMR) からの登録が解除されます。 プロバイダー モジュールが呼び出すことによって、NMR から登録解除の開始、 [ **NmrDeregisterProvider** ](https://msdn.microsoft.com/library/windows/hardware/ff568778)関数からはその**アンロード**関数。 プロバイダー モジュールから返す必要がありますいないその**アンロード**が完全に登録解除された、NMR から後まで関数。 場合に呼び出し**NmrDeregisterProvider**ステータスを返します\_保留中、プロバイダー モジュールを呼び出す必要があります、 [ **NmrWaitForProviderDeregisterComplete** ](https://msdn.microsoft.com/library/windows/hardware/ff568787)関数から返す前に完了する登録解除を待機する、**アンロード**関数。

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

プロバイダー モジュールは、複数のプロバイダーとして登録されている場合[ネットワーク プログラミング インターフェイス (NPIs)](network-programming-interface.md)、呼び出す必要があります[ **NmrDeregisterProvider** ](https://msdn.microsoft.com/library/windows/hardware/ff568778)各 NPI のことサポートされています。 ネットワーク モジュールは、プロバイダー モジュールとクライアントのモジュールの両方として登録されている場合 (つまり、これが NPI の 1 つのプロバイダーと別の NPI のクライアント)、どちらも呼び出す必要があります**NmrDeregisterProvider**と[ **NmrDeregisterClient**](https://msdn.microsoft.com/library/windows/hardware/ff568774)します。

ネットワーク モジュールはから戻る前に、登録解除のすべてが完了するまで待機する必要があります、 [**アンロード**](https://msdn.microsoft.com/library/windows/hardware/ff564886)関数。

プロバイダー モジュールを呼び出す必要はありません[ **NmrDeregisterProvider** ](https://msdn.microsoft.com/library/windows/hardware/ff568778)内からその[**アンロード**](https://msdn.microsoft.com/library/windows/hardware/ff564886)関数。 たとえば、プロバイダー モジュールが複雑なドライバーのサブコンポーネントが場合、プロバイダー モジュールの登録解除が発生するプロバイダー モジュールのサブコンポーネントが非アクティブ化します。 ただし、このような状況では、ドライバーする必要がありますもことを確認するプロバイダー モジュールが完全に登録解除された、NMR からから戻る前にその**アンロード**関数。

 

 





