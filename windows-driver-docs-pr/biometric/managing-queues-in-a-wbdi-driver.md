---
title: WBDI ドライバーでのキューの管理
description: WBDI ドライバーでのキューの管理
ms.assetid: f0434581-8492-42e1-ae50-4114e7b8b202
keywords:
- 生体認証ドライバー WDK、キューを管理します。
- キュー WDK 生体認証を管理します。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 37351b27d8ca02c4def553b19131f09425ce6b60
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67364690"
---
# <a name="managing-queues-in-a-wbdi-driver"></a>WBDI ドライバーでのキューの管理


WBDI ドライバーでは、サービスから複数の同時要求を処理するために少なくとも 1 つのキューを作成する必要があります。 UMDF を使用している場合、キューの管理サポートの利用できます。

[WudfBioUsbSample](https://github.com/Microsoft/Windows-driver-samples/tree/master/biometrics/driver)、CBiometricIoQueue クラスは、I/O キューのインターフェイスを実装します。

メソッドで`CBiometricIoQueue::Initialize`、具体的には、ドライバーへのポインターを所有している CBiometricIoQueue オブジェクトのクエリ実行、 [IQueueCallbackDeviceIoControl](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nn-wudfddi-iqueuecallbackdeviceiocontrol)フレームワークがイベントのコールバック関数の決定に使用するインターフェイスドライバーは、キューをサブスクライブします。

```cpp
if (SUCCEEDED(hr)) 
{
hr = this->QueryInterface(__uuidof(IUnknown), (void **)&unknown);
}
```

そのドライバー呼び出し[ **IWDFDevice::CreateIoQueue** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nf-wudfddi-iwdfdevice-createioqueue)既定の I/O キューを構成します。

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

次に、ドライバーを呼び出す[ **IWDFDevice::ConfigureRequestDispatching** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nf-wudfddi-iwdfdevice-configurerequestdispatching)をすべてのデバイスの I/O 要求をフィルター処理するキューを構成します。

```cpp
hr = FxDevice->ConfigureRequestDispatching(fxQueue,
WdfRequestDeviceIoControl,
TRUE);
```

ドライバーでは、この呼び出しで WdfRequestDeviceIoControl を指定します、ため、提供、 [ **OnDeviceIoControl** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nf-wudfddi-iqueuecallbackdeviceiocontrol-ondeviceiocontrol)フレームワークからの I/O の通知を処理するハンドラー。 これでは、 **IQueueCallbackDeviceIoControl::OnDeviceIoControl**以前 CreateIoQueue への呼び出しで「不明」のパラメーターの一部であるメソッド。

のみ考え未処理[ **IOCTL\_生体認証の\_キャプチャ\_データ**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/winbio_ioctl/ni-winbio_ioctl-ioctl_biometric_capture_data)時に要求します。 ドライバーは、IOCTL を追跡する必要があります\_生体認証の\_キャプチャ\_データ要求、内部的に保留中の要求へのポインターを保持することで、またはそれらの要求を処理するために別のフレームワークのキューを使用して、いずれか。

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

 

 





