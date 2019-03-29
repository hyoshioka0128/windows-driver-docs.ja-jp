---
title: 先頭と末尾のエッジ ストリーム ポインター
description: 先頭と末尾のエッジ ストリーム ポインター
ms.assetid: 73ab974f-8034-421f-980a-2393d84ec54c
keywords:
- WDK AVStream、リードとトレーリング エッジのポインターをストリーム配信します。
- リーディング エッジ ストリーム ポインター WDK AVStream
- トレーリング エッジ ストリーム ポインター WDK AVStream
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: cba66bb34a726076a97d47d52022cd0427f50ff7
ms.sourcegitcommit: b3859d56cb393e698c698d3fb13519ff1522c7f3
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/05/2019
ms.locfileid: "57348843"
---
# <a name="leading-and-trailing-edge-stream-pointers"></a>先頭と末尾のエッジ ストリーム ポインター





既定では、各 AVStream キューを含む、*リーディング エッジ*ストリーム ポインター。 リーディング エッジは、キューに到着すると、新しいフレームを指します。 具体的には、リーディング エッジは最初に、キューに到着する最初のフレームをポイントし、ミニドライバーは、それを移動するまでは移動しません。 AVStream は、キューの有効期間が存在し、最先端を作成します。 ミニドライバーは、Microsoft によって提供される関数を使用してのリーディング エッジを操作できます。

キューに到着すると、新しいフレーム、AVStream は、フレームを既に指してされていないのリーディング エッジをこのフレームをポイントするリーディング エッジを設定します。

リーディング エッジ ストリーム ポインターへのポインターを取得するようにミニドライバーを呼び出す[ **KsPinGetLeadingEdgeStreamPointer**](https://msdn.microsoft.com/library/windows/hardware/ff563513)します。

すべてのリーディング エッジが次の表に示す 2 つの状況を進めるため、ミニドライバーが担当します。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>状況</th>
<th>AVStream の動作</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>フレームは、空のキューに到着します。</p></td>
<td><p>AVStream では、このフレームをポイントするリーディング エッジを設定します。</p></td>
</tr>
<tr class="even">
<td><p>リーディング エッジは、フレームを指します。 このフレームに対応する IRP が取り消されました。</p></td>
<td><p>AVStream のリーディング エッジを進めます。 リーディング エッジは、新しいフレームを指すようになりました。</p></td>
</tr>
</tbody>
</table>

 

参照してください[Stream ポインターの概要](introduction-to-stream-pointers.md)ストリーム ポインターを進めるの詳細についてはします。

### <a name="specifying-a-trailing-edge-stream-pointer"></a>トレーリング エッジの Stream ポインターを指定します。

ミニドライバーは、キューがトレーリング エッジ ストリーム ポインターがあることを指定できます。 トレーリング エッジは、通常、ミニドライバーに関心のある最も古いフレームを示します。 トレーリング エッジを指定する設定、KSPIN\_フラグ\_DISTINCT\_トレーリング\_EDGE フラグ、**フラグ**の関連メンバー [ **KSPIN\_記述子\_EX** ](https://msdn.microsoft.com/library/windows/hardware/ff563534)構造体。 呼び出して[ **KsPinGetTrailingEdgeStreamPointer** ](https://msdn.microsoft.com/library/windows/hardware/ff563518)トレーリング エッジ ストリーム ポインターへのポインターを取得します。

トレーリング エッジが進めますが既に 0 にドロップを指しているフレームとフレームの参照カウントが完了します。 シンク pin IRP を呼び出し元が完了すると、フレームが IRP を内に含まれる最後の場合は、ソース暗証番号 (pin) は、接続されている pin に IRP を送信します。

### <a name="maintaining-a-frame-window"></a>フレーム ウィンドウの管理

規則」で説明するフレームの参照カウントの結果として[Stream ポインターの概要](introduction-to-stream-pointers.md)、リードとトレーリング エッジの間のフレームが取り消されるまでキューに残ります<em>フレームがによって参照されていない場合でも、ストリーム ポインター</em>します。 そのため、ミニドライバーは複数の連続するフレームの作業ウィンドウを維持するためにリードとトレーリング エッジのポインターを使用できます。 フレーム ウィンドウには、処理するか、入力待ち状態可能性があります。

次の図では、最も古いフレームは、下部にあります。 新しいフレームは、上部に到達します。 各フレームの数は、そのフレームの参照カウントです。 ストリーム ポインターを進めるときにこのダイアグラム内移動します。

![avstream ストリーム ポインターをピン留めするキューの参照を示す図](images/cnstream4.png)

左端のキューでは、ミニドライバーがトレーリング エッジを使用して、フレームのワーキング セットを作成する方法を示します。 リードとトレーリング エッジの間には、各フレームでは、ストリーム ポインターにはこれらのフレームが参照されていないという事実に関係なく 1 つの参照カウントには。

中央のキューの例に示します[Stream ポインターの複製](cloning-stream-pointers.md)します。 ドライバーが繰り返しを複製し、暗証番号 (pin) プロセスの手順」の説明に従って、最先端を advanced [AVStream DMA サービス](avstream-dma-services.md)します。

最も右にあるキューでは、複製のストリーム ポインターを使用して、ミニドライバーがトレーリング エッジの背後にあるフレームの参照カウントを維持する方法を示します。

 

 




