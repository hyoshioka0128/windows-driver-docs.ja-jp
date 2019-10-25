---
title: WBDI ドライバーでの WinUSB の使用
description: WBDI ドライバーでの WinUSB の使用
ms.assetid: a2f109cd-cb61-4c63-8e93-111f62a2c02d
keywords:
- 生体認証ドライバー WDK、WinUSB
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: db1906e4202fba1cd20f319fa51f5da2edb1c51c
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72833911"
---
# <a name="using-winusb-in-a-wbdi-driver"></a>WBDI ドライバーでの WinUSB の使用


WBDI ドライバーでは、ユーザーモードドライバーフレームワーク (UMDF) に組み込まれている[USB i/o ターゲット](https://docs.microsoft.com/windows-hardware/drivers/wdf/usb-i-o-targets-in-umdf)を使用することをお勧めします。

### <a name="span-idsetting_umdfdispatcherspanspan-idsetting_umdfdispatcherspansetting-umdfdispatcher"></a><span id="setting_umdfdispatcher"></span><span id="SETTING_UMDFDISPATCHER"></span>UmdfDispatcher の設定

UMDF ドライバーをインストールする INF ファイルには、WDF 固有の**Ddinstall**セクションが含まれている必要があります。 UMDF で USB i/o ターゲットを使用する場合は、この**Ddinstall**セクション内で UmdfDispatcher registry ディレクティブを設定する必要があります。

[WudfBioUsbSample](https://github.com/Microsoft/Windows-driver-samples/tree/master/biometrics/driver)サンプルの WudfBioUsbSample の次のセクションは、このディレクティブの設定方法を示しています。

```cpp
[Biometric_Install.NT.Wdf]
KmdfService=WINUSB, WinUsb_Install
UmdfDispatcher=WinUsb
UmdfService=WudfBioUsbSample, WudfBioUsbSample_Install
UmdfServiceOrder=WudfBioUsbSample
```

UmdfDispatcher の具体的な情報については、「 [UMDFDISPATCHER INF ディレクティブの指定](https://docs.microsoft.com/windows-hardware/drivers/wdf/specifying-wdf-directives-in-inf-files)」を参照してください。 WDF registry ディレクティブに関する一般的な情報については、「 [WDF ディレクティブの指定](https://docs.microsoft.com/windows-hardware/drivers/wdf/specifying-wdf-directives-in-inf-files)」を参照してください。

### <a name="span-idpending_asynchronous_read_requestsspanspan-idpending_asynchronous_read_requestsspanpending-asynchronous-read-requests"></a><span id="pending_asynchronous_read_requests"></span><span id="PENDING_ASYNCHRONOUS_READ_REQUESTS"></span>保留中の非同期読み取り要求

WinUsb では、複数の未処理の読み取り要求を処理できます。 スキャン中に読み取り操作間の待機時間を最小限にする必要があるデバイスは、いくつかの未処理の非同期読み取り要求を保留状態のままにしておく必要があります。 ドライバーが非同期要求を行う場合、WinUsb は、前の読み取り要求の完了ルーチンのユーザーモードへの転送前に、これらの要求を発行します。

[WudfBioUsbSample](https://github.com/Microsoft/Windows-driver-samples/tree/master/biometrics/driver)の `CBiometricDevice::InitiatePendingRead` メソッドを参照して、読み取り要求を保留する方法のコード例を確認できます。

読み取り要求を保留するコードは、次の手順のループにする必要があります。

1.  [**Iwdfdriver:: CreatePreallocatedWdfMemory**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iwdfdriver-createpreallocatedwdfmemory)を呼び出して、事前に割り当てられたフレームワークメモリオブジェクトを作成します。

2.  [**Oncompletion**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-irequestcallbackrequestcompletion-oncompletion)ルーチンでコールバックコードを指定します。 このサンプルの「`CBiometricDevice::OnCompletion`」を参照してください。

3.  所有しているオブジェクトの[**Irequestの要求完了**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nn-wudfddi-irequestcallbackrequestcompletion)インターフェイスへのポインターを取得します。

4.  [**IWDFIoRequest:: Setcompletion callback**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iwdfiorequest-setcompletioncallback)を呼び出し、前の手順で取得した[**irequestcallbackrequestcompletion**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nn-wudfddi-irequestcallbackrequestcompletion)へのポインターを渡すことによって、コールバック関数を登録します。 これで、i/o 要求が完了すると、フレームワークはコールバックを呼び出します。

5.  [**IWDFIoRequest:: Send**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iwdfiorequest-send)を呼び出して、読み取り要求をデバイスに送信します。

6.  コールバックの完了時に読み取り要求を処理します。 [**Oncompletion**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-irequestcallbackrequestcompletion-oncompletion)ルーチンは、保留中の新しい読み取り要求を開始する前に、i/o ターゲットの状態を確認する必要があります。 これを行うには、 [IWDFIoTargetStateManagement](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nn-wudfddi-iwdfiotargetstatemanagement)インターフェイスへのポインターに対して[IWDFUsbTargetPipe](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfusb/nn-wudfusb-iwdfusbtargetpipe)をクエリします。 次に、 [**IWDFIoTargetStateManagement:: GetState**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iwdfiotargetstatemanagement-getstate)を呼び出します。
    ```cpp
    IWDFIoTarget * pTarget
    IWDFIoTargetStateManagement * pStateMgmt = NULL;
    WDF_IO_TARGET_STATE state;

    HRESULT hrQI = pTarget->QueryInterface(IID_PPV_ARGS(&pStateMgmt));
    WUDF_TEST_DRIVER_ASSERT((SUCCEEDED(hrQI) && pStateMgmt));

    state = pStateMgmt->GetState();
    ```

スキャンが完了したら、保留中の読み取り要求を取り消します。

UMDF USB ターゲットを使用している場合は、電源を入れながら電源を入れて、読み取り要求を保留したままにすることができます。

UMDF USB ターゲットを使用しない場合、ドライバーは D0Exit で保留中の読み取り要求の送信を停止し、D0Entry で再起動する必要があります。

### <a name="span-idselective_suspendspanspan-idselective_suspendspanselective-suspend"></a><span id="selective_suspend"></span><span id="SELECTIVE_SUSPEND"></span>選択的中断

WBDI ドライバーは、 [USB のセレクティブサスペンド](../usbcon/usb-selective-suspend.md)をサポートする必要があります。

システムのスリープとデバイスのアイドル状態をサポートするデバイスでは、次の WudfBioUsbSample のコード例に示すように、WinUsb でのセレクティブサスペンドのレジストリ設定を有効にする必要があります。

```cpp
HKR,,"SystemWakeEnabled",0x00010001,1
HKR,,"DeviceIdleEnabled",0x00010001,1
```

オペレーティングシステムの USB スタックは、システムのスリープ解除と、ドライバーがデバイスからの読み取りを開始できるタイミングを保証できません。

理想的には、デバイスは、システムが中断されたときにスキャンをキャプチャする準備ができている状態のままにしておく必要があります。 システムが中断されている間にスキャンが実行された場合、デバイスは、指紋スキャン全体の入力データをキャッシュする必要があります。 システムが起動すると、ドライバーはデバイスからデータを読み取ります。 このシナリオをサポートすることで、システムのスリープ解除とロック解除/ログインのシナリオを有効にすることができます。

 

 





