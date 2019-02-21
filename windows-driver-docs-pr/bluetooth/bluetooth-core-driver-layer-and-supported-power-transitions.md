---
title: Bluetooth Core ドライバー レイヤーとサポートされている電源遷移
description: 次の表では、Bluetooth core のドライバーがサポートするデバイスとシステムの電源状態をまとめたものです。
ms.assetid: 25A3598E-51A7-4B16-92F7-9D2F39177946
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 58fbf752748e57c0fe0017d902d942474d0af1e5
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56535764"
---
# <a name="bluetooth-core-driver-layer-and-supported-power-transitions"></a>Bluetooth Core ドライバー レイヤーとサポートされている電源遷移


次の表では、Bluetooth core のドライバーがサポートするデバイスとシステムの電源状態をまとめたものです。 「スリープ」状態に使用されるスループットは、このセクションと、Bluetooth 無線の内部設定と構成は永続的状態のサブトピックを非常に低電力について説明します。

<table>
    <tr>
        <td></td>
        <td></td>
        <td colspan="3"><b>デバイスの電源の状態</b></td>
    </tr>
    <tr>
        <td></td>
        <td></td>
        <td>D0 (アクティブ)</td>
        <td>D2 (スリープ) – Bluetooth チップの内部状態を保持するためにいくつかの電源が維持されます</td>
        <td>D3 (Off) の電源は、削除された (*)</td>
    </tr>
    <tr>
        <td rowspan="6"><b>システム電源の状態</b></td>
        <td>S0 (アクティブ)</td>
        <td>Active</td>
        <td>スリープ ウェイクいる場合</td>
        <td>無線 RM オフ</td>
    </tr>
    <tr>
        <td>S1</td>
        <td>なし</td>
        <td>なし</td>
        <td>なし</td>
    </tr>
    <tr>
       <td>S2</td>
        <td>なし</td>
        <td>なし</td>
        <td>なし</td>
    </tr>
    <tr>
        <td>S3 (スリープ)</td>
        <td>なし</td>
        <td>スリープ ウェイクいる場合</td>
        <td>電源がオフできます。</td>
    </tr>
    <tr>
        <td>S4 (休止)</td>
        <td>なし</td>
        <td>スリープ ウェイクいる場合</td>
        <td>電源がオフできます。</td>
    </tr>
    <tr>
        <td>S5 (オフ)</td>
        <td>なし</td>
        <td>なし</td>
        <td>電源がオフできます。</td>
    </tr>
</table>



\*電源が Bluetooth チップに失われるために、Bluetooth core ドライバーによって再初期化が必要です。

システム状態のガイドラインは、SoC システムに対するサポートします。

-   S0 (on) および S5 (シャット ダウン) のサポートがすべて Soc に必要です
-   S4 (休止状態) は x86 ベースの Soc に必要です。
-   コネクト スタンバイをサポートするシステムでは、S3 をサポートしていません

## <a name="span-idactives0d0spanspan-idactives0d0spanspan-idactives0d0spanactive-s0d0"></a><span id="Active__S0_D0_"></span><span id="active__s0_d0_"></span><span id="ACTIVE__S0_D0_"></span>アクティブ (S0/D0)


これは、クライアント アプリケーションは Bluetooth 機能を使用してアクティブにした状態です。

## <a name="span-idlowdutycyclesleeps0d2spanspan-idlowdutycyclesleeps0d2spanspan-idlowdutycyclesleeps0d2spanlow-duty-cyclesleep-s0d2"></a><span id="Low_Duty_Cycle_Sleep__S0_D2_"></span><span id="low_duty_cycle_sleep__s0_d2_"></span><span id="LOW_DUTY_CYCLE_SLEEP__S0_D2_"></span>低デューティ サイクル/スリープ (S0/D2)


これは、最も一般的な状態をシステムが効果的で (S0) が、ドライバーは D2 状態 – 低電力状態まで、コント ローラーが調整されます。 この状態では、コント ローラーには、エンド ユーザー エクスペリエンスに影響を与えずに短時間ではなくアクティブな状態 (D0) を再開できます。

Bluetooth キーボードを使用して、この状態の例を示すことができます。 数秒のキーが押されていません Bluetooth core レイヤーは D2 に通知し、電力消費の削減をスニッフィング モードでの接続を維持しながら、アイドル状態にコント ローラーを調整します。 キーの押下時に無線はウェイク アップ通知を受け取るし、D0 を再開し、受信データの読み取りを Bluetooth core ドライバー ウェイク イベントをトリガーします。

別の例は最初の条件では関連付けがない場合、Bluetooth core スタックは D2 に通知し、スリープ状態に制限する Bluetooth 無線を入力できます。 永続的な非揮発性の設定には、ユーザーにリモートの Bluetooth デバイスに関連付けるときにすばやくを再開できるときに、無線の電力消費量が最適化されます。

この状態では一般的で重大なシナリオ:

1.  関連付け (つまり Bluetooth デバイスとなしの組み合わせなど) があるないです。
2.  関連付けられて、接続しますが、アイドル状態で
3.  アソシエーションが切断されます。

以降のサブトピックでは、アクティブにアイドル状態と再開を入力のメカニズムに詳細な情報を提供します。 この状態も AOAC (Always On Always Connected) システムのプライマリの状態になります。

## <a name="span-idsystemisonbutdeviceisoffs0d3spanspan-idsystemisonbutdeviceisoffs0d3spanspan-idsystemisonbutdeviceisoffs0d3spansystem-is-on-but-device-is-off-s0d3"></a><span id="System_is_On_but_Device_is_Off__S0_D3_"></span><span id="system_is_on_but_device_is_off__s0_d3_"></span><span id="SYSTEM_IS_ON_BUT_DEVICE_IS_OFF__S0_D3_"></span>システムがしていますが、デバイスがオフ (S0/D3) には


この状態は、現在、ラジオが"off"モードでは場合にのみ、ラジオの管理をサポートします。 状態は、Bluetooth コント ローラーをプロセスが含まれていますは Bluetooth core ドライバーでは、デバイス レベルの初期化と構成では、ホストとデバイスの初期化に無制限のアクティブな状態に復元する長い待ち時間が発生します。

## <a name="span-idsystemremotewake-ablesxd2spanspan-idsystemremotewake-ablesxd2spanspan-idsystemremotewake-ablesxd2spansystem-remote-wake-able-sxd2"></a><span id="System_Remote_Wake-able__Sx_D2_"></span><span id="system_remote_wake-able__sx_d2_"></span><span id="SYSTEM_REMOTE_WAKE-ABLE__SX_D2_"></span>システム リモート ウェイクできる (Sx/D2)


Windows 8.1 では、この Sx のサポートは変更されませんし、この特定の状態を使用して、HID デバイスからシステムをスリープ解除を有効にします。 D2 の中には電源が入っているため、その内部の揮発性の設定および構成しても永続的な Bluetooth チップが続行されます。 この機能は省略可能です。

## <a name="span-idsystemoffsxd3spanspan-idsystemoffsxd3spanspan-idsystemoffsxd3spansystem-off-sxd3"></a><span id="System_Off__Sx_D3__"></span><span id="system_off__sx_d3__"></span><span id="SYSTEM_OFF__SX_D3__"></span>オフ (Sx/D3) システム


システムはオフであり、Bluetooth 無線をオフまたは低電力状態にすると見なされます。 一部 (シャット ダウン) を除くの Sx 状態では、ドライバー スタックは (つまり、読み込まれたまま) メモリに残ります。

## <a name="span-idradiomanagementspanspan-idradiomanagementspanspan-idradiomanagementspanradio-management"></a><span id="Radio_Management"></span><span id="radio_management"></span><span id="RADIO_MANAGEMENT"></span>ラジオの管理


今後、ラジオの管理 (RM) は、Bluetooth 4.0 ラジオの標準化がいます。 Bluetooth スタックは、HCI ダウン送信\_リセット コマンドは、転送モードがなしと D3 電源状態のデバイスで無線を配置することで応答するオプションが必要です。 スタックは、突然「機内」モードで無線を効果的に配置するすべての子 devnode を削除するには。 オプションをオンに戻すスタックから要求を受信できるようにシリアル バス ドライバーがオフの状態を無線でアンロード中に維持されます。 受信トレイ スタックが devnode 列挙が再処理されます。 無線管理の実装の詳細についてを参照してください、 [Bluetooth ソフトウェア無線スイッチ関数プロトタイプ](https://msdn.microsoft.com/library/windows/hardware/hh450832)します。

 

 





