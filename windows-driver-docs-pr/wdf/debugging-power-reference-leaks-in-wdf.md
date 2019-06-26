---
title: WDF での電源参照リークのデバッグ
description: Windows Driver Frameworks (WDF) ドライバー呼び出し WdfDeviceStopIdle ときに、フレームワークは、デバイスの電源の参照カウントをインクリメントします。
ms.assetid: 25F4EEBB-4733-498C-8704-8E015F81FE06
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d66337d9180fb9d3233a49b684409dc64e14c50e
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67377493"
---
# <a name="debugging-power-reference-leaks-in-wdf"></a>WDF での電源参照リークのデバッグ


Windows Driver Frameworks (WDF) ドライバーを呼び出すと[ **WdfDeviceStopIdle**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nf-wdfdevice-wdfdevicestopidle)フレームワークは、デバイスの電源の参照カウントをインクリメントします。 すべての成功した呼び出し**WdfDeviceStopIdle**への呼び出しで一致する必要があります[ **WdfDeviceResumeIdle** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nf-wdfdevice-wdfdeviceresumeidle) power 参照カウントをデクリメントします。

カーネル モード ドライバー フレームワーク (KMDF) 1.15 とユーザー モード ドライバー フレームワーク (UMDF) 2.15 以降、監視できます power 参照の使用方法を使用して、 [ **! wdfkd.wdfdevice** ](https://docs.microsoft.com/windows-hardware/drivers/debugger/-wdfkd-wdfdevice)と[ **! wdfkd.wdftagtracker** ](https://docs.microsoft.com/windows-hardware/drivers/debugger/-wdfkd-wdftagtracker)デバッガーの拡張機能。 WdfVerifier アプリケーションまたはドライバーのサービス キーを手動で編集してにオンにする必要があるために、パフォーマンス上の理由から、既定でこの機能が無効です。

## <a name="wdfverifier"></a>WdfVerifier


右クリックして、ドライバーの設定一覧を開き、 **TrackPower**設定します。 シナリオに適したオプションを選択します。

**ヒント:**   パフォーマンス クリティカルなコード パスでスタック トレースをキャプチャしないようにします。

 

![wdfverifier でトラック power 参照の設定](images/wdfverifier--track-power-references-on.png)

## <a name="editing-the-registry"></a>レジストリの編集


ドライバーのサービス キーを編集して追跡 Verifier サポートと電源の参照を有効することもできます。

KMDF ドライバー。

**HKLM\\システム\\ControlSet001\\サービス\\&lt;ドライバー サービス名&gt;\\パラメーター\\Wdf**

UMDF ドライバー。

**HKLM\\ソフトウェア\\Microsoft\\Windows NT\\CurrentVersion\\WUDF\\サービス\\&lt;ドライバー サービス名&gt;\\パラメーター\\Wdf**

```cpp
(REG_DWORD) VerifierOn = 0x1
(REG_DWORD) TrackPower = 0x0 (disabled)
                       = 0x1 (capture tick count, file name, line number)
                       = 0x2 (capture tick count, file name, line number, and stack traces)
```

## <a name="driver-code"></a>ドライバーのコード


ドライバー呼び出し[ **WdfDeviceStopIdle** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nf-wdfdevice-wdfdevicestopidle)と[ **WdfDeviceResumeIdle** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nf-wdfdevice-wdfdeviceresumeidle)デバイス管理の作業の電源状態次のようにします。

```cpp
//
// Take power reference
//
status = WdfDeviceStopIdle(device, FALSE);
if (NT_SUCCESS(status)) {
    //
    // Release power reference
    //
    WdfDeviceResumeIdle(device);
}
```

## <a name="debugging-with-wdfkd"></a>WdfKd でのデバッグ


タグの追跡ツールの参照の履歴が表示されるほか、デバイスで実行される電源の参照を表示する使用[ **! wdfkd.wdfdevice** ](https://docs.microsoft.com/windows-hardware/drivers/debugger/-wdfkd-wdfdevice)フラグの詳細。

```cpp
kd> !wdfkd.wdfdevice 0x6d939790 ff
Power references: 0 !wdftagtracker 0x9ea030a8
```

呼び出す、 [ **! wdfkd.wdftagtracker** ](https://docs.microsoft.com/windows-hardware/drivers/debugger/-wdfkd-wdftagtracker)デバイスの電源の参照の履歴を表示します。

```cpp
kd> !wdftagtracker 0x9ea030a8
Reference and Release History:
# (showing most recent first; refcount is approximate in multi-threaded scenarios)

## 3 entries, history depth is 25

(--) 0 ref: Tag '....' at Time 0x1331e ticks
##      path\to\your\driver\code.c @ 374

(++) 1 refs: Tag '....' at Time 0x1331e ticks
##      path\to\your\driver\code.c @ 372

(++) Initial Tag '....' at Time 0x12c9a ticks
```

## <a name="specifying-a-tag"></a>タグを指定します。


必要に応じて、特定の電源の参照の id を容易にタグ名を指定します。 これを行うには、使用[ **WdfDeviceStopIdleWithTag** ](https://docs.microsoft.com/windows-hardware/drivers/wdf/wdfdevicestopidlewithtag)と[ **WdfDeviceResumeIdleWithTag**](https://docs.microsoft.com/windows-hardware/drivers/wdf/wdfdeviceresumeidlewithtag):

```cpp
status = WdfDeviceStopIdleWithTag(device, FALSE, (PVOID)'oyeH');
if (NT_SUCCESS(status)) {
    WdfDeviceResumeIdleWithTag(device, (PVOID)'oyeH');
}
```

対応する[ **! wdftagtracker** ](https://docs.microsoft.com/windows-hardware/drivers/debugger/-wdfkd-wdftagtracker)サンプル出力。

```cpp
(--) 0 ref: Tag 'Heyo' at Time 0x24e40 ticks
##      path\to\your\driver\code.c @ 374

(++) 1 refs: Tag 'Heyo' at Time 0x24e40 ticks
##      path\to\your\driver\code.c @ 372

(++) Initial Tag '....' at Time 0x12c9a ticks
```

 

 





