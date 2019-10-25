---
title: オーディオ デバイス クラスの無通信タイマーの実装
description: オーディオ デバイス クラスの無通信タイマーの実装
ms.assetid: e7e431ec-626d-4fdb-8705-fc5420c43f17
keywords:
- 非アクティブタイマー WDK オーディオ
- タイマー WDK オーディオ
- 電力アイドル検出 WDK オーディオ
- アイドル状態の電源 (WDK audio)
- アイドルタイムアウト WDK オーディオ
- タイムアウト間隔 WDK オーディオ
- 省電力モード WDK オーディオ
- 省電力モード WDK オーディオ
- パフォーマンスモード WDK オーディオ
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: f9042e8bb5a27b05b5986a2571323f99ade4ded8
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72831370"
---
# <a name="audio-device-class-inactivity-timer-implementation"></a>オーディオ デバイス クラスの無通信タイマーの実装


## <span id="audio_device_class_inactivity_timer_implementation"></span><span id="AUDIO_DEVICE_CLASS_INACTIVITY_TIMER_IMPLEMENTATION"></span>


Windows Server 2003 SP1、Windows XP SP2 以降では、PortCls システムドライバーは、システムの電源アイドル検出機能を利用して、オーディオクライアントの非アクティブタイマーを実装します。 PortCls は、初期化時に2つのタイムアウト値と必要なアイドル電源状態をタイマーにプログラムします。 PortCls は、デバイスのすべてのアクセス (i/o やプロパティアクセスなど) を監視し、各アクセスのタイマーカウントを効果的にリセットします。 タイマーがタイムアウトした場合、システムはデバイスを望ましいアイドル状態にするように電源 IRP を要求します。 デバイスがアイドル状態になると、PortCls は新しいアクセスアクティビティが発生した場合にデバイスの電源を入れます。

PortCls には、アイドルタイムアウトとアイドル状態の電源のためのハードコーディングされた既定値が含まれています。 ハードウェアベンダーは、必要に応じて、システムレジストリのドライバー固有のキーに独自の値を書き込むことによって既定値を上書きできます。 これにより、ベンダーは、デバイスに最適な電力アイドル状態のパラメーター値を選択できます。

ベンダーは、次の電源アイドルパラメーターの既定値を上書きできます。

-   *ConservationIdleTime*

    このパラメーターは、システムが電力保護モードで実行されている場合のアイドルタイムアウト間隔を指定します。 これは、システムがバッテリ電源で動作しているときに通常使用されるモードです。 このパラメーターの既定値は0で、節約モードでの電源アイドルタイマーを無効にします。 ハードウェアベンダーは、次のドライバー固有のレジストリキーに DWORD 値を書き込むことによって、既定値を上書きできます。

    ```inf
    \HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\Class\xxxx\yyyy\PowerSettings\ConservationIdleTime
    ```

    *Xxxx*は、メディアクラス guid を表します ([システムによって提供されるデバイスセットアップクラス](https://docs.microsoft.com/previous-versions/ff553419(v=vs.85))を参照してください)。 *YYYY*は、メディアクラス guid の下にあるドライバーのサブキーの名前を表します。 キーの値は、タイムアウト間隔を秒単位で指定します。

-   *PerformanceIdleTime*

    このパラメーターは、システムがパフォーマンスモードで実行されている場合のアイドルタイムアウト間隔を指定します。 これは、システムが AC 電源で実行されている場合に通常使用されるモードです。 このパラメーターの既定値は0で、パフォーマンスモードでの電源アイドルタイマーを無効にします。 ハードウェアベンダーは、次のドライバー固有のレジストリキーに DWORD 値を書き込むことによって、既定値を上書きできます。

    ```inf
    \HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\Class\xxxx\yyyy\PowerSettings\PerformanceIdleTime
    ```

    ここでも、 *xxxx*は MEDIA クラス GUID を表し、 *yyyy*はドライバーのサブキーの名前を表します。 キーの値は、タイムアウト間隔を秒単位で指定します。

-   *IdlePowerState*

    このパラメーターは、アイドルタイムアウト期間が経過した場合にデバイスが配置される電源状態を指定します。 このパラメーターの既定値は0で、デバイスの電源状態の D0 (フルパワー) に対応しています。 ハードウェアベンダーは、次のドライバー固有のレジストリキーに DWORD 値を書き込むことによって、既定値を上書きできます。

    ```inf
    \HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\Class\xxxx\yyyy\PowerSettings\IdlePowerState
    ```

    ここでも、 *xxxx*は MEDIA クラス GUID を表し、 *yyyy*はドライバーのサブキーの名前を表します。 キーに格納される値は、デバイスの電源状態の D0、D1、D2、または D3 にそれぞれ対応する0、1、2、または3である必要があります。

この3つの電源アイドルレジストリキーは、デバイスインストールの INF ファイルによって作成された場合にのみ存在します。 PortCls は、電源アイドルタイマーを構成する前に、ドライバー固有の電源アイドルパラメーターをレジストリから取得しようとします。 PortCls は、レジストリ内で検出されない電源アイドルパラメーターの代わりに既定値を使用します。 前に説明したように、既定の電源アイドルパラメーター値はアイドルタイマーを無効にします。

*ConservationIdleTime*、 *PerformanceIdleTime*、および*IdlePowerState*パラメーターの指定の詳細については、 [**PoRegisterDeviceForIdleDetection**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-poregisterdeviceforidledetection)の最後の3つの呼び出しパラメーターの定義を参照してください。

### <a name="span-idexamplespanspan-idexamplespan-example"></a><span id="example"></span><span id="EXAMPLE"></span>よう

たとえば、ハードウェアベンダーは、オーディオデバイスに対して、 *ConservationIdleTime* = 0x0000001e (30 秒)、 *PerformanceIdleTime* = 0x0000012c (300 秒)、および*IdlePowerState* = の各電源アイドルパラメーターを指定することができます。0x00000003 (デバイスの電源状態 D3)。 これらの設定を有効にするために、デバイスインストールファイルには、次のディレクティブを含む[**INF AddReg セクション**](https://docs.microsoft.com/windows-hardware/drivers/install/inf-addreg-directive)を含めることができます。

```inf
[MyAudioDevice.AddReg]
HKR,PowerSettings,ConservationIdleTime,1,1e,00,00,00
HKR,PowerSettings,PerformanceIdleTime,1,2c,01,00,00
HKR,PowerSettings,IdlePowerState,1,03,00,00,00
```

HKR は、レジストリ内のドライバーのルートキーを表します。

```inf
\HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\Class\xxxx\yyyy
```

ここでも、 *xxxx*は MEDIA クラス GUID を表し、 *yyyy*はドライバーのサブキーの名前を表します。 **Powersettings**サブキーは、ルートキーのパス名に対して相対的に指定されます。

 

 




