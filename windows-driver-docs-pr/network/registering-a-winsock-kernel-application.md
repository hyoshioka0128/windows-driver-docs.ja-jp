---
title: Winsock カーネル アプリケーションの登録
description: Winsock カーネル アプリケーションの登録
ms.assetid: aaba39b8-8609-46e6-906d-3f050d91af7f
keywords:
- Winsock カーネル WDK ネットワーク、登録します。
- Winsock Kernel アプリケーションの登録
- WSK WDK ネットワーク、登録します。
- ネットワーク WSK WDK、プロバイダー NPI をキャプチャします。
- キャプチャ WSK プロバイダー NPI WDK ネットワーク
- クライアント オブジェクト WDK Winsock カーネル
- WskRegister
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d67b641949397063071d8f4e49faeb28f67abc04
ms.sourcegitcommit: b3859d56cb393e698c698d3fb13519ff1522c7f3
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/05/2019
ms.locfileid: "57348671"
---
# <a name="registering-a-winsock-kernel-application"></a>Winsock カーネル アプリケーションの登録


### <a name="wsk-client-object-registration"></a>WSK クライアント オブジェクトの登録

Winsock カーネル (WSK) アプリケーションを呼び出すことによって WSK クライアントとして登録する必要があります、 [ **WskRegister** ](https://msdn.microsoft.com/library/windows/hardware/ff571143)関数。 **WskRegister** WSK アプリケーションを初期化し、その WSK クライアントのポインターを渡す必要があります[ネットワーク プログラミング インターフェイス (NPI)](network-programming-interface.md)(、 [ **WSK\_クライアント\_NPI** ](https://msdn.microsoft.com/library/windows/hardware/ff571163)構造) と WSK 登録オブジェクト (、 [ **WSK\_登録**](https://msdn.microsoft.com/library/windows/hardware/ff571178)構造)で初期化する**WskRegister**成功時にします。

次のコード例では、WSK クライアントとして WSK アプリケーションを登録する方法を示します。

```C++
// Include the WSK header file
#include "wsk.h"

// WSK Client Dispatch table that denotes the WSK version
// that the WSK application wants to use and optionally a pointer
// to the WskClientEvent callback function
const WSK_CLIENT_DISPATCH WskAppDispatch = {
  MAKE_WSK_VERSION(1,0), // Use WSK version 1.0
  0,    // Reserved
  NULL  // WskClientEvent callback not required for WSK version 1.0
};

// WSK Registration object
WSK_REGISTRATION WskRegistration;

// DriverEntry function
NTSTATUS
  DriverEntry(
    PDRIVER_OBJECT DriverObject,
    PUNICODE_STRING RegistryPath
    )
{
  NTSTATUS Status;
  WSK_CLIENT_NPI wskClientNpi;

  .
  . 
  .

  // Register the WSK application
  wskClientNpi.ClientContext = NULL;
  wskClientNpi.Dispatch = &WskAppDispatch;
  Status = WskRegister(&wskClientNpi, &WskRegistration);

  if(!NT_SUCCESS(Status)) {
      .
      .
      .
      return Status;
  }

  .
  . 
  .
}
```

WSK アプリケーションを呼び出す必要はありません[ **WskRegister** ](https://msdn.microsoft.com/library/windows/hardware/ff571143)内からその**DriverEntry**関数。 たとえば、WSK アプリケーションが複雑なドライバーのサブコンポーネントの場合は、WSK アプリケーションのサブコンポーネントがアクティブな場合にのみが、アプリケーションの登録することがあります。

WSK アプリケーションを保持する必要があります、 [ **WSK\_クライアント\_ディスパッチ**](https://msdn.microsoft.com/library/windows/hardware/ff571159)に構造体が渡される**WskRegister**有効となるまで、メモリに常駐しています。[ **WskDeregister** ](https://msdn.microsoft.com/library/windows/hardware/ff571128)と呼ばれますが、登録が無効になっているとします。 [ **WSK\_登録**](https://msdn.microsoft.com/library/windows/hardware/ff571178)構造も保持する必要が有効であり、メモリに常駐 WSK アプリケーションは、他の呼び出しが停止するまで[WSK 登録関数](https://msdn.microsoft.com/library/windows/hardware/ff571179). 上記のコード例では、確保されるため、構造データ メモリに常駐しているドライバーがロードされるまで、ドライバーのグローバル データ セクションにこれら 2 つの構造を保持します。

### <a name="wsk-provider-npi-capture"></a>WSK プロバイダー NPI キャプチャ

持つ WSK クライアントとしてアプリケーションが登録されて、WSK 後[ **WskRegister**](https://msdn.microsoft.com/library/windows/hardware/ff571143)、それを使用する必要があります、 [ **WskCaptureProviderNPI** ](https://msdn.microsoft.com/library/windows/hardware/ff571122)関数WSK インターフェイスの使用を開始するには、WSK サブシステムから WSK プロバイダー NPI をキャプチャします。

WSK サブシステムまだ準備が整っていない WSK アプリケーションが NPI、WSK プロバイダーをキャプチャしようとしたときのため、 **WskCaptureProviderNPI**関数により、WSK アプリケーションとして準備を整えるために、WSK サブシステムのポーリング、待機するには次に示します。

-   場合、 *WaitTimeout*パラメーターは、WSK\_いいえ\_待機、関数は常に返します直ちに待機なし。

-   場合*WaitTimeout* WSK は\_無限\_待機、WSK サブシステム準備が整うまで、関数はまで待機します。

-   場合*WaitTimeout* 、他の値は、関数は、WSK サブシステム準備が整ったときに、または (ミリ秒単位)、待機時間の値に達する*WaitTimeout*、早い方.

**重要な**  悪影響を及ぼす他のドライバーやサービスを呼び出す WSK アプリケーションの開始に影響しないように**WskCaptureProviderNPI**からその**DriverEntry**関数は設定しないでください、 *WaitTimeout* WSK パラメーター\_無限\_待つか、過剰な待機時間。 また、WSK アプリケーションは、システムのスタートアップの段階で最初に起動する場合を待つべきものを別のワーカー スレッドの準備を整えるために、WSK サブシステム**DriverEntry**を実行します。

 

場合に呼び出し**WskCaptureProviderNPI**状態で失敗\_NOINTERFACE、WSK アプリケーションを使用できる、 [ **WskQueryProviderCharacteristics** ](https://msdn.microsoft.com/library/windows/hardware/ff571138)WSK サブシステムでサポートされる範囲の WSK NPI バージョンを検出する関数。 WSK アプリケーションを呼び出して**WskDeregister**登録の現在のインスタンスの登録を解除し、さまざまなを使用してもう一度登録[ **WSK\_クライアント\_ディスパッチ** ](https://msdn.microsoft.com/library/windows/hardware/ff571159)はサポートされている WSK NPI バージョンを使用するインスタンス。

ときに**WskCaptureProviderNPI** 、正常に返されますその*WskProviderNpi*パラメーターが指す WSK プロバイダー NPI ( [ **WSK\_プロバイダー\_NPI**](https://msdn.microsoft.com/library/windows/hardware/ff571177)) WSK アプリケーションで使用できるようにします。 WSK\_プロバイダー\_NPI 構造体には、WSK クライアント オブジェクトへのポインターが含まれています ( [ **WSK\_クライアント**](https://msdn.microsoft.com/library/windows/hardware/ff571155)) および[ **WSK\_プロバイダー\_ディスパッチ**](https://msdn.microsoft.com/library/windows/hardware/ff571175) WSK アプリケーションは、WSK ソケットを作成し、WSK クライアント オブジェクトでは、その他の操作の実行に使用できる WSK 関数のディスパッチ テーブル。 WSK 適用された後は、WSK を使用して完成した\_プロバイダー\_ディスパッチ関数、WSK プロバイダー NPI を呼び出すことによって解放が必要があります[ **WskReleaseProviderNPI**](https://msdn.microsoft.com/library/windows/hardware/ff571145)します。

次のコード例では、WSK アプリケーションでキャプチャ WSK プロバイダー NPI、ソケットの作成に使用し、元の方法を示します。

```C++
// WSK application routine that waits for WSK subsystem
// to become ready and captures the WSK Provider NPI
NTSTATUS
  WskAppWorkerRoutine(
    )
{
  NTSTATUS Status;
  WSK_PROVIDER_NPI wskProviderNpi;
 
  // Capture the WSK Provider NPI. If WSK subsystem is not ready yet,
  // wait until it becomes ready.
  Status = WskCaptureProviderNPI(
    &WskRegistration, // must have been initialized with WskRegister
    WSK_INFINITE_WAIT,
    &wskProviderNpi
    );

  if(!NT_SUCCESS(Status))
  {
    // The WSK Provider NPI could not be captured.
    if( Status == STATUS_NOINTERFACE ) {
      // WSK application's requested version is not supported
    }
    else if( status == STATUS_DEVICE_NOT_READY ) {
      // WskDeregister was invoked in another thread thereby causing
      // WskCaptureProviderNPI to be canceled.
    } 
    else {
      // Some other unexpected failure has occurred
    }

    return Status;
  }

  // The WSK Provider NPI has been captured.
  // Create and set up a listening socket that accepts
   // incoming connections.
  Status = CreateListeningSocket(&wskProviderNpi, ...);

  // The WSK Provider NPI will not be used any more.
  // So, release it here immediately.
  WskReleaseProviderNPI(&WskRegistration);

  // Return result of socket creation routine
  return Status;

}
```

WSK アプリケーションが呼び出すことができます[ **WskCaptureProviderNPI** ](https://msdn.microsoft.com/library/windows/hardware/ff571122) 2 回以上。 呼び出しごとに**WskCaptureProviderNPI**正常に返されますが、対応する呼び出しが必要があります[ **WskReleaseProviderNPI**](https://msdn.microsoft.com/library/windows/hardware/ff571145)します。 WSK アプリケーションが内の関数に対する呼び出しを行う必要がありますいない[ **WSK\_プロバイダー\_ディスパッチ**](https://msdn.microsoft.com/library/windows/hardware/ff571175)呼び出した後**WskReleaseProviderNPI**.

 

 





