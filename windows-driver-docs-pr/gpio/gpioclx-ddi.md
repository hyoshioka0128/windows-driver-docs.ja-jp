---
title: GpioClx DDI
description: 汎用 I/O (GPIO) コントローラーのドライバーは、GpioClx デバイス ドライバー インターフェイス (DDI) を介して GPIO フレームワーク拡張機能 (GpioClx) と通信します。
ms.assetid: AE8883C3-178F-44AB-AB1D-65DEC1472929
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: aa9f8aca0a72dc52385ce215f7a3f314ca1a0282
ms.sourcegitcommit: f663c383886d87ea762e419963ff427500cc5042
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67393108"
---
# <a name="gpioclx-ddi"></a>GpioClx DDI


汎用 I/O (GPIO) コントローラーのドライバーは、GpioClx デバイス ドライバー インターフェイス (DDI) を介して GPIO フレームワーク拡張機能 (GpioClx) と通信します。 この DDI は Gpioclx.h ヘッダー ファイルで定義され、[汎用 I/O (GPIO) ドライバー リファレンス](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/index)に記載されています。 この DDI の一部として、GpioClx により、GPIO コントローラーのドライバーによって呼び出されるいくつかの[ドライバー サポート メソッド](https://docs.microsoft.com/previous-versions/hh439460(v=vs.85))が実装されます。 このドライバーにより、GpioClx によって呼び出される一連の[イベント コールバック関数](https://docs.microsoft.com/previous-versions/hh439464(v=vs.85))が実装されます。 GpioClx では、これらのコールバックを使用して、割り込みの入力として構成されている GPIO ピンからの割り込み要求が管理され、データ入力およびデータ出力として構成されている GPIO ピンとの間でデータ転送が行われます。

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
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/gpio/driver-support-methods-in-the-gpioclx-ddi" data-raw-source="[Driver Support Methods in the GpioClx DDI](https://docs.microsoft.com/windows-hardware/drivers/gpio/driver-support-methods-in-the-gpioclx-ddi)">GpioClx DDI のドライバー サポート メソッド</a></p></td>
<td><p>GPIO フレームワーク拡張機能 (GpioClx) では、Windows 8 以降で使用できます。 システム提供の GpioClx DDI メソッドは、Msgpioclx.sys GpioClx カーネル モード ドライバーに実装されます。 このドライバーのエントリ ポイントのエクスポート、 <a href="https://docs.microsoft.com/previous-versions/hh439460(v=vs.85)" data-raw-source="[GpioClx driver support methods](https://docs.microsoft.com/previous-versions/hh439460(v=vs.85))">GpioClx ドライバー サポート メソッド</a>します。 Windows 8 以降、Msgpioclx.sys は、オペレーティング システムの標準的なコンポーネントです。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/gpio/optional-and-required-gpio-callback-functions" data-raw-source="[Optional and Required GPIO Callback Functions](https://docs.microsoft.com/windows-hardware/drivers/gpio/optional-and-required-gpio-callback-functions)">省略可能で、必要な GPIO コールバック関数</a></p></td>
<td><p>汎用の I/O (GPIO) コント ローラー ドライバーは呼び出し、 <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/gpioclx/nf-gpioclx-gpio_clx_registerclient" data-raw-source="[&lt;strong&gt;GPIO_CLX_RegisterClient&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/gpioclx/nf-gpioclx-gpio_clx_registerclient)"> <strong>GPIO_CLX_RegisterClient</strong> </a> GPIO フレームワーク拡張機能 (GpioClx) のクライアントとして登録します。 この呼び出し中に、ドライバーはドライバーによって実装されているイベントのコールバック関数の一覧を示す GpioClx に登録パケットを渡します。 GpioClx は、GPIO コント ローラーのハードウェア構成、I/O 操作を実行および割り込みを管理するこれらのコールバック関数を呼び出します。 GpioClx では、GPIO コント ローラーのドライバーを特定のコールバック関数の実装が他のコールバック関数は省略可能なサポートが必要です。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/gpio/gpio-device-contexts" data-raw-source="[GPIO Device Contexts](https://docs.microsoft.com/windows-hardware/drivers/gpio/gpio-device-contexts)">GPIO デバイス コンテキスト</a></p></td>
<td><p>汎用の I/O (GPIO) コント ローラー デバイスは、framework デバイス オブジェクトによって表されます。 GPIO コント ローラーのドライバーでは、このデバイス オブジェクトとデバイス コンテキストを関連付けることができます。 ドライバーでは、このデバイス コンテキストを使用して、永続的に GPIO コント ローラーのデバイスの状態に関する情報を格納します。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/gpio/partitioning-a-gpio-controller-into-banks-of-pins" data-raw-source="[Partitioning a GPIO Controller into Banks of Pins](https://docs.microsoft.com/windows-hardware/drivers/gpio/partitioning-a-gpio-controller-into-banks-of-pins)">ピンの銀行に GPIO コント ローラーをパーティション分割</a></p></td>
<td><p>ドライバー開発者向けオプション、GPIO ピンの 2 つ以上の銀行に汎用入出力 (GPIO) コント ローラーのデバイス パーティションとしてことができます。 たとえば、32 の GPIO ピンを持つ 2 つの銀行としてするには、GPIO コント ローラー ドライバーが 64 の GPIO ピン GPIO コント ローラー デバイスを説明します。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/gpio/implementation-issues-for-gpio-controller-drivers" data-raw-source="[Implementation Issues for GPIO Controller Drivers](https://docs.microsoft.com/windows-hardware/drivers/gpio/implementation-issues-for-gpio-controller-drivers)">GPIO コント ローラーのドライバーの実装の問題</a></p></td>
<td><p>GPIO フレームワーク拡張機能 (GpioClx) は、柔軟性に優れたデバイス ドライバー インターフェイス (DDI) を提供します。 この DDI では、代替のコールバック インターフェイスを選択することができます。 ドライバー開発者は、ターゲットの GPIO コント ローラー デバイスのハードウェア アーキテクチャに最適であるイベントのコールバック関数のセットを実装する必要があります。</p></td>
</tr>
</tbody>
</table>

 

 

 




