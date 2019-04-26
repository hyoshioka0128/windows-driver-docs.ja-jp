---
title: クライアント モジュールのアンロード
description: クライアント モジュールのアンロード
ms.assetid: 2cca2918-ce0b-4016-b3f2-fbbc06c0b7f7
keywords:
- クライアント モジュールをアンロード WDK ネットワーク モジュール レジストラー
- ネットワーク モジュールのアンロード
- NmrDeregisterClient
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: f79248bd77e9a5170b083da4d30ff0e98ee603e7
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63346636"
---
# <a name="unloading-a-client-module"></a>クライアント モジュールのアンロード


オペレーティング システムをクライアント モジュールをアンロードするには、呼び出しのクライアント モジュールの[**アンロード**](https://msdn.microsoft.com/library/windows/hardware/ff564886)関数。 参照してください[の初期化とクライアント モジュールを登録する](initializing-and-registering-a-client-module.md)クライアント モジュールを指定する方法の詳細について**アンロード**の初期化中に機能します。

クライアント モジュールの[**アンロード**](https://msdn.microsoft.com/library/windows/hardware/ff564886)関数により、クライアント モジュールがシステム メモリからアンロードの直前にあるクライアント モジュールがネットワーク モジュール レジストラー (NMR) からの登録が解除されます。 クライアントのモジュールを呼び出すことによって、NMR から登録解除の開始、 [ **NmrDeregisterClient** ](https://msdn.microsoft.com/library/windows/hardware/ff568774)関数からはその**アンロード**関数。 クライアント モジュールから返す必要がありますいないその**アンロード**が完全に登録解除された、NMR から後まで関数。 場合に呼び出し**NmrDeregisterClient**ステータスを返します\_保留中、クライアント モジュールを呼び出す必要があります、 [ **NmrWaitForClientDeregisterComplete** ](https://msdn.microsoft.com/library/windows/hardware/ff568786)関数登録解除を返す前に完了するまで待ちますその**アンロード**関数。

例:

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

クライアント モジュールは、複数のクライアントとして登録されている場合[ネットワーク プログラミング インターフェイス (NPIs)](network-programming-interface.md)、呼び出す必要があります[ **NmrDeregisterClient** ](https://msdn.microsoft.com/library/windows/hardware/ff568774)各 NPI でサポートされるのです。 ネットワーク モジュールがクライアント モジュールとプロバイダー モジュールの両方として登録されている場合 (つまり、これが NPI の 1 つのクライアントおよび別の NPI のプロバイダー)、どちらも呼び出す必要があります**NmrDeregisterClient**と[ **NmrDeregisterProvider**](https://msdn.microsoft.com/library/windows/hardware/ff568778)します。

ネットワーク モジュールはから戻る前に、登録解除のすべてが完了するまで待機する必要があります、 [**アンロード**](https://msdn.microsoft.com/library/windows/hardware/ff564886)関数。

クライアント モジュールを呼び出す必要はありません[ **NmrDeregisterClient** ](https://msdn.microsoft.com/library/windows/hardware/ff568774)内からその[**アンロード**](https://msdn.microsoft.com/library/windows/hardware/ff564886)関数。 たとえば、クライアント モジュールが複雑なドライバーのサブコンポーネントが場合、クライアント モジュールの登録解除が発生するクライアント モジュールのサブコンポーネントが非アクティブ化します。 ただし、このような状況では、ドライバーする必要がありますもことを確認するクライアント モジュールが完全に登録解除された、NMR からから戻る前にその**アンロード**関数。

 

 





