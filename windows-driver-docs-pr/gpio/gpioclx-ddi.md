---
title: GpioClx DDI
description: 汎用 I/O (GPIO) コントローラーのドライバーは、GpioClx デバイス ドライバー インターフェイス (DDI) を介して GPIO フレームワーク拡張機能 (GpioClx) と通信します。
ms.assetid: AE8883C3-178F-44AB-AB1D-65DEC1472929
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 82982725b5b20aa18e5f2deef828056631801a9d
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72824968"
---
# <a name="gpioclx-ddi"></a>GpioClx DDI


汎用 I/O (GPIO) コントローラーのドライバーは、GpioClx デバイス ドライバー インターフェイス (DDI) を介して GPIO フレームワーク拡張機能 (GpioClx) と通信します。 この DDI は Gpioclx.h ヘッダー ファイルで定義され、[汎用 I/O (GPIO) ドライバー リファレンス](https://docs.microsoft.com/windows-hardware/drivers/ddi/index)に記載されています。 この DDI の一部として、GpioClx により、GPIO コントローラーのドライバーによって呼び出されるいくつかの[ドライバー サポート メソッド](https://docs.microsoft.com/previous-versions/hh439460(v=vs.85))が実装されます。 このドライバーにより、GpioClx によって呼び出される一連の[イベント コールバック関数](https://docs.microsoft.com/previous-versions/hh439464(v=vs.85))が実装されます。 GpioClx では、これらのコールバックを使用して、割り込みの入力として構成されている GPIO ピンからの割り込み要求が管理され、データ入力およびデータ出力として構成されている GPIO ピンとの間でデータ転送が行われます。

## <a name="in-this-section"></a>このセクションの内容


<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>トピック</th>
<th>説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/gpio/driver-support-methods-in-the-gpioclx-ddi" data-raw-source="[Driver Support Methods in the GpioClx DDI](https://docs.microsoft.com/windows-hardware/drivers/gpio/driver-support-methods-in-the-gpioclx-ddi)">GpioClx DDI のドライバーサポートメソッド</a></p></td>
<td><p>GPIO framework 拡張機能 (GpioClx) は、Windows 8 以降で使用できます。 GpioClx DDI のシステム提供のメソッドは、GpioClx カーネルモードドライバーである Msgpioclx に実装されています。 このドライバーは、 <a href="https://docs.microsoft.com/previous-versions/hh439460(v=vs.85)" data-raw-source="[GpioClx driver support methods](https://docs.microsoft.com/previous-versions/hh439460(v=vs.85))">Gpioclx ドライバーのサポートメソッド</a>のエントリポイントをエクスポートします。 Windows 8 以降では、Msgpioclx はオペレーティングシステムの標準コンポーネントです。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/gpio/optional-and-required-gpio-callback-functions" data-raw-source="[Optional and Required GPIO Callback Functions](https://docs.microsoft.com/windows-hardware/drivers/gpio/optional-and-required-gpio-callback-functions)">オプションおよび必要な GPIO コールバック関数</a></p></td>
<td><p>汎用 i/o (GPIO) コントローラードライバーは、 <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/gpioclx/nf-gpioclx-gpio_clx_registerclient" data-raw-source="[&lt;strong&gt;GPIO_CLX_RegisterClient&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/gpioclx/nf-gpioclx-gpio_clx_registerclient)"><strong>GPIO_CLX_RegisterClient</strong></a>メソッドを呼び出して、GPIO framework 拡張機能 (GpioClx) のクライアントとして登録します。 この呼び出しの間に、ドライバーは、ドライバーによって実装されているイベントコールバック関数のリストを指定する登録パケットを GpioClx に渡します。 GpioClx は、これらのコールバック関数を呼び出して、GPIO コントローラーハードウェアを構成し、i/o 操作を実行し、割り込みを管理します。 GpioClx では、特定のコールバック関数を実装するために、GPIO コントローラードライバーが必要ですが、他のコールバック関数のサポートは省略可能です。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/gpio/gpio-device-contexts" data-raw-source="[GPIO Device Contexts](https://docs.microsoft.com/windows-hardware/drivers/gpio/gpio-device-contexts)">GPIO デバイスコンテキスト</a></p></td>
<td><p>汎用 i/o (GPIO) コントローラーデバイスは、フレームワークデバイスオブジェクトによって表されます。 GPIO コントローラードライバーは、デバイスコンテキストをこのデバイスオブジェクトに関連付けることができます。 ドライバーは、このデバイスコンテキストを使用して、GPIO コントローラーデバイスの状態に関する情報を永続的に格納します。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/gpio/partitioning-a-gpio-controller-into-banks-of-pins" data-raw-source="[Partitioning a GPIO Controller into Banks of Pins](https://docs.microsoft.com/windows-hardware/drivers/gpio/partitioning-a-gpio-controller-into-banks-of-pins)">GPIO コントローラーをピンのバンクにパーティション分割する</a></p></td>
<td><p>ドライバー開発者は、オプションとして汎用 i/o (GPIO) コントローラーデバイスを2つ以上の GPIO pin のバンクに分割できます。 たとえば、64 GPIO ピンを持つ GPIO controller デバイスは、GPIO コントローラードライバーによって、それぞれ 32 GPIO ピンを持つ2つの銀行として記述できます。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/gpio/implementation-issues-for-gpio-controller-drivers" data-raw-source="[Implementation Issues for GPIO Controller Drivers](https://docs.microsoft.com/windows-hardware/drivers/gpio/implementation-issues-for-gpio-controller-drivers)">GPIO コントローラードライバーの実装に関する問題</a></p></td>
<td><p>GPIO framework 拡張機能 (GpioClx) は、柔軟なデバイスドライバーインターフェイス (DDI) を提供します。 この DDI を使用すると、開発者は別のコールバックインターフェイスを選択できます。 ドライバー開発者は、ターゲットの GPIO コントローラーデバイスのハードウェアアーキテクチャに最適な一連のイベントコールバック関数を実装する必要があります。</p></td>
</tr>
</tbody>
</table>

 

 

 




