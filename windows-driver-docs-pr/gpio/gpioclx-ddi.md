---
title: GpioClx DDI
description: 汎用 I/O (GPIO) コントローラーのドライバーは、GpioClx デバイス ドライバー インターフェイス (DDI) を介して GPIO フレームワーク拡張機能 (GpioClx) と通信します。
ms.assetid: AE8883C3-178F-44AB-AB1D-65DEC1472929
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ff8a5283367f4ecebdd4de59308f4f42c264c815
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63326132"
---
# <a name="gpioclx-ddi"></a>GpioClx DDI


汎用 I/O (GPIO) コントローラーのドライバーは、GpioClx デバイス ドライバー インターフェイス (DDI) を介して GPIO フレームワーク拡張機能 (GpioClx) と通信します。 この DDI は Gpioclx.h ヘッダー ファイルで定義され、[汎用 I/O (GPIO) ドライバー リファレンス](https://msdn.microsoft.com/library/windows/hardware/hh439515)に記載されています。 この DDI の一部として、GpioClx により、GPIO コントローラーのドライバーによって呼び出されるいくつかの[ドライバー サポート メソッド](https://msdn.microsoft.com/library/windows/hardware/hh439460)が実装されます。 このドライバーにより、GpioClx によって呼び出される一連の[イベント コールバック関数](https://msdn.microsoft.com/library/windows/hardware/hh439464)が実装されます。 GpioClx では、これらのコールバックを使用して、割り込みの入力として構成されている GPIO ピンからの割り込み要求が管理され、データ入力およびデータ出力として構成されている GPIO ピンとの間でデータ転送が行われます。

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
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/hh439453" data-raw-source="[Driver Support Methods in the GpioClx DDI](https://msdn.microsoft.com/library/windows/hardware/hh439453)">GpioClx DDI のドライバー サポート メソッド</a></p></td>
<td><p>GPIO フレームワーク拡張機能 (GpioClx) では、Windows 8 以降で使用できます。 システム提供の GpioClx DDI メソッドは、Msgpioclx.sys GpioClx カーネル モード ドライバーに実装されます。 このドライバーのエントリ ポイントのエクスポート、 <a href="https://msdn.microsoft.com/library/windows/hardware/hh439460" data-raw-source="[GpioClx driver support methods](https://msdn.microsoft.com/library/windows/hardware/hh439460)">GpioClx ドライバー サポート メソッド</a>します。 Windows 8 以降、Msgpioclx.sys は、オペレーティング システムの標準的なコンポーネントです。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/hh406514" data-raw-source="[Optional and Required GPIO Callback Functions](https://msdn.microsoft.com/library/windows/hardware/hh406514)">省略可能で、必要な GPIO コールバック関数</a></p></td>
<td><p>汎用の I/O (GPIO) コント ローラー ドライバーは呼び出し、 <a href="https://msdn.microsoft.com/library/windows/hardware/hh439490" data-raw-source="[&lt;strong&gt;GPIO_CLX_RegisterClient&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/hh439490)"> <strong>GPIO_CLX_RegisterClient</strong> </a> GPIO フレームワーク拡張機能 (GpioClx) のクライアントとして登録します。 この呼び出し中に、ドライバーはドライバーによって実装されているイベントのコールバック関数の一覧を示す GpioClx に登録パケットを渡します。 GpioClx は、GPIO コント ローラーのハードウェア構成、I/O 操作を実行および割り込みを管理するこれらのコールバック関数を呼び出します。 GpioClx では、GPIO コント ローラーのドライバーを特定のコールバック関数の実装が他のコールバック関数は省略可能なサポートが必要です。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/hh406460" data-raw-source="[GPIO Device Contexts](https://msdn.microsoft.com/library/windows/hardware/hh406460)">GPIO デバイス コンテキスト</a></p></td>
<td><p>汎用の I/O (GPIO) コント ローラー デバイスは、framework デバイス オブジェクトによって表されます。 GPIO コント ローラーのドライバーでは、このデバイス オブジェクトとデバイス コンテキストを関連付けることができます。 ドライバーでは、このデバイス コンテキストを使用して、永続的に GPIO コント ローラーのデバイスの状態に関する情報を格納します。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/hh406517" data-raw-source="[Partitioning a GPIO Controller into Banks of Pins](https://msdn.microsoft.com/library/windows/hardware/hh406517)">ピンの銀行に GPIO コント ローラーをパーティション分割</a></p></td>
<td><p>ドライバー開発者向けオプション、GPIO ピンの 2 つ以上の銀行に汎用入出力 (GPIO) コント ローラーのデバイス パーティションとしてことができます。 たとえば、32 の GPIO ピンを持つ 2 つの銀行としてするには、GPIO コント ローラー ドライバーが 64 の GPIO ピン GPIO コント ローラー デバイスを説明します。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/hh406479" data-raw-source="[Implementation Issues for GPIO Controller Drivers](https://msdn.microsoft.com/library/windows/hardware/hh406479)">GPIO コント ローラーのドライバーの実装の問題</a></p></td>
<td><p>GPIO フレームワーク拡張機能 (GpioClx) は、柔軟性に優れたデバイス ドライバー インターフェイス (DDI) を提供します。 この DDI では、代替のコールバック インターフェイスを選択することができます。 ドライバー開発者は、ターゲットの GPIO コント ローラー デバイスのハードウェア アーキテクチャに最適であるイベントのコールバック関数のセットを実装する必要があります。</p></td>
</tr>
</tbody>
</table>

 

 

 




