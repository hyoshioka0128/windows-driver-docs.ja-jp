---
title: WBDI ドライバーでキューを管理します。
description: WBDI ドライバーでキューを管理します。
ms.assetid: f0434581-8492-42e1-ae50-4114e7b8b202
keywords:
- 生体認証ドライバー WDK、キューを管理します。
- キュー WDK 生体認証を管理します。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: cd717b6b621fca0da0c9a4c2bb4d4573651f4f44
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56530301"
---
# <a name="managing-queues-in-a-wbdi-driver"></a>WBDI ドライバーでキューを管理します。


WBDI ドライバーでは、サービスから複数の同時要求を処理するために少なくとも 1 つのキューを作成する必要があります。 UMDF を使用している場合、キューの管理サポートの利用できます。

[WudfBioUsbSample](https://github.com/Microsoft/Windows-driver-samples/tree/master/biometrics/driver)、CBiometricIoQueue クラスは、I/O キューのインターフェイスを実装します。

メソッドで`CBiometricIoQueue::Initialize`、具体的には、ドライバーへのポインターを所有している CBiometricIoQueue オブジェクトのクエリ実行、 [IQueueCallbackDeviceIoControl](https://msdn.microsoft.com/library/windows/hardware/ff556852)フレームワークがイベントのコールバック関数の決定に使用するインターフェイスドライバーは、キューをサブスクライブします。

```cpp
if (SUCCEEDED(hr)) 
{
hr = this->QueryInterface(__uuidof(IUnknown), (void **)&unknown);
}
```

そのドライバー呼び出し[ **IWDFDevice::CreateIoQueue** ](https://msdn.microsoft.com/library/windows/hardware/ff557020)既定の I/O キューを構成します。

```cpp
hr = FxDevice->CreateIoQueue(unknown,
FALSE,
WdfIoQueueDispatchParallel,
FALSE,
FALSE,
&fxQueue);
BiometricSafeRelease(unknown);
```

呼び出しでは、要求を利用するとすぐに、ドライバーの I/O キューのコールバック関数への要求が表示されます、framework ように WdfIoQueueDispatchParallel を指定します。

次に、ドライバーを呼び出す[ **IWDFDevice::ConfigureRequestDispatching** ](https://msdn.microsoft.com/library/windows/hardware/ff557014)をすべてのデバイスの I/O 要求をフィルター処理するキューを構成します。

```cpp
hr = FxDevice->ConfigureRequestDispatching(fxQueue,
WdfRequestDeviceIoControl,
TRUE);
```

ドライバーでは、この呼び出しで WdfRequestDeviceIoControl を指定します、ため、提供、 [ **OnDeviceIoControl** ](https://msdn.microsoft.com/library/windows/hardware/ff556854)フレームワークからの I/O の通知を処理するハンドラー。 これでは、 **IQueueCallbackDeviceIoControl::OnDeviceIoControl**以前 CreateIoQueue への呼び出しで「不明」のパラメーターの一部であるメソッド。

のみ考え未処理[ **IOCTL\_生体認証の\_キャプチャ\_データ**](https://msdn.microsoft.com/library/windows/hardware/ff536429)時に要求します。 ドライバーは、IOCTL を追跡する必要があります\_生体認証の\_キャプチャ\_データ要求、内部的に保留中の要求へのポインターを保持することで、またはそれらの要求を処理するために別のフレームワークのキューを使用して、いずれか。

サンプルでは、保留中の I/O 要求がある場合、サンプルは、CBiometricDevice クラスのメンバーでは、要求へのポインター Device.h で定義されています。

```cpp
IWDFIoRequest *m_PendingRequest;
```

1 つのセンサー データ コレクション I/O は保留中ですが、データ コレクションに後続の呼び出し Ioctl が失敗します。

```cpp
FxRequest->Complete(WINBIO_E_DATA_COLLECTION_IN_PROGRESS);
```

この値に設定のキャプチャ要求が完了またはキャンセル時**NULL**:

```cpp
IWDFIoRequest *FxRequest = (IWDFIoRequest *)InterlockedExchangePointer((PVOID *)&m_PendingRequest, NULL);
```

 

 





