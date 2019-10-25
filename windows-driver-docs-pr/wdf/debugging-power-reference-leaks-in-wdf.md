---
title: WDF での電源参照リークのデバッグ
description: Windows Driver Framework (WDF) ドライバーが WdfDeviceStopIdle を呼び出すと、フレームワークによってデバイスの電源参照カウントがインクリメントされます。
ms.assetid: 25F4EEBB-4733-498C-8704-8E015F81FE06
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 58e2d1cda1ba2cdd6f4e21283b7063cf16f8d5bb
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72844674"
---
# <a name="debugging-power-reference-leaks-in-wdf"></a>WDF での電源参照リークのデバッグ


Windows Driver Framework (WDF) ドライバーが[**Wdfdevicestopidle**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdevicestopidle)を呼び出すと、フレームワークによってデバイスの電源参照カウントがインクリメントされます。 **Wdfdevicestopidle**への呼び出しが成功するたびに、 [**WdfDeviceResumeIdle**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdeviceresumeidle)の呼び出しによって、電源参照カウントがデクリメントされる必要があります。

カーネルモードドライバーフレームワーク (KMDF) 1.15 およびユーザーモードドライバーフレームワーク (UMDF) 2.15 以降では、 [ **! wdfkd**](https://docs.microsoft.com/windows-hardware/drivers/debugger/-wdfkd-wdfdevice)および[ **! wdfkd**](https://docs.microsoft.com/windows-hardware/drivers/debugger/-wdfkd-wdftagtracker) (wd) デバッガー拡張機能を使用して、power reference の使用状況を監視できます。 パフォーマンス上の理由から、この機能は既定で無効になっているので、WdfVerifier アプリケーションで有効にするか、ドライバーのサービスキーを手動で編集する必要があります。

## <a name="wdfverifier"></a>WdfVerifier


ドライバーの設定リストを開き、 **Trackpower**設定を右クリックします。 シナリオに適したオプションを選択します。

**ヒント**  パフォーマンスが重要なコードパスでスタックトレースをキャプチャしないようにします。

 

![wdfverifier での電源参照の追跡の設定](images/wdfverifier--track-power-references-on.png)

## <a name="editing-the-registry"></a>レジストリの編集


また、ドライバーのサービスキーを編集して、検証機能のサポートと電源参照の追跡を有効にすることもできます。

KMDF ドライバーの場合:

**HKLM\\SYSTEM\\ControlSet001\\Services\\&lt;ドライバーサービス名&gt;\\パラメーター\\Wdf**

UMDF ドライバーの場合:

**HKLM\\ソフトウェア\\Microsoft\\Windows NT\\CurrentVersion\\WUDF\\Services\\&lt;Driver Service Name&gt;\\Parameters\\Wdf**

```cpp
(REG_DWORD) VerifierOn = 0x1
(REG_DWORD) TrackPower = 0x0 (disabled)
                       = 0x1 (capture tick count, file name, line number)
                       = 0x2 (capture tick count, file name, line number, and stack traces)
```

## <a name="driver-code"></a>ドライバーコード


ドライバーは、次のように、 [**Wdfdevicestopidle**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdevicestopidle)と[**WdfDeviceResumeIdle**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdeviceresumeidle)を呼び出して、デバイスの動作中の電源状態を管理します。

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

## <a name="debugging-with-wdfkd"></a>WdfKd を使用したデバッグ


デバイスで作成された電源参照と、参照履歴を示すタグトラッカーを表示するには、次のように、 [ **! wdfkd. wdfkd**](https://docs.microsoft.com/windows-hardware/drivers/debugger/-wdfkd-wdfdevice) verbose フラグを使用します。

```cpp
kd> !wdfkd.wdfdevice 0x6d939790 ff
Power references: 0 !wdftagtracker 0x9ea030a8
```

[ **! Wdfkd. wdftagtracker**](https://docs.microsoft.com/windows-hardware/drivers/debugger/-wdfkd-wdftagtracker)を呼び出すと、デバイスの電源参照履歴が表示されます。

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

## <a name="specifying-a-tag"></a>タグの指定


必要に応じて、特定の電源参照の識別を容易にするタグ名を指定します。 これを行うには、 [**WdfDeviceStopIdleWithTag**](https://docs.microsoft.com/windows-hardware/drivers/wdf/wdfdevicestopidlewithtag)と[**WdfDeviceResumeIdleWithTag**](https://docs.microsoft.com/windows-hardware/drivers/wdf/wdfdeviceresumeidlewithtag)を使用します。

```cpp
status = WdfDeviceStopIdleWithTag(device, FALSE, (PVOID)'oyeH');
if (NT_SUCCESS(status)) {
    WdfDeviceResumeIdleWithTag(device, (PVOID)'oyeH');
}
```

対応する[ **! wdftagtracker**](https://docs.microsoft.com/windows-hardware/drivers/debugger/-wdfkd-wdftagtracker)サンプル出力:

```cpp
(--) 0 ref: Tag 'Heyo' at Time 0x24e40 ticks
##      path\to\your\driver\code.c @ 374

(++) 1 refs: Tag 'Heyo' at Time 0x24e40 ticks
##      path\to\your\driver\code.c @ 372

(++) Initial Tag '....' at Time 0x12c9a ticks
```

 

 





