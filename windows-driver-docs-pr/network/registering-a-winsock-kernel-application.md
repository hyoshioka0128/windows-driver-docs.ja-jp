---
title: Winsock カーネル アプリケーションの登録
description: Winsock カーネル アプリケーションの登録
ms.assetid: aaba39b8-8609-46e6-906d-3f050d91af7f
keywords:
- Winsock カーネル WDK ネットワーク, 登録
- Winsock カーネルアプリケーションを登録しています
- WSK WDK ネットワーク, 登録
- WSK WDK ネットワーク、プロバイダ NPI キャプチャ
- WSK プロバイダーのキャプチャ NPI WDK ネットワーク
- クライアントオブジェクト WDK Winsock カーネル
- WskRegister
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 425fa6f0a8f5d6936d696ecb198dfe40227c83d4
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72842097"
---
# <a name="registering-a-winsock-kernel-application"></a>Winsock カーネル アプリケーションの登録


### <a name="wsk-client-object-registration"></a>WSK クライアントオブジェクトの登録

Winsock カーネル (WSK) アプリケーションは、 [**Wskregister**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wsk/nf-wsk-wskregister)関数を呼び出すことによって wsk クライアントとして登録する必要があります。 **Wskregister**では、wsk クライアントの[ネットワークプログラミングインターフェイス (NPI)](network-programming-interface.md)( [**WSK\_client\_NPI**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wsk/ns-wsk-_wsk_client_npi)構造) と wsk 登録オブジェクト (wsk [ **\_registration**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wsk/ns-wsk-_wsk_registration)構造体) へのポインターを渡す必要があります。これは、正常に返されたときに**wskregister**によって初期化されます。

WSK アプリケーションを WSK クライアントとして登録する方法を次のコード例に示します。

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

WSK アプリケーションは、 **Driverentry**関数内から[**wskregister**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wsk/nf-wsk-wskregister)を呼び出す必要はありません。 たとえば、WSK アプリケーションが複雑なドライバーのサブコンポーネントである場合、WSK アプリケーションサブコンポーネントがアクティブになっている場合にのみ、アプリケーションの登録が発生する可能性があります。

WSK アプリケーションは、 **Wskregister**が有効になり、 [**wskregister**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wsk/nf-wsk-wskderegister)が呼び出され、登録が有効でなくなるまで、 [**WSK\_クライアント\_ディスパッチ**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wsk/ns-wsk-_wsk_client_dispatch)構造体をメモリ内に保持する必要があります。 Wsk の[ **\_登録**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wsk/ns-wsk-_wsk_registration)構造も有効である必要があり、wsk アプリケーションが他の[wsk 登録関数](https://docs.microsoft.com/windows-hardware/drivers/ddi/_netvista/)の呼び出しを停止するまでメモリに常駐します。 前のコード例では、ドライバーのグローバルデータセクションにこれら2つの構造体を保持します。これにより、ドライバーがアンロードされるまで、構造体データはメモリに常駐します。

### <a name="wsk-provider-npi-capture"></a>WSK プロバイダー NPI Capture

Wsk アプリケーションを WSK クライアントとして[**Wskregister**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wsk/nf-wsk-wskregister)に登録した後、wsk インターフェイスの使用を開始するには、 [**WskCaptureProviderNPI**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wsk/nf-wsk-wskcaptureprovidernpi)関数を使用して wsk サブシステムから wsk プロバイダー NPI をキャプチャする必要があります。

Wsk アプリケーションが WSK プロバイダー NPI をキャプチャしようとしたときに WSK サブシステムがまだ準備ができていない可能性があるため、 **WskCaptureProviderNPI**関数を使用すると、wsk アプリケーションは、次のように wsk サブシステムをポーリングまたは待機できるようになります。

-   *Waittimeout*パラメーターが wsk\_\_待機しない場合、関数は常に待機せずに直ちに戻ります。

-   *Waittimeout*が wsk\_無限\_待機の場合、この関数は wsk サブシステムが準備できるようになるまで待機します。

-   *Waittimeout*がその他の値の場合、関数は wsk サブシステムが準備できたとき、または待機時間 (ミリ秒単位) が*waittimeout*の値 (どちらか早い方) に達したときに、を返します。

**重要**  他のドライバーやサービスの開始に悪影響を及ぼさないようにするために、 **driverentry**関数から**WskCaptureProviderNPI**を呼び出す Wsk アプリケーションでは、 *waittimeout*パラメーターを wsk\_無限\_待機または過剰な待機時間に設定しないでください。 また、WSK アプリケーションがシステム開始フェーズの初期段階で開始された場合、WSK サブシステムが**Driverentry**が実行されているものとは別のワーカースレッドで準備されるまで待機する必要があります。

 

**WskCaptureProviderNPI**の呼び出しがステータス\_nointerface で失敗した場合、wsk アプリケーションは[**Wskqueryprovidercharacteristics**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wsk/nf-wsk-wskqueryprovidercharacteristics)関数を使用して wsk サブシステムでサポートされている wsk NPI バージョンの範囲を見つけることができます。 WSK アプリケーションは、 **Wskderegister**を呼び出して現在の登録インスタンスの登録を解除してから、サポートされている WSK NPI バージョンを使用する別の[**WSK\_クライアント\_ディスパッチ**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wsk/ns-wsk-_wsk_client_dispatch)インスタンスを使用して再度登録できます。

**WskCaptureProviderNPI**が正常に返されると、その*WskProviderNpi*パラメーターは wsk プロバイダー NPI ( [**WSK\_provider\_NPI**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wsk/ns-wsk-_wsk_provider_npi)) をポイントし、wsk アプリケーションで使用できるようになります。 WSK\_PROVIDER\_NPI 構造体には、wsk クライアントオブジェクト ( [**wsk\_クライアント**](https://docs.microsoft.com/windows-hardware/drivers/network/wsk-client)) へのポインターと wsk 関数の[**WSK\_PROVIDER\_ディスパッチ**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wsk/ns-wsk-_wsk_provider_dispatch)ディスパッチテーブルへのポインターが含まれています。 wsk アプリケーションは wsk ソケットの作成や wsk クライアントオブジェクトに対するその他の操作を実行するために使用できます。 Wsk\_PROVIDER\_ディスパッチ関数を使用して WSK アプリケーションを終了した後は、 [**WskReleaseProviderNPI**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wsk/nf-wsk-wskreleaseprovidernpi)を呼び出して wsk プロバイダー NPI を解放する必要があります。

WSK アプリケーションが WSK プロバイダー NPI をキャプチャし、それを使用してソケットを作成してから解放する方法を次のコード例に示します。

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

WSK アプリケーションは、 [**WskCaptureProviderNPI**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wsk/nf-wsk-wskcaptureprovidernpi)を複数回呼び出すことができます。 が正常に返される**WskCaptureProviderNPI**への呼び出しごとに、 [**WskReleaseProviderNPI**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wsk/nf-wsk-wskreleaseprovidernpi)への対応する呼び出しが必要です。 WSK アプリケーションは、 **WskReleaseProviderNPI**を呼び出した後に、 [**WSK\_プロバイダー\_ディスパッチ**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wsk/ns-wsk-_wsk_provider_dispatch)の関数をそれ以上呼び出すことはできません。

 

 





