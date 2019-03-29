---
title: AVStream のデータ範囲の交差
description: AVStream のデータ範囲の交差
ms.assetid: 44281574-8258-47a3-857d-fd44bb949f17
keywords:
- データの交差部分を WDK AVStream
- WDK AVStream の交差部分
- データ形式の WDK AVStream
- データの範囲は WDK AVStream
- WDK AVStream を範囲します。
- WDK AVStream を書式設定します。
- 暗証番号 (pin) のデータ範囲 WDK
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ba6d8656959f8125ef7da6d970b153d773317042
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56571409"
---
# <a name="data-range-intersections-in-avstream"></a>AVStream のデータ範囲の交差





データ形式は、接続の一部の側面を記述するパラメーターの 1 つのセットです。 たとえば、オーディオ データ形式は X 秒あたりのサンプルとサンプルあたりのビット数 Y でオーディオの特定の形式を指定する可能性があります。

データ範囲は、有効なパラメーターのシーケンスを指定します。 たとえば、オーディオ データの範囲は、2 番目と C D サンプルごとのビットごとの A B サンプルでオーディオの特定の形式を指定できます。

ミニドライバーで特定の pin をサポートするデータ範囲の一覧を示します、 **DataRanges**の対応するメンバー [ **KSPIN\_記述子**](https://msdn.microsoft.com/library/windows/hardware/ff563533)構造体。

AVStream、ミニドライバーは、内のミニドライバーで提供されるコールバック ルーチンへのポインターを提供することで独自のデータ範囲の交差部分ハンドラーを提供できます、 **IntersectHandler**のメンバー、 [ **KSPIN\_記述子\_EX**](https://msdn.microsoft.com/library/windows/hardware/ff563534)します。 範囲の交差 AVStream させるには、このメンバーを設定**NULL**します。 参照してください[ *AVStrMiniIntersectHandlerEx* ](https://msdn.microsoft.com/library/windows/hardware/ff556326)にコールバック ルーチンを定義する方法について説明します。

交差にする必要がある場合、ミニドライバーは、intersect ハンドラーを提供する場合、ミニドライバーはサブフォーマット、および指定子の主な種類の一致する 2 つのデータ範囲を受け取ります。 さらに、データの範囲の必要な属性が一致します。

範囲の積集合およびに十分なバッファー領域が提供されているかどうか、**データ**のパラメーター、 *AVStrMiniIntersectHandlerEx*コールバック ルーチンでは、交差ルーチンが、形式で、指すバッファーに呼び出し元に返し、交差**データ**します。

2 つのデータ範囲が交差しない場合、ハンドラーがステータスを返します\_いいえ\_一致します。

ミニドライバーが指定されている場合、 [ *AVStrMiniPinSetDataFormat* ](https://msdn.microsoft.com/library/windows/hardware/ff556355)ディスパッチ、AVStream AVStream が、ピンで、特定の形式を設定しているようにミニドライバーに通知するには、このディスパッチを呼び出します。 ポインターを提供、 *AVStrMiniPinSetDataFormat*コールバック ルーチンで、 **SetDataFormat**のメンバー、 [ **KSPIN\_ディスパッチ**](https://msdn.microsoft.com/library/windows/hardware/ff563535)構造体。 (ミニドライバーのクライアントである[クラスのストリーム](https://msdn.microsoft.com/library/windows/hardware/ff568275)受信[ **SRB\_設定\_データ\_形式**](https://msdn.microsoft.com/library/windows/hardware/ff568201) ではなく*AVStrMiniPinSetDataFormat*)。

ミニドライバーは、提案された形式を拒否する状態を返すことによって\_いいえ\_から一致*AVStrMiniPinSetDataFormat*します。

最初の呼び出しだけでなく[ *AVStrMiniPinSetDataFormat* ](https://msdn.microsoft.com/library/windows/hardware/ff556355) 、暗証番号 (pin) が作成される前に、ミニドライバーは、2 つ目を受け取ることが*AVStrMiniPinSetDataFormat*を呼び出す直前に実行状態にピン留めする遷移します。 AVStream またはストリーム クラス クライアントがビデオ キャプチャ ミニドライバーと、このような通知を受け取る場合*ディスパッチには、実際の画面のパラメーターが含まれています。* します。 可能であれば、この 2 つ目の形式変更、ミニドライバーは失敗しません。 2 番目のディスパッチ呼び出しが行われることを前提としてはいません。

ミニドライバーは、どのような形式は、最後に含まれていたでデータをキャプチャする必要があります成功*AVStrMiniPinSetDataFormat*ディスパッチします。

 

 




