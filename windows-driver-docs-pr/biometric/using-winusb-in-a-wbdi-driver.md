---
title: WBDI ドライバーでの WinUSB の使用
description: WBDI ドライバーでの WinUSB の使用
ms.assetid: a2f109cd-cb61-4c63-8e93-111f62a2c02d
keywords:
- 生体認証ドライバー WDK、WinUSB
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 88e7667e3a7b36638937af29cb4efd69fc1a52d9
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67354061"
---
# <a name="using-winusb-in-a-wbdi-driver"></a>WBDI ドライバーでの WinUSB の使用


Microsoft WBDI ドライバーを使用することをお勧め、 [USB I/O ターゲット](https://docs.microsoft.com/windows-hardware/drivers/wdf/usb-i-o-targets-in-umdf)ユーザー モード ドライバー フレームワーク (UMDF) には構築されています。

### <a name="span-idsettingumdfdispatcherspanspan-idsettingumdfdispatcherspansetting-umdfdispatcher"></a><span id="setting_umdfdispatcher"></span><span id="SETTING_UMDFDISPATCHER"></span>UmdfDispatcher の設定

UMDF ドライバーをインストールする INF ファイルは、特定の WDF を含める必要があります**DDInstall**セクション。 UMDF で USB I/O ターゲットを使用する場合は、この UmdfDispatcher レジストリ ディレクティブを設定する必要があります**DDInstall**セクション。

次のセクションで WudfBioUsbSample.inx から、 [WudfBioUsbSample](https://github.com/Microsoft/Windows-driver-samples/tree/master/biometrics/driver)サンプルは、このディレクティブを設定する方法を示します。

```cpp
[Biometric_Install.NT.Wdf]
KmdfService=WINUSB, WinUsb_Install
UmdfDispatcher=WinUsb
UmdfService=WudfBioUsbSample, WudfBioUsbSample_Install
UmdfServiceOrder=WudfBioUsbSample
```

UmdfDispatcher 詳細については、次を参照してください。 [UmdfDispatcher INF ディレクティブの指定](https://docs.microsoft.com/windows-hardware/drivers/wdf/specifying-wdf-directives-in-inf-files)します。 WDF レジストリ ディレクティブについては、次を参照してください。 [WDF ディレクティブを指定する](https://docs.microsoft.com/windows-hardware/drivers/wdf/specifying-wdf-directives-in-inf-files)します。

### <a name="span-idpendingasynchronousreadrequestsspanspan-idpendingasynchronousreadrequestsspanpending-asynchronous-read-requests"></a><span id="pending_asynchronous_read_requests"></span><span id="PENDING_ASYNCHRONOUS_READ_REQUESTS"></span>保留中の非同期読み取り要求

WinUsb には、複数の未処理の読み取り要求を処理できます。 スキャン中に読み取り操作の間の最小限の待機時間を必要とするデバイスは、いくつかの保留中の未処理の非同期読み取り要求を保持する必要があります。 ドライバーは、非同期要求を行う、WinUsb は以前の読み取り要求の完了ルーチンのユーザー モードに戻す、転送する前にこれらの要求を発行します。

参照することができます、`CBiometricDevice::InitiatePendingRead`メソッドで Device.cpp [WudfBioUsbSample](https://github.com/Microsoft/Windows-driver-samples/tree/master/biometrics/driver)に読み取り要求を保留する方法のコード例を参照してください。

読み取り要求を保留するコードは、次の手順のループになります。

1.  呼び出して、事前に割り当てられた framework メモリ オブジェクトを作成する[ **IWDFDriver::CreatePreallocatedWdfMemory**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nf-wudfddi-iwdfdriver-createpreallocatedwdfmemory)します。

2.  コールバック コードで提供、 [ **OnCompletion** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nf-wudfddi-irequestcallbackrequestcompletion-oncompletion)ルーチン。 参照してください`CBiometricDevice::OnCompletion`サンプル。

3.  ポインターを取得、 [ **IRequestCallbackRequestCompletion** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nn-wudfddi-irequestcallbackrequestcompletion)所有するオブジェクトのインターフェイス。

4.  コールバック関数を呼び出すことによって登録[ **IWDFIoRequest::SetCompletionCallback** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nf-wudfddi-iwdfiorequest-setcompletioncallback)へのポインターを渡して[ **IRequestCallbackRequestCompletion**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nn-wudfddi-irequestcallbackrequestcompletion)前の手順で取得したものでした。 I/O 要求が完了すると、フレームワークは、コールバックを呼び出しますようになりました。

5.  呼び出す[ **IWDFIoRequest::Send** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nf-wudfddi-iwdfiorequest-send)デバイスに、読み取り要求を送信します。

6.  プロセスは、コールバックの完了が発生したときに要求を読み取る。 前に、 [ **OnCompletion** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nf-wudfddi-irequestcallbackrequestcompletion-oncompletion)ルーチンを開始する、新しい読み取り要求の保留中、I/O のターゲットの状態を確認する必要があります。 これを行うには、クエリ[IWDFUsbTargetPipe](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfusb/nn-wudfusb-iwdfusbtargetpipe)へのポインターの[IWDFIoTargetStateManagement](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nn-wudfddi-iwdfiotargetstatemanagement)インターフェイス。 呼び出して[ **IWDFIoTargetStateManagement::GetState**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nf-wudfddi-iwdfiotargetstatemanagement-getstate):
    ```cpp
    IWDFIoTarget * pTarget
    IWDFIoTargetStateManagement * pStateMgmt = NULL;
    WDF_IO_TARGET_STATE state;

    HRESULT hrQI = pTarget->QueryInterface(IID_PPV_ARGS(&pStateMgmt));
    WUDF_TEST_DRIVER_ASSERT((SUCCEEDED(hrQI) && pStateMgmt));

    state = pStateMgmt->GetState();
    ```

スキャンが完了したら、保留中の読み取り要求をキャンセルします。

UMDF USB ターゲットを使用した場合は、保留状態のままに読み取り要求を許可できます電源の間で、電源アップします。

UMDF USB ターゲットを使用しない場合ドライバーが D0Exit に読み取り要求の保留中の送信を停止し、D0Entry で再起動する必要があります。

### <a name="span-idselectivesuspendspanspan-idselectivesuspendspanselective-suspend"></a><span id="selective_suspend"></span><span id="SELECTIVE_SUSPEND"></span>選択的な中断

WBDI ドライバーをサポートする必要があります[USB のセレクティブ サスペンド](../usbcon/usb-selective-suspend.md)します。

システム スリープ解除をサポートするデバイスとデバイスがアイドル状態のレジストリ設定を有効にする必要があります選択的 WudfBioUsbSample.inx からこのコード例で示すように、WinUsb で中断します。

```cpp
HKR,,"SystemWakeEnabled",0x00010001,1
HKR,,"DeviceIdleEnabled",0x00010001,1
```

オペレーティング システムの USB スタックは、システムのスリープ解除と、ドライバーがデバイスから読み取りを開始するときのタイミングを保証できません。

理想的には、デバイスが状態のままに、システムが中断されている場合、スキャンをキャプチャする準備が。 システムが中断されている間に、スキャンが発生した場合、デバイスは、全体の指紋のスキャンの入力データをキャッシュする必要があります。 ときに、システムは、ドライバー、スリープ状態を解除し、デバイスからデータを読み取ります。 このシナリオをサポートすることでシステムのスリープ解除を有効にしてシナリオのロックを解除/ログインします。

 

 





