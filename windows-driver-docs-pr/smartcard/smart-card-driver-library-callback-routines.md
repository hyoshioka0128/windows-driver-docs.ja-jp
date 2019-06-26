---
title: スマート カード ドライバー ライブラリのコールバックルーチン
description: スマート カード ドライバー ライブラリのコールバックルーチン
ms.assetid: e536d539-4871-4b1d-bb5a-92a310dfa1e7
keywords:
- Ioctl WDK のスマート カード
- ライブラリ コールバック ルーチン WDK スマート カード
- コールバック ルーチン WDK のスマート カード
- ReaderFunction
- ベンダーから提供されたドライバー WDK スマート カード、IOCTL 要求の管理
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 74b6b2878385ebe9791d76ce702fa72e2b2bde77
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67356665"
---
# <a name="smart-card-driver-library-callback-routines"></a>スマート カード ドライバー ライブラリのコールバックルーチン


## <span id="_ntovr_smart_card_driver_library_callback_routines"></span><span id="_NTOVR_SMART_CARD_DRIVER_LIBRARY_CALLBACK_ROUTINES"></span>


スマート カードのアーキテクチャでは、一連の標準的なコールバックの日常的な型を定義します。 詳細については、これらのルーチンは、次を参照してください。[スマート カード ドライバー コールバック](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/index)します。

リーダー ドライバーする必要がありますこれらのコールバック ルーチンを使用できるようにドライバー ライブラリのルーチン、 [ **SmartcardDeviceControl (WDM)** ](https://docs.microsoft.com/previous-versions/ff548939(v=vs.85))を呼び出す、スマート カード デバイス拡張機能でそれらへのポインターを格納することで、型の[**スマート カード\_拡張子**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/smclib/ns-smclib-_smartcard_extension)します。 これらのポインターに配置されている配列に格納されます、 **ReaderFunction**スマート カードのメンバー\_拡張機能の構造体。 個々 のコールバック ルーチンは、一連の定数の値へのインデックスとして使用する必要がありますで識別できます、 **ReaderFunction**配列。

たとえば、する場合は[ **SmartcardDeviceControl** ](https://docs.microsoft.com/previous-versions/ff548939(v=vs.85))をという名前は、リーダー ドライバー コールバック ルーチンを呼び出す**DriverCardPower** の処理が終了してたびに[**IOCTL\_スマート カード\_POWER** ](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff548907(v=vs.85))要求、使用する必要があります、 [ *RDF\_カード\_POWER*](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff548919(v=vs.85))定数を次のように、デバイスの拡張機能を初期化します。

```cpp
SmartcardExtension->ReaderFunction[RDF_CARD_POWER] = 
DriverCardPower;
```

RDF\_カード\_電源は常に、IOCTL サービスを提供するコールバック ルーチンに対応する固定のシステム定義の定数\_スマート カード\_POWER 要求。

場合のメンバー、 **ReaderFunction**処理中の IOCTL に対応する配列が**NULL**、 [ **SmartcardDeviceControl** ](https://docs.microsoft.com/previous-versions/ff548939(v=vs.85))ステータスを返します\_いない\_リーダーのドライバーをサポートします。 場合によっては、この動作は便利です。 たとえば、カード取り出しまたはカードを受け入れるには、このドライバーはサポートされて場合は、適切なメンバーを割り当てるだけで、 **ReaderFunction**配列**NULL**と**SmartcardDeviceControl**ステータスを返します\_いない\_メンバー ルーチンが呼び出されるたびにサポートします。

次の表では、コールバック ルーチンのさまざまな種類を識別する定数を示します。 これらは、定数へのインデックスとして使用する必要があります、 **ReaderFunction**配列。 テーブルは、日常的な各種の簡単な説明し、必須またはオプションで、ルーチンを実装するためにリーダーのドライバーがあるかどうかを示します。

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">インデックス</th>
<th align="left">対応するコールバック ルーチンの説明</th>
<th align="left">リーダーのドライバーによる実装</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff548919(v=vs.85)" data-raw-source="[&lt;em&gt;RDF_CARD_POWER&lt;/em&gt;](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff548919(v=vs.85))"><em>RDF_CARD_POWER</em></a></p></td>
<td align="left"><p>リセット、または挿入されたスマート カードをオフに</p></td>
<td align="left"><p>必須</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff548918(v=vs.85)" data-raw-source="[&lt;em&gt;RDF_CARD_EJECT&lt;/em&gt;](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff548918(v=vs.85))"><em>RDF_CARD_EJECT</em></a></p></td>
<td align="left"><p>挿入されたスマート カードを取り出す</p></td>
<td align="left"><p>省略可能</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff548920(v=vs.85)" data-raw-source="[&lt;em&gt;RDF_CARD_TRACKING&lt;/em&gt;](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff548920(v=vs.85))"><em>RDF_CARD_TRACKING</em></a></p></td>
<td align="left"><p>カードの挿入と削除を追跡するために、イベント ハンドラーをインストールします。</p></td>
<td align="left"><p>必須</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff548921(v=vs.85)" data-raw-source="[&lt;em&gt;RDF_IOCTL_VENDOR&lt;/em&gt;](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff548921(v=vs.85))"><em>RDF_IOCTL_VENDOR</em></a></p></td>
<td align="left"><p>ベンダー固有の IOCTL 操作を実行します</p></td>
<td align="left"><p>省略可能</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff548922(v=vs.85)" data-raw-source="[&lt;em&gt;RDF_READER_SWALLOW&lt;/em&gt;](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff548922(v=vs.85))"><em>RDF_READER_SWALLOW</em></a></p></td>
<td align="left"><p>機械的な理解しには</p></td>
<td align="left"><p>省略可能</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff548923(v=vs.85)" data-raw-source="[&lt;em&gt;RDF_SET_PROTOCOL&lt;/em&gt;](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff548923(v=vs.85))"><em>RDF_SET_PROTOCOL</em></a></p></td>
<td align="left"><p>カード リーダーにカードの伝送プロトコルを選択します。</p></td>
<td align="left"><p>必須</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff548924(v=vs.85)" data-raw-source="[&lt;em&gt;RDF_TRANSMIT&lt;/em&gt;](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff548924(v=vs.85))"><em>RDF_TRANSMIT</em></a></p></td>
<td align="left"><p>データ転送を実行します。</p></td>
<td align="left"><p>必須</p></td>
</tr>
</tbody>
</table>

 

リーダーのドライバーがこれらのルーチンを呼び出すと、呼び出しのパラメーターから取得、入力バッファー」の説明に従って[スマート カード ドライバー コールバック](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/index)します。 リーダーのドライバーが内の同じセクションの説明に従って、出力データを適切なバッファー領域を格納もする必要があります。

カードの追跡のコールバック ルーチン以外の任意のコールバック ルーチンが状態を返す場合\_リーダーのドライバーからさらに、呼び出しがスマート カードのライブラリ保留中、停止します。 (カードの追跡のコールバック ルーチンの詳細については、次を参照してください[ *RDF\_カード\_追跡*](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff548920(v=vs.85))。)。ライブラリ ルーチンのステータスを返しますリーダーのドライバーは、ライブラリがこの状態の中にドライバー ライブラリのルーチンを使用すると、\_デバイス\_ビジーです。 効果的にこうリーダーのドライバーから resource manager では、IOCTL 要求の処理から呼び出すことができない場合、リーダーのドライバーは IOCTL 要求を処理できないので[ **SmartcardDeviceControl** ](https://docs.microsoft.com/previous-versions/ff548939(v=vs.85)).

 

 





