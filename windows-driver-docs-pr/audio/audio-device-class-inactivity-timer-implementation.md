---
title: オーディオ デバイス クラスの非アクティブ タイマーの実装
description: オーディオ デバイス クラスの非アクティブ タイマーの実装
ms.assetid: e7e431ec-626d-4fdb-8705-fc5420c43f17
keywords:
- 非アクティブ タイマーの WDK オーディオ
- タイマーの WDK オーディオ
- WDK オーディオの電力アイドル状態の検出
- アイドル状態の電源状態の WDK オーディオ
- アイドル タイムアウトの WDK オーディオ
- タイムアウト間隔の WDK オーディオ
- 電源節約モード WDK オーディオ
- この活動の電源モード WDK オーディオ
- パフォーマンスの電源モード WDK オーディオ
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 26ba356afcf9e9f9c6f2d5cb5e92985c2a1c150a
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56557312"
---
# <a name="audio-device-class-inactivity-timer-implementation"></a>オーディオ デバイス クラスの非アクティブ タイマーの実装


## <span id="audio_device_class_inactivity_timer_implementation"></span><span id="AUDIO_DEVICE_CLASS_INACTIVITY_TIMER_IMPLEMENTATION"></span>


Windows Server 2003 SP1、Windows XP SP2 で PortCls システム ドライバーが、非アクティブ タイマーのオーディオ クライアントを実装するために、システムの電力アイドル状態の検出機能を利用して後と。 PortCls プログラムの 2 つのタイムアウト値と、必要なを初期化したときに、タイマーに電源状態をアイドルです。 PortCls では、すべてのアクセスがデバイスの I/O とプロパティのアクセス) などを監視し、効果的にアクセスごとにタイマーのカウントをリセットします。 タイマーがタイムアウトした場合、システムは、必要なアイドル状態で、デバイスを配置する電源 IRP を要求します。 デバイスがアイドル状態で配置されている後、PortCls の電源がデバイスをバックアップする新しいアクセス アクティビティが発生した場合。

PortCls には、アイドル状態のタイムアウトとアイドル状態の電源の状態のハード コーディングされた既定値が含まれています。 必要に応じて、ハードウェア ベンダーは、システム レジストリ内のドライバー固有のキーを独自の値を記述することで、既定値をオーバーライドできます。 これにより、ベンダーは、自分のデバイスに最適である電力アイドル状態のパラメーター値を選択できます。

ベンダーは、次のアイドル状態の電源のパラメーターの既定値をオーバーライドできます。

-   *ConservationIdleTime*

    このパラメーターは、システムが電源保護モードで実行されている場合、アイドル状態のタイムアウト間隔を指定します。 これは、システムがバッテリ電源で実行されているときに通常使用されるモードです。 このパラメーターの既定値は 0 で、保護モードで電力アイドル タイマーを無効にします。 ハードウェア ベンダーは、DWORD 値を次のドライバー固有のレジストリ キーに記述することで、既定をオーバーライドできます。

    ```inf
    \HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\Class\xxxx\yyyy\PowerSettings\ConservationIdleTime
    ```

    なお*xxxx* Media クラス GUID を表します (を参照してください[System-Supplied デバイス セットアップ クラス](https://msdn.microsoft.com/library/windows/hardware/ff553419)) と*yyyy* Media クラスの下に、ドライバーのサブキーの名前を表しますGUID。 キーの値は、タイムアウト間隔を秒単位で指定します。

-   *PerformanceIdleTime*

    このパラメーターは、システムがパフォーマンス モードで実行されている場合、アイドル状態のタイムアウト間隔を指定します。 これは、システムが AC 電源で実行されているときに通常使用されるモードです。 このパラメーターの既定値は 0 で、パフォーマンス モードで電力アイドル タイマーを無効にします。 ハードウェア ベンダーは、DWORD 値を次のドライバー固有のレジストリ キーに記述することで、既定をオーバーライドできます。

    ```inf
    \HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\Class\xxxx\yyyy\PowerSettings\PerformanceIdleTime
    ```

    ここでも、 *xxxx* Media クラス GUID を表すと*yyyy*ドライバーのサブキーの名前を表します。 キーの値は、タイムアウト間隔を秒単位で指定します。

-   *IdlePowerState*

    このパラメーターは、アイドル状態のタイムアウト期間が終了する場合にそのデバイスがでに配置する電源状態を指定します。 既定値のこのパラメーターが 0 の場合はデバイスの電源状態 D0 (完全な電源) に対応します。 ハードウェア ベンダーは、DWORD 値を次のドライバー固有のレジストリ キーに記述することで、既定をオーバーライドできます。

    ```inf
    \HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\Class\xxxx\yyyy\PowerSettings\IdlePowerState
    ```

    ここでも、 *xxxx* Media クラス GUID を表すと*yyyy*ドライバーのサブキーの名前を表します。 0、1、2、または 3、D0 や D1、d2 に切り替わり、D3、デバイスの電源状態に対応するそれぞれのキーに指定する値があります。

デバイス インストールの INF ファイルを作成している場合にのみ、3 つの電力アイドル状態のレジストリ キーが存在します。 電力アイドル タイマーを構成する前に、PortCls はレジストリからドライバー固有の電力アイドル パラメーターを取得しようとします。 PortCls には、レジストリで見つからないすべて電力アイドル状態のパラメーターの代わりに既定値が使用されます。 以前は、既定のアイドル状態の電源を説明するよう、パラメーターの値には、アイドル タイマが無効にします。

指定の詳細については、 *ConservationIdleTime*、 *PerformanceIdleTime*、および*IdlePowerState*パラメーターは、最後の 3 つの定義を参照してください。パラメーターを呼び出し、 [ **PoRegisterDeviceForIdleDetection**](https://msdn.microsoft.com/library/windows/hardware/ff559721)します。

### <a name="span-idexamplespanspan-idexamplespan-example"></a><span id="example"></span><span id="EXAMPLE"></span> 例

たとえば、ハードウェア ベンダーは、オーディオ デバイスの次の電力アイドル パラメーターを指定する場合。*ConservationIdleTime* 0x0000001e (30 秒) = *PerformanceIdleTime* = では 0x0000012c (300 秒) と*IdlePowerState* 0x00000003 (デバイスの電源状態 D3) を = です。 これらの設定を有効にするデバイスのインストール ファイルを含めることができます、 [ **INF AddReg セクション**](https://msdn.microsoft.com/library/windows/hardware/ff546320)次のディレクティブを含みます。

```inf
[MyAudioDevice.AddReg]
HKR,PowerSettings,ConservationIdleTime,1,1e,00,00,00
HKR,PowerSettings,PerformanceIdleTime,1,2c,01,00,00
HKR,PowerSettings,IdlePowerState,1,03,00,00,00
```

HKR では、ドライバーのルートのレジストリ キーを表します。

```inf
\HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\Class\xxxx\yyyy
```

ここでも、 *xxxx* Media クラス GUID を表すと*yyyy*ドライバーのサブキーの名前を表します。 **PowerSettings**ルート キーのパス名を基準としたサブキーが指定されています。

 

 




