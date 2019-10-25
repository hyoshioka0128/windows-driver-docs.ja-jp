---
title: Bluetooth コア ドライバー レイヤーとサポートされている電源遷移
description: 次の表は、Bluetooth コアドライバーがサポートしているデバイスとシステムの電源の状態をまとめたものです。
ms.assetid: 25A3598E-51A7-4B16-92F7-9D2F39177946
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: acefa2bf99669bb5633b69cd6fcc7a9306d03b3d
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72832189"
---
# <a name="bluetooth-core-driver-layer-and-supported-power-transitions"></a>Bluetooth コア ドライバー レイヤーとサポートされている電源遷移


次の表は、Bluetooth コアドライバーがサポートしているデバイスとシステムの電源の状態をまとめたものです。 "スリープ" 状態は、このセクションとサブトピックを使用して、Bluetooth 無線の内部設定と構成が永続的である非常に低い電力状態を説明します。

<table>
    <tr>
        <td></td>
        <td></td>
        <td colspan="3"><b>デバイスの電源状態</b></td>
    </tr>
    <tr>
        <td></td>
        <td></td>
        <td>D0 (アクティブ)</td>
        <td>D2 (スリープ) –一部の電源は、内部状態を保持するために Bluetooth チップに保持されます。</td>
        <td>D3 (オフ)-電源が取り外されています (*)</td>
    </tr>
    <tr>
        <td rowspan="6"><b>システム電源の状態</b></td>
        <td>S0 (アクティブ)</td>
        <td>Active</td>
        <td>ウェイクの場合はスリープ</td>
        <td>無線 RM オフ</td>
    </tr>
    <tr>
        <td>S1</td>
        <td>該当なし</td>
        <td>該当なし</td>
        <td>該当なし</td>
    </tr>
    <tr>
       <td>S2</td>
        <td>該当なし</td>
        <td>該当なし</td>
        <td>該当なし</td>
    </tr>
    <tr>
        <td>S3 (スリープ)</td>
        <td>該当なし</td>
        <td>ウェイクの場合はスリープ</td>
        <td>電源をオフにすることができます</td>
    </tr>
    <tr>
        <td>S4 (休止)</td>
        <td>該当なし</td>
        <td>ウェイクの場合はスリープ</td>
        <td>電源をオフにすることができます</td>
    </tr>
    <tr>
        <td>S5 (オフ)</td>
        <td>該当なし</td>
        <td>該当なし</td>
        <td>電源をオフにすることができます</td>
    </tr>
</table>



bluetooth チップに電力が失われるため、Bluetooth コアドライバーによる再初期化 \*必要があります。

SoC システムのシステム状態サポートのガイドライン:

-   すべてのソケットに対して S0 (on) と S5 (シャットダウン) のサポートが必要
-   86 (休止状態) は、x86 ベースのソケットの場合に必要です。
-   コネクトスタンバイをサポートするシステムでは S3 がサポートされない

## <a name="span-idactive__s0_d0_spanspan-idactive__s0_d0_spanspan-idactive__s0_d0_spanactive-s0d0"></a><span id="Active__S0_D0_"></span><span id="active__s0_d0_"></span><span id="ACTIVE__S0_D0_"></span>アクティブ (S0/D0)


これは、クライアントアプリケーションが Bluetooth 機能をアクティブに使用しているときの状態です。

## <a name="span-idlow_duty_cycle_sleep__s0_d2_spanspan-idlow_duty_cycle_sleep__s0_d2_spanspan-idlow_duty_cycle_sleep__s0_d2_spanlow-duty-cyclesleep-s0d2"></a><span id="Low_Duty_Cycle_Sleep__S0_D2_"></span><span id="low_duty_cycle_sleep__s0_d2_"></span><span id="LOW_DUTY_CYCLE_SLEEP__S0_D2_"></span>低負荷サイクル/スリープ (S0/D2)


これは、システムが (S0 で) 効果的にオンになっているが、ドライバーが D2 状態の場合に、コントローラーが低い電力状態に制限されている最も一般的な状態です。 この状態では、コントローラーはエンドユーザーエクスペリエンスに影響を与えることなく、すぐにアクティブ状態 (D0) に再開できます。

この状態の例は、Bluetooth キーボードを使用して示すことができます。 数秒のうちにキーが押されていない場合、Bluetooth コアレイヤーは D2 にスロットルして、電源消費を減らすために、スニフモードで接続を維持したまま、コントローラーがアイドル状態になるのを待ちます。 キーを押すと、ラジオがウェイクアップ通知を受信し、Bluetooth コアドライバーが D0 に再開して受信データを読み取るための wake イベントをトリガーします。

もう1つの例は、関連付けがない場合の初期状態です。 Bluetooth コアスタックは D2 に入り、通知し、Bluetooth ラジオがスリープ状態になるのを許可します。 無線の電力消費は最適化されていますが、ユーザーがリモート Bluetooth デバイスに関連付けようとすると、永続的な不揮発性設定がすぐに再開されます。

この状態の一般的なシナリオと重大なシナリオを次に示します。

1.  関連付けがありません (つまり、Bluetooth デバイスとの組み合わせはありません)
2.  関連付けがありますが、接続されていますがアイドル状態です
3.  関連付けはありますが、切断されています

後のサブトピックでは、アイドル状態に入り、アクティブに復帰するメカニズムについて詳しく説明します。 また、この状態は、(常に接続されている) システムの Always On によって、プライマリ状態になります。

## <a name="span-idsystem_is_on_but_device_is_off__s0_d3_spanspan-idsystem_is_on_but_device_is_off__s0_d3_spanspan-idsystem_is_on_but_device_is_off__s0_d3_spansystem-is-on-but-device-is-off-s0d3"></a><span id="System_is_On_but_Device_is_Off__S0_D3_"></span><span id="system_is_on_but_device_is_off__s0_d3_"></span><span id="SYSTEM_IS_ON_BUT_DEVICE_IS_OFF__S0_D3_"></span>システムはオンですが、デバイスがオフになっています (S0/D3)


この状態は、ラジオが "オフ" モードの場合にのみ、ラジオ管理でサポートされます。 この状態では、Bluetooth コントローラーをアクティブな状態に復元するための待機時間が長くなりますが、デバイスレベルの初期化と構成だけでなく、Bluetooth コアドライバーによるホストとデバイスの初期化にも制限されません。

## <a name="span-idsystem_remote_wake-able__sx_d2_spanspan-idsystem_remote_wake-able__sx_d2_spanspan-idsystem_remote_wake-able__sx_d2_spansystem-remote-wake-able-sxd2"></a><span id="System_Remote_Wake-able__Sx_D2_"></span><span id="system_remote_wake-able__sx_d2_"></span><span id="SYSTEM_REMOTE_WAKE-ABLE__SX_D2_"></span>システムリモートウェイクアップ (Sx/D2)


この Sx のサポートは Windows 8.1 に対して変更されません。この特定の状態は、HID デバイスからシステムのスリープを解除できるようにするために使用されます。 D2 では、Bluetooth チップの内部的な揮発性設定と構成が永続的なままになるため、Bluetooth チップは引き続き電力を保持します。 この機能は省略可能です。

## <a name="span-idsystem_off__sx_d3__spanspan-idsystem_off__sx_d3__spanspan-idsystem_off__sx_d3__spansystem-off-sxd3"></a><span id="System_Off__Sx_D3__"></span><span id="system_off__sx_d3__"></span><span id="SYSTEM_OFF__SX_D3__"></span>システムオフ (Sx/D3)


システムはオフになっており、Bluetooth ラジオはオフになっているか、電力が低い状態であると見なされます。 一部の Sx 状態 (シャットダウンを除く) では、ドライバースタックはまだメモリ内にあります (つまり、読み込まれたまま)。

## <a name="span-idradio_managementspanspan-idradio_managementspanspan-idradio_managementspanradio-management"></a><span id="Radio_Management"></span><span id="radio_management"></span><span id="RADIO_MANAGEMENT"></span>ラジオ管理


今後、Bluetooth 4.0 ラジオ用に無線管理 (RM) が標準化される予定です。 Bluetooth スタックは HCI\_RESET コマンドを送信します。このコマンドは、無線が送信モードではなく、デバイスが D3 電源状態であるために応答することが期待されています。 その後、スタックはすべての子 devnodes を驚かせ、無線を "機内" モードで効果的に配置します。 Serial bus ドライバーは、ラジオがオフの状態になっている間は読み込まれたままになるため、スタックから要求を受信して、ラジオを再びオンにすることができます。 受信トレイスタックは、devnodes の再列挙を処理します。 ラジオ管理の実装の詳細については、 [Bluetooth ソフトウェアのラジオスイッチ関数プロトタイプ](https://docs.microsoft.com/windows-hardware/drivers/ddi/index)に関する説明を参照してください。

 

 





