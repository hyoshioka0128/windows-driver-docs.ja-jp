---
title: 先頭と末尾のエッジ ストリーム ポインター
description: 先頭と末尾のエッジ ストリーム ポインター
ms.assetid: 73ab974f-8034-421f-980a-2393d84ec54c
keywords:
- ストリームポインター WDK AVStream、先頭および末尾のエッジ
- リーディングエッジストリームポインター WDK AVStream
- 末尾のエッジストリームポインター WDK AVStream
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: aebd11c4c4f3c7a3fda4a03b3075c237b98166d3
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72843044"
---
# <a name="leading-and-trailing-edge-stream-pointers"></a>先頭と末尾のエッジ ストリーム ポインター





既定では、各 AVStream キューには、*先頭のエッジ*ストリームポインターが含まれています。 先頭のエッジは、キューに到着した新しいフレームを指します。 具体的には、先頭のエッジは最初にキューに到達する最初のフレームを指し、ミニドライバーが移動するまでは移動しません。 AVStream は、キューの有効期間中に存在する先頭エッジを作成します。 ミニドライバーは、Microsoft が提供する関数を使用して最先端のエッジを操作できます。

新しいフレームがキューに到着すると、AVStream はこのフレームを指すように先頭のエッジを設定します。これは、先頭のエッジがまだフレームを指していないことが原因です。

ミニドライバーは、先頭のエッジストリームポインターへのポインターを取得するために[**KsPinGetLeadingEdgeStreamPointer**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/nf-ks-kspingetleadingedgestreampointer)を呼び出します。

ミニドライバーは、次の表に要約されている2つの状況のすべてで、最先端のエッジを進める役割を担います。

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
<td><p>前の空のキューにフレームが到着します。</p></td>
<td><p>AVStream は、このフレームを指すように先頭のエッジを設定します。</p></td>
</tr>
<tr class="even">
<td><p>先頭のエッジがフレームを指しています。 このフレームに対応する IRP は取り消されます。</p></td>
<td><p>AVStream は、最先端を進めます。 新しいフレームを指すようになりました。</p></td>
</tr>
</tbody>
</table>

 

ストリームポインターの進め方の詳細については、「[ストリームポインターの概要」を](introduction-to-stream-pointers.md)参照してください。

### <a name="specifying-a-trailing-edge-stream-pointer"></a>末尾のエッジストリームポインターの指定

ミニドライバーは、キューに末尾のエッジストリームポインターがあることを指定できます。 末尾のエッジは通常、ミニドライバーにとって最も古いフレームを示します。 末尾のエッジを指定するには、関連する[**kspin\_DESCRIPTOR\_EX**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-_kspin_descriptor_ex)構造体の**Flags**メンバーで、kspin\_フラグ\_DISTINCT\_末尾の\_エッジフラグを設定します。 次に、 [**KsPinGetTrailingEdgeStreamPointer**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/nf-ks-kspingettrailingedgestreampointer)を呼び出して、末尾のエッジストリームポインターへのポインターを取得します。

末尾のエッジが進むと、前にポイントしたフレームの参照カウントが0になり、フレームが完了します。 フレームが IRP 内に最後に含まれている場合、シンクピンは IRP を呼び出し元に対して完了します。ソースピンは、IRP を接続先の pin に送信します。

### <a name="maintaining-a-frame-window"></a>フレームウィンドウの保守

「ストリームポインターの[概要](introduction-to-stream-pointers.md)」で説明されているフレーム参照カウントルールの結果、<em>フレームがストリームポインターによって参照されていない場合でも</em>、先頭と末尾の境界の間のフレームはキャンセルされるまでキューに残ります。 そのため、ミニドライバーは、エッジの先頭と末尾のポインターを使用して、複数の連続したフレームの作業ウィンドウを維持することができます。 ウィンドウ内のフレームは、たとえば、処理または入力を待機している可能性があります。

次の図では、最も古いフレームが一番下にあります。 新しいフレームが上部に到達します。 各フレームの数値は、そのフレームの参照カウントです。 ストリームポインターが進むと、この図の上に移動します。

![ピンキューを参照する avstream ストリームポインターを示す図](images/cnstream4.png)

左端のキューは、ミニドライバーが最後のエッジを使用してフレームのワーキングセットを作成する方法を示しています。 これらのフレームを参照するストリームポインターがないという事実にかかわらず、先頭と末尾のエッジ間の各フレームの参照カウントは1になります。

中間キューは、[ストリームポインターを複製](cloning-stream-pointers.md)する例です。 [Avstream DMA サービス](avstream-dma-services.md)の [プロセスのピン留め] ステップで説明されているように、ドライバーは繰り返し複製されてから、最先端のエッジを高度に拡張しています。

右端のキューは、ストリームポインターの複製を使用して、ミニドライバーが末尾のエッジの背後にあるフレームの参照カウントを維持する方法を示しています。

 

 




