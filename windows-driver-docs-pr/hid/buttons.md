---
title: HID ボタン ドライバー
description: GPIO ボタンには、Microsoft 提供のボタンドライバーを使用します。それ以外の場合は、オペレーティングシステムに HID データを挿入するドライバーを実装します。
ms.assetid: FBA8141D-8DBA-4C68-8BB5-44B3EDB7D062
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: a9d8eda9b022d836b2900c9e857ffb4c7fa6d820
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72824860"
---
# <a name="hid-button-drivers"></a>HID ボタン ドライバー


**要約**

-   [ACPI で GPIO ボタンを記述し、Microsoft が提供するドライバーを読み込む](acpi-button-device.md)
-   [非 GPIO ボタンのために、HID ソースドライバーをカーネルモードで記述する](virtual-hid-framework--vhf-.md)
-   [非 GPIO ボタンの UMDF HID ミニドライバーを作成する](https://docs.microsoft.com/windows-hardware/drivers/wdf/creating-umdf-hid-minidrivers)

**適用対象**

-   Windows 10
-   HID ボタンデバイスのドライバー開発者

**重要な API**

-   [仮想 HID フレームワークリファレンス](https://docs.microsoft.com/windows-hardware/drivers/ddi/index)
-   [UMDF HID ミニドライバー Ioctl](https://docs.microsoft.com/previous-versions/hh463977(v=vs.85))

GPIO ボタンには、Microsoft 提供のボタンドライバーを使用します。それ以外の場合は、オペレーティングシステムに HID データを挿入するドライバーを実装します。

ボタン (電源、ウィンドウ、ボリューム、および回転ロック) は、通常、ユーザーが物理キーボードを使用できないときに発生するタスク (コンバーチブルやスレートなどのフォームファクター) に使用されます。 ボタンは、 [hid ボタンのレポート記述子](https://docs.microsoft.com/windows-hardware/drivers/gpiobtn/hid-button-report-descriptors)を指定することによって、オペレーティングシステムに対して hid デバイスとして自身を宣言します。 これにより、システムは、これらのボタンの目的とイベントを標準化された方法で解釈できます。 ボタンの状態が変化すると、そのイベントは[HID の使用](hid-usages.md)にマップされます。 HID トランスポートミニドライバーは、これらのイベントを上位レベルのドライバーに報告し、ユーザーモードまたはカーネルモードで詳細を HID クライアントに送信します。

物理汎用 i/o (GPIO) ボタンの場合、HID transport ミニドライバーは、定義された GPIO ハードウェアリソースで受信した割り込みに基づいてイベントを報告する、Microsoft が提供するインボックスドライバーです。

インボックスドライバーは、割り込み線に結線されていないボタンを処理することはできません。 このようなボタンを使用するには、ボタンを HID ボタンとして公開し、状態の変更を HID クラスドライバー (Microsoft 提供) に報告するドライバーを作成する必要があります。 ドライバーは、HID ソースドライバーまたは HID トランスポートドライバーである可能性があります。

## <a name="guidance-for-supporting-hid-buttons"></a>HID ボタンのサポートに関するガイダンス


ここでは、HID ボタンを作成する場合に従う必要のある実装を決定するのに役立つ一般的なポインターを示します。

![ボタンを実装するためのデシジョンチャート](images/button.png)

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p><strong>Microsoft 提供のインボックスボタンドライバーを使用する</strong></p>
<p><img src="images/hid-acpi.png" alt="ACPI description of a HID button" /></p></td>
<td><p>GPIO ボタンを実装する場合は、システム ACPI のボタンを記述します。これにより、Windows では、オペレーティングシステムにイベントを報告するボタンドライバーとして、組み込みのドライバーである Hidinterrupt .sys を読み込むことができます。</p>
<ul>
<li><a href="acpi-button-device.md" data-raw-source="[ACPI button device](acpi-button-device.md)">ACPI ボタンデバイス</a></li>
<li><a href="https://docs.microsoft.com/windows-hardware/drivers/gpiobtn/button-behavior" data-raw-source="[Button Behavior](https://docs.microsoft.com/windows-hardware/drivers/gpiobtn/button-behavior)">ボタンの動作</a></li>
<li><a href="acpi-button-device.md#acpi-button-phone" data-raw-source="[Sample buttons ACPI for phone/tablet](acpi-button-device.md#acpi-button-phone)">電話/タブレット用のサンプルボタン ACPI</a></li>
<li><a href="acpi-button-device.md#acpi-button-desktop" data-raw-source="[Sample buttons ACPI for desktop](acpi-button-device.md#acpi-button-desktop)">デスクトップ用のサンプルボタン ACPI</a></li>
</ul>
<p>Microsoft では、可能な限り、インボックスミニドライバーを使用することをお勧めします。</p></td>
</tr>
<tr class="even">
<td><p><strong>カーネルモードで HID ソースドライバーを作成する</strong></p>
<p><img src="images/hid-vhf.png" alt="Buttons using Virtual HID Framework" /></p></td>
<td><p>別のソフトウェアコンポーネントによって挿入される必要があるデータストリームなどの非 GPIO ボタンを HID 形式で実装する場合は、カーネルモードドライバーを作成することを選択できます。 Windows 10 以降では、仮想 HID フレームワーク (VHF) と通信するプログラミングインターフェイスを呼び出し、hid クラスドライバーとの間で hid レポートを取得して設定することによって、HID ソースドライバーを記述できます。</p>
<ul>
<li><a href="virtual-hid-framework--vhf-.md" data-raw-source="[How to write a HID source driver that interacts with Virtual HID Framework (VHF)](virtual-hid-framework--vhf-.md)">仮想 HID フレームワーク (VHF) と対話する HID ソースドライバーを作成する方法</a></li>
<li><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/index" data-raw-source="[Virtual HID Framework Reference](https://docs.microsoft.com/windows-hardware/drivers/ddi/index)">仮想 HID フレームワークリファレンス</a></li>
</ul>
<p>または、以前のバージョンの Windows でサポートされているように、カーネルモード HID トランスポートミニドライバーを作成することもできます。 しかし、この方法は推奨されません。 KMDF HID transport ミニドライバーがシステムをクラッシュさせる可能性があるためです。</p>
<ul>
<li><a href="transport-minidrivers.md" data-raw-source="[Transport Minidrivers](transport-minidrivers.md)">トランスポートミニドライバー</a></li>
<li><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/index" data-raw-source="[HID Minidriver IOCTLs](https://docs.microsoft.com/windows-hardware/drivers/ddi/index)">HID ミニドライバー Ioctl</a></li>
</ul></td>
</tr>
<tr class="odd">
<td><p><strong>UMDF HID ミニドライバーを作成する</strong></p>
<p><img src="images/hid-umdf.png" alt="HID Transport Minidriver" /></p></td>
<td><p>非 GPIO ボタンを実装する場合は、以前の HID ソースドライバーの作成モデルを使用するのではなく、ユーザーモードで HID transport ミニドライバーを記述できます。 これらのドライバーは、カーネルモードのドライバーよりも開発が容易で、このドライバーのエラーはシステム全体をバグチェックしません。</p>
<ul>
<li><a href="https://docs.microsoft.com/windows-hardware/drivers/wdf/creating-umdf-hid-minidrivers" data-raw-source="[Creating UMDF HID Minidrivers](https://docs.microsoft.com/windows-hardware/drivers/wdf/creating-umdf-hid-minidrivers)">UMDF HID ミニドライバーを作成しています</a></li>
<li><a href="https://docs.microsoft.com/previous-versions/hh463977(v=vs.85)" data-raw-source="[UMDF HID Minidriver IOCTLs](https://docs.microsoft.com/previous-versions/hh463977(v=vs.85))">UMDF HID ミニドライバー Ioctl</a></li>
</ul></td>
</tr>
</tbody>
</table>

 

## <a name="universal-windows-drivers-for-hid-buttons"></a>HID 用ユニバーサル Windows ドライバーのボタン


Windows 10 以降では、HID ドライバーのプログラミングインターフェイスは、OneCoreUAP ベースの Windows のエディションの一部になっています。 この共通のインターフェイスセットを使用して、[仮想 HID フレームワーク](https://docs.microsoft.com/windows-hardware/drivers/ddi/index)または[トランスポートミニドライバー](transport-minidrivers.md)インターフェイスを使用して、ボタンドライバーを作成できます。 これらのドライバーは、Windows 10 for desktop エディション (Home、Pro、Enterprise、および教育) と Windows 10 Mobile、およびその他の Windows 10 バージョンで動作します。

詳細な手順のガイダンスについては、「[ユニバーサル Windows ドライバーでのはじめに](https://docs.microsoft.com/windows-hardware/drivers)」を参照してください。

## <a name="related-topics"></a>関連トピック
[ヒューマンインターフェイスデバイス](https://developer.microsoft.com/windows/hardware)  



