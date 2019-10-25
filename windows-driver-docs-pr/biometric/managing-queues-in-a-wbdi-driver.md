---
title: WBDI ドライバーでのキューの管理
description: WBDI ドライバーでのキューの管理
ms.assetid: f0434581-8492-42e1-ae50-4114e7b8b202
keywords:
- 生体認証ドライバー WDK、キューの管理
- キューの管理 (WDK 生体認証)
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: f299272b90ccd690a5a81e965528d807f28c4ffd
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72833952"
---
# <a name="managing-queues-in-a-wbdi-driver"></a>WBDI ドライバーでのキューの管理


WBDI ドライバーは、サービスからの複数の同時要求を処理するために、少なくとも1つのキューを作成する必要があります。 UMDF を使用している場合は、キュー管理サポートを利用できます。

[WudfBioUsbSample](https://github.com/Microsoft/Windows-driver-samples/tree/master/biometrics/driver)では、CBiometricIoQueue クラスは i/o queue インターフェイスを実装します。

メソッド `CBiometricIoQueue::Initialize`では、ドライバーは、CBiometricIoQueue オブジェクトに対してクエリを行って、ドライバーがサブスクライブするイベントコールバック関数を決定するためにフレームワークが使用する[IQueueCallbackDeviceIoControl](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nn-wudfddi-iqueuecallbackdeviceiocontrol)インターフェイスへのポインターを検索します。キューに対して:

```cpp
if (SUCCEEDED(hr)) 
{
hr = this->QueryInterface(__uuidof(IUnknown), (void **)&unknown);
}
```

次に、ドライバーは[**Iwdfdevice:: CreateIoQueue**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iwdfdevice-createioqueue)を呼び出して、既定の i/o キューを構成します。

```cpp
hr = FxDevice->CreateIoQueue(unknown,
FALSE,
WdfIoQueueDispatchParallel,
FALSE,
FALSE,
&fxQueue);
BiometricSafeRelease(unknown);
```

この呼び出しでは、要求が使用可能になるとすぐに、フレームワークがドライバーの i/o キューコールバック関数に要求を提示するように、WdfIoQueueDispatchParallel を指定します。

次に、ドライバーは[**Iwdfdevice:: ConfigureRequestDispatching**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iwdfdevice-configurerequestdispatching)を呼び出して、すべてのデバイス i/o 要求をフィルター処理するようにキューを構成します。

```cpp
hr = FxDevice->ConfigureRequestDispatching(fxQueue,
WdfRequestDeviceIoControl,
TRUE);
```

ドライバーはこの呼び出しで WdfRequestDeviceIoControl を指定しているため、フレームワークからの i/o 通知を処理する[**OnDeviceIoControl**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iqueuecallbackdeviceiocontrol-ondeviceiocontrol)ハンドラーを提供します。 これは、以前の CreateIoQueue の呼び出しの "unknown" パラメーターの一部である**IQueueCallbackDeviceIoControl:: OnDeviceIoControl**メソッドで実行されます。

[**生体認証\_\_** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/winbio_ioctl/ni-winbio_ioctl-ioctl_biometric_capture_data)の未処理の IOCTL は、一度に1つの\_データ要求をキャプチャすることだけができます。 ドライバーは、保留中の要求へのポインターを内部的に保持するか、別のフレームワークキューを使用してそれらの要求を処理することによって、データ要求\_キャプチャ\_IOCTL\_生体認証を追跡する必要があります。

このサンプルでは、保留中の i/o 要求がある場合、CBiometricDevice で定義されているように、このサンプルでは、要求へのポインターを、このクラスのメンバーに保持します。

```cpp
IWDFIoRequest *m_PendingRequest;
```

1つのセンサーデータ収集 i/o が保留中ですが、その後のデータコレクション Ioctl への呼び出しは失敗します。

```cpp
FxRequest->Complete(WINBIO_E_DATA_COLLECTION_IN_PROGRESS);
```

キャプチャ要求が完了するか取り消されると、この値は**NULL**に設定されます。

```cpp
IWDFIoRequest *FxRequest = (IWDFIoRequest *)InterlockedExchangePointer((PVOID *)&m_PendingRequest, NULL);
```

 

 





