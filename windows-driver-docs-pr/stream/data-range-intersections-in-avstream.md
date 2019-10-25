---
title: AVStream のデータ範囲の交差
description: AVStream のデータ範囲の交差
ms.assetid: 44281574-8258-47a3-857d-fd44bb949f17
keywords:
- データの共通部分 (WDK AVStream)
- WDK AVStream の共通部分
- データ形式 WDK AVStream
- データ範囲 WDK AVStream
- WDK AVStream の範囲
- WDK AVStream の形式
- データ範囲の固定 WDK
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3eb4dc3ba6a88eb27b335d4647eddf384dc6ae6d
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72837720"
---
# <a name="data-range-intersections-in-avstream"></a>AVStream のデータ範囲の交差





データ形式は、接続の一部の側面を記述するパラメーターの1つのセットです。 たとえば、オーディオデータ形式では、特定の形式のオーディオ (1 秒あたりの X サンプル数と、サンプルあたりの Y ビット) を指定できます。

データ範囲では、有効なパラメーターのシーケンスを指定します。 たとえば、オーディオデータ範囲では、特定の形式のオーディオを、1秒あたりのサンプル数と、サンプルあたりの C-D ビットで指定できます。

ミニドライバーは、対応する[**Kspin\_記述子**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-kspin_descriptor)構造の**DataRanges**メンバーの特定のピンに対してサポートするデータ範囲の一覧を提供します。

AVStream では、ミニドライバーはミニドライバーで指定さ**れたコール**バック[ **\_\_** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-_kspin_descriptor_ex)ルーチンへのポインターを提供することで、独自のデータ範囲の交差ハンドラーを提供できます。 AVStream を範囲と交差させるには、このメンバーを**NULL**に設定します。 コールバックルーチンを定義する方法については、「 [*AVStrMiniIntersectHandlerEx*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/nc-ks-pfnksintersecthandlerex) 」を参照してください。

ミニドライバーが intersect ハンドラーを提供する場合、積集合を作成する必要がある場合、ミニドライバーは、メジャー型、サブ形式、および指定子と一致する2つのデータ範囲を受け取ります。 また、データ範囲の必須の属性も一致します。

範囲が交差し、 *AVStrMiniIntersectHandlerEx*コールバックルーチンの**Data**パラメーターに十分なバッファー領域が指定されている場合、交差ルーチンは交差部分の形式を選択し、バッファー内の呼び出し元に返します。**データ**によってポイントされます。

2つのデータ範囲が交差しない場合、ハンドラーは状態\_返し\_一致しません。

ミニドライバーが[*AVStrMiniPinSetDataFormat*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/nc-ks-pfnkspinsetdataformat)ディスパッチを指定した場合、avstream はこのディスパッチを呼び出して、avstream が pin に特定の形式を設定していることをミニドライバーに通知します。 [**Kspin\_ディスパッチ**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-_kspin_dispatch)構造体の**SetDataFormat**メンバーの*AVStrMiniPinSetDataFormat* callback ルーチンへのポインターを指定します。 (SRB\_*AVStrMiniPinSetDataFormat*の代わりに[**データ\_形式\_設定**](https://docs.microsoft.com/windows-hardware/drivers/stream/srb-set-data-format)されている[stream クラス](https://docs.microsoft.com/windows-hardware/drivers/ddi/_stream/index)のクライアントであるミニドライバーです)。

ミニドライバーは、 *AVStrMiniPinSetDataFormat*とは\_一致しない状態\_返すことで、提案された形式を拒否できます。

Pin が作成される前の[*AVStrMiniPinSetDataFormat*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/nc-ks-pfnkspinsetdataformat)の初回呼び出しに加えて、ミニドライバーは PIN が実行状態に移行する直前に2つ目の*AVStrMiniPinSetDataFormat*呼び出しを受け取る可能性があります。 AVStream または stream クラスクライアントがビデオキャプチャミニドライバーで、このような通知を受信した場合、*このディスパッチには実際のサーフェイスパラメーターが含まれ*ます。 可能であれば、ミニドライバーはこの2番目の形式の変更に失敗しないようにする必要があります。 2番目のディスパッチ呼び出しが発生すると想定しないでください。

ミニドライバーは、最後に成功した*AVStrMiniPinSetDataFormat*ディスパッチに含まれていた形式でデータをキャプチャする必要があります。

 

 




