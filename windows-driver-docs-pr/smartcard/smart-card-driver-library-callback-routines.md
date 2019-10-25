---
title: スマート カード ドライバー ライブラリのコールバックルーチン
description: スマート カード ドライバー ライブラリのコールバックルーチン
ms.assetid: e536d539-4871-4b1d-bb5a-92a310dfa1e7
keywords:
- Ioctl WDK スマートカード
- ライブラリコールバックルーチン WDK スマートカード
- コールバックルーチン WDK スマートカード
- ReaderFunction
- ベンダー提供のドライバー WDK スマートカード、IOCTL 要求の管理
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 19a3b6db0d38847219a1de4bf220ada0ddbb876e
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72845045"
---
# <a name="smart-card-driver-library-callback-routines"></a>スマート カード ドライバー ライブラリのコールバックルーチン


## <span id="_ntovr_smart_card_driver_library_callback_routines"></span><span id="_NTOVR_SMART_CARD_DRIVER_LIBRARY_CALLBACK_ROUTINES"></span>


スマートカードアーキテクチャは、一連の標準のコールバックルーチンの種類を定義します。 これらのルーチンの詳細については、「[スマートカードドライバーのコールバック](https://docs.microsoft.com/windows-hardware/drivers/ddi/index)」を参照してください。

リーダードライバーは、スマートカードデバイス拡張機能 (スマートカード[ **\_拡張機能**](https://docs.microsoft.com/windows-hardware/drivers/ddi/smclib/ns-smclib-_smartcard_extension)) にポインターを格納することによって呼び出しを行うために、これらのコールバックルーチンを driver library ルーチン[ **(Smartcarddevicecontrol)** ](https://docs.microsoft.com/previous-versions/ff548939(v=vs.85))で使用できるようにする必要があります。 これらのポインターは、スマートカード\_拡張機能の構造体の**Readerfunction**メンバーにある配列に格納されます。 個々のコールバックルーチンは一連の定数値によって識別できます。これは、 **Readerfunction**配列へのインデックスとして使用する必要があります。

たとえば、 [**Smartcarddevicecontrol**](https://docs.microsoft.com/previous-versions/ff548939(v=vs.85))が、 [**IOCTL\_スマートカード\_の電源**](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff548907(v=vs.85))要求の処理が完了するたびに**drivercardpower**という名前のリーダードライバーでコールバックルーチンを呼び出すようにする場合は、RDF を使用する必要があります。 [ *\_カード*](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff548919(v=vs.85))は次の方法でデバイス拡張機能を初期化するために、POWER constant を\_します。

```cpp
SmartcardExtension->ReaderFunction[RDF_CARD_POWER] = 
DriverCardPower;
```

RDF\_CARD\_POWER は、IOCTL\_スマートカード\_の電源要求をサービスするコールバックルーチンに常に対応する固定システム定義定数です。

処理されている IOCTL に対応する**Readerfunction**配列のメンバーが**NULL**の場合、 [**smartcarddevicecontrol**](https://docs.microsoft.com/previous-versions/ff548939(v=vs.85))は状態の状態を返します。リーダードライバーでは\_サポートされていません\_。 場合によっては、この動作は便利です。 たとえば、ドライバーがカードの取り出しまたはカードの飲み込みをサポートしていない場合は、 **Readerfunction**配列の適切なメンバーを**NULL**として割り当てるだけで、 **SMARTCARDDEVICECONTROL**は状態\_返しません\_そのメンバールーチンが呼び出されるたびにサポートされます。

次の表は、さまざまな種類のコールバックルーチンを識別する定数を示しています。 これらは、 **Readerfunction**配列へのインデックスとして使用する必要がある定数です。 また、この表では、各ルーチンの種類の簡単な説明と、ルーチンを実装するリーダードライバーの必須または省略可能かどうかを示します。

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">インデックス</th>
<th align="left">対応するコールバックルーチンの説明</th>
<th align="left">リーダードライバーによる実装</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff548919(v=vs.85)" data-raw-source="[&lt;em&gt;RDF_CARD_POWER&lt;/em&gt;](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff548919(v=vs.85))"><em>RDF_CARD_POWER</em></a></p></td>
<td align="left"><p>挿入されたスマートカードをリセットまたはオフにします</p></td>
<td align="left"><p>Mandatory</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff548918(v=vs.85)" data-raw-source="[&lt;em&gt;RDF_CARD_EJECT&lt;/em&gt;](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff548918(v=vs.85))"><em>RDF_CARD_EJECT</em></a></p></td>
<td align="left"><p>挿入されたスマートカードを排出します</p></td>
<td align="left"><p>オプション</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff548920(v=vs.85)" data-raw-source="[&lt;em&gt;RDF_CARD_TRACKING&lt;/em&gt;](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff548920(v=vs.85))"><em>RDF_CARD_TRACKING</em></a></p></td>
<td align="left"><p>カードの挿入と削除を追跡するイベントハンドラーをインストールします。</p></td>
<td align="left"><p>Mandatory</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff548921(v=vs.85)" data-raw-source="[&lt;em&gt;RDF_IOCTL_VENDOR&lt;/em&gt;](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff548921(v=vs.85))"><em>RDF_IOCTL_VENDOR</em></a></p></td>
<td align="left"><p>ベンダー固有の IOCTL 操作を実行します</p></td>
<td align="left"><p>オプション</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff548922(v=vs.85)" data-raw-source="[&lt;em&gt;RDF_READER_SWALLOW&lt;/em&gt;](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff548922(v=vs.85))"><em>RDF_READER_SWALLOW</em></a></p></td>
<td align="left"><p>機械的飲み込む</p></td>
<td align="left"><p>オプション</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff548923(v=vs.85)" data-raw-source="[&lt;em&gt;RDF_SET_PROTOCOL&lt;/em&gt;](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff548923(v=vs.85))"><em>RDF_SET_PROTOCOL</em></a></p></td>
<td align="left"><p>カードリーダー内のカードの伝送プロトコルを選択します。</p></td>
<td align="left"><p>Mandatory</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff548924(v=vs.85)" data-raw-source="[&lt;em&gt;RDF_TRANSMIT&lt;/em&gt;](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff548924(v=vs.85))"><em>RDF_TRANSMIT</em></a></p></td>
<td align="left"><p>データ転送を実行する</p></td>
<td align="left"><p>Mandatory</p></td>
</tr>
</tbody>
</table>

 

リーダードライバーは、これらのルーチンを呼び出すと、「[スマートカードドライバーのコールバック](https://docs.microsoft.com/windows-hardware/drivers/ddi/index)」で説明されているように、入力バッファーから呼び出し元のパラメーターを取得する必要があります。 また、リーダードライバーは、同じセクションで説明されているように、適切なバッファー領域に出力データを格納する必要があります。

カード追跡コールバックルーチン以外のコールバックルーチンが STATUS\_PENDING を返した場合、スマートカードライブラリは、リーダードライバーからのその他の呼び出しのサービスを停止します。 (カード追跡コールバックルーチンの詳細については、「 [*RDF\_カード\_の追跡*](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff548920(v=vs.85))」を参照してください)。ライブラリがこの状態にあるときに、リーダードライバーがドライバーライブラリルーチンを使用しようとすると、ライブラリルーチンは、状態\_デバイス\_ビジー状態の状態を返します。 これにより、リーダードライバーは、 [**Smartcarddevicecontrol**](https://docs.microsoft.com/previous-versions/ff548939(v=vs.85))を呼び出すことができない場合に ioctl 要求を処理できないので、リソースマネージャーからの ioctl 要求を、リーダードライバーが処理できないようにします。

 

 





