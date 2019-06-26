---
title: HID ボタン ドライバー
description: GPIO ボタンの Microsoft 提供のボタン ドライバーを使用します。それ以外の場合、オペレーティング システムに HID データを挿入するドライバーを実装します。
ms.assetid: FBA8141D-8DBA-4C68-8BB5-44B3EDB7D062
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: da20c3b6476e1ab339e202979d2a6922d4af0e90
ms.sourcegitcommit: f663c383886d87ea762e419963ff427500cc5042
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67393486"
---
# <a name="hid-button-drivers"></a>HID ボタン ドライバー


**概要**

-   [ACPI と負荷の Microsoft 提供のドライバーの GPIO ボタンについて説明します](acpi-button-device.md)
-   [HID ソース ドライバーを非 GPIO ボタンのカーネル モードの作成します。](virtual-hid-framework--vhf-.md)
-   [非 GPIO ボタンの UMDF HID ミニドライバーを作成します。](https://docs.microsoft.com/windows-hardware/drivers/wdf/creating-umdf-hid-minidrivers)

**適用対象**

-   Windows 10
-   HID ボタンのデバイスのドライバー開発者向け

**重要な API**

-   [仮想 HID Framework リファレンス](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/index)
-   [UMDF HID ミニドライバー Ioctl](https://docs.microsoft.com/previous-versions/hh463977(v=vs.85))

GPIO ボタンの Microsoft 提供のボタン ドライバーを使用します。それ以外の場合、オペレーティング システムに HID データを挿入するドライバーを実装します。

(電源、Windows、ボリューム、および回転ロック) のボタンは通常、物理キーボードがコンバーチブルやスレートなどのフォーム ファクターで、ユーザーが利用できるときに発生したタスクに使用されます。 ボタン宣言自体、オペレーティング システムに HID デバイスとして指定することによって[HID ボタンのレポート記述子](https://docs.microsoft.com/windows-hardware/drivers/gpiobtn/hid-button-report-descriptors)します。 これにより、標準化された方法で、目的とこれらのボタンのイベントを解釈するシステムです。 ボタンの状態変更では、そのイベントにマップされます、 [HID の使用](hid-usages.md)します。 HID のトランスポート ミニドライバーは、ユーザー モードまたはカーネル モードでの HID クライアントに詳細情報を送信する上位レベルのドライバーをこれらのイベントを報告します。

物理の汎用入出力 (GPIO) ボタンが定義されている GPIO ハードウェア リソースを受信する割り込みに基づいてイベントを報告する Microsoft 提供のインボックス ドライバーは HID トランスポートのミニドライバーです。

インボックス ドライバーは、割り込みの行にワイヤード (有線) ではないボタンでサービスことはできません。 このようなボタンは HID クラス ドライバーについて、HID ボタンとレポートの状態の変化に応じて、ボタンを公開するドライバーを作成する必要があります (Microsoft が提供)。 ドライバーは、HID ソースのドライバーまたは HID トランスポート ドライバーです。

## <a name="guidance-for-supporting-hid-buttons"></a>HID ボタンをサポートするためのガイダンス


ここでは、いくつかの一般的なポインターを判断する実装の HID ボタンを作成する場合に従う必要があります。

![ボタンを実装するための意思決定グラフ](images/button.png)

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p><strong>Microsoft 提供のボックスにボタン ドライバーを使用します。</strong></p>
<p><img src="images/hid-acpi.png" alt="ACPI description of a HID button" /></p></td>
<td><p>GPIO ボタンを実装する場合は、できるように、Windows オペレーティング システムにイベントを報告するボタン ドライバーとして Hidinterrupt.sys、インボックス ドライバーを読み込むことができます、ボタンを ACPI システムに説明してください。</p>
<ul>
<li><a href="acpi-button-device.md" data-raw-source="[ACPI button device](acpi-button-device.md)">ACPI ボタン デバイス</a></li>
<li><a href="https://docs.microsoft.com/windows-hardware/drivers/gpiobtn/button-behavior" data-raw-source="[Button Behavior](https://docs.microsoft.com/windows-hardware/drivers/gpiobtn/button-behavior)">ボタンの動作</a></li>
<li><a href="acpi-button-device.md#acpi-button-phone" data-raw-source="[Sample buttons ACPI for phone/tablet](acpi-button-device.md#acpi-button-phone)">電話やタブレットのサンプル ボタン ACPI</a></li>
<li><a href="acpi-button-device.md#acpi-button-desktop" data-raw-source="[Sample buttons ACPI for desktop](acpi-button-device.md#acpi-button-desktop)">デスクトップ用サンプル ボタン ACPI</a></li>
</ul>
<p>Microsoft では、インボックス トランスポートのミニドライバー可能な限りを使用することお勧めします。</p></td>
</tr>
<tr class="even">
<td><p><strong>カーネル モードでの HID ソースのドライバーを記述します。</strong></p>
<p><img src="images/hid-vhf.png" alt="Buttons using Virtual HID Framework" /></p></td>
<td><p>別のソフトウェア コンポーネントで挿入する必要がある HID 形式でデータのストリームなどの非 GPIO ボタンを実装する場合は、カーネル モード ドライバーを記述することもできます。 Windows 10 以降、通信と仮想 HID フレームワーク (VHF) と取得して、HID クラス ドライバーとの間に、HID レポートを設定するプログラミング インターフェイスを呼び出すことによって、HID ソースのドライバーを記述できます。</p>
<ul>
<li><a href="virtual-hid-framework--vhf-.md" data-raw-source="[How to write a HID source driver that interacts with Virtual HID Framework (VHF)](virtual-hid-framework--vhf-.md)">仮想 HID フレームワーク (VHF) と連携する HID ソース ドライバーを記述する方法</a></li>
<li><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/index" data-raw-source="[Virtual HID Framework Reference](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/index)">仮想 HID Framework リファレンス</a></li>
</ul>
<p>代わりに、カーネル モード HID トランスポート ミニドライバー Windows の以前のバージョンでサポートされているを記述することができます。 ただしは勧めこのアプローチ コーディング KMDF HID トランスポート ミニドライバー、システムがクラッシュすることができます。</p>
<ul>
<li><a href="transport-minidrivers.md" data-raw-source="[Transport Minidrivers](transport-minidrivers.md)">トランスポート ミニドライバー</a></li>
<li><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/index" data-raw-source="[HID Minidriver IOCTLs](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/index)">HID ミニドライバー Ioctl</a></li>
</ul></td>
</tr>
<tr class="odd">
<td><p><strong>UMDF HID のミニドライバーを作成します。</strong></p>
<p><img src="images/hid-umdf.png" alt="HID Transport Minidriver" /></p></td>
<td><p>HID ソース ドライバーでは、書き込みの前のモデルを使用する代わりに、非 GPIO ボタンを実装している場合は、ユーザー モードで、HID トランスポート ミニドライバーを作成できます。 これらのドライバーはカーネル モード ドライバーよりも開発を容易にし、このドライバーでエラーがシステム全体をバグをオンにしないでいます。</p>
<ul>
<li><a href="https://docs.microsoft.com/windows-hardware/drivers/wdf/creating-umdf-hid-minidrivers" data-raw-source="[Creating UMDF HID Minidrivers](https://docs.microsoft.com/windows-hardware/drivers/wdf/creating-umdf-hid-minidrivers)">UMDF HID ミニドライバーを作成します。</a></li>
<li><a href="https://docs.microsoft.com/previous-versions/hh463977(v=vs.85)" data-raw-source="[UMDF HID Minidriver IOCTLs](https://docs.microsoft.com/previous-versions/hh463977(v=vs.85))">UMDF HID ミニドライバー Ioctl</a></li>
</ul></td>
</tr>
</tbody>
</table>

 

## <a name="universal-windows-drivers-for-hid-buttons"></a>HID ボタンのユニバーサル Windows ドライバー


Windows 10 以降、HID ドライバーのプログラミング インターフェイスは、Windows OneCoreUAP ベース エディションの一部です。 使用して、ボタン ドライバーを記述するその共通のインターフェイスのセットを使用すると、[仮想 HID Framework](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/index)または[トランスポート ミニドライバー](transport-minidrivers.md)インターフェイス。 これらのドライバーは、バージョンに両方のデスクトップ エディション (Home、Pro、Enterprise、および教育機関向け) の Windows 10 および Windows 10 Mobile、だけでなく他の Windows 10 で実行されます。

ステップ バイ ステップ ガイダンスについては、次を参照してください。[ユニバーサル Windows ドライバーの概要](https://docs.microsoft.com/windows-hardware/drivers)します。

## <a name="related-topics"></a>関連トピック
[ヒューマン インターフェイス デバイス](https://developer.microsoft.com/windows/hardware)  



