---
title: WIA\_DPC\_キャプチャ\_遅延
description: WIA\_DPC\_キャプチャ\_遅延プロパティには、キャプチャのトリガーと実際の開始、データ キャプチャの間に挿入する必要がありますをミリ秒単位での遅延時間の量を表す値が含まれています。
ms.assetid: dc633117-88b1-4f09-ae64-160a53f75f73
keywords:
- WIA_DPC_CAPTURE_DELAY イメージング デバイス
topic_type:
- apiref
api_name:
- WIA_DPC_CAPTURE_DELAY
api_location:
- Wiadef.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6bf3a1acbd1a69aeada756c72b010ba39ba2dd7c
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56558510"
---
# <a name="wiadpccapturedelay"></a>WIA\_DPC\_キャプチャ\_遅延


WIA\_DPC\_キャプチャ\_遅延プロパティには、キャプチャのトリガーと実際の開始、データ キャプチャの間に挿入する必要がありますをミリ秒単位での遅延時間の量を表す値が含まれています。

## <span id="ddk_wia_dpc_capture_delay_si"></span><span id="DDK_WIA_DPC_CAPTURE_DELAY_SI"></span>


プロパティの種類:VT\_I4

有効な値 :WIA\_PROP\_リストまたは WIA\_PROP\_範囲

アクセス権:読み取り/書き込み

<a name="remarks"></a>注釈
-------

WIA\_DPC\_キャプチャ\_遅延プロパティをシングルによる開始のフレームの間の時間の記述に使用する必要はありません、個別の間隔のプロパティ (である時間の急増時や撮りなどの複数のキャプチャ[**WIA\_DPC\_バースト\_間隔**](wia-dpc-burst-interval.md)と[ **WIA\_DPC\_TIMELAPSE\_間隔**](wia-dpc-timelapse-interval.md)、それぞれ)。 その場合、WIA\_DPC\_キャプチャ\_遅延依然として機能を初期遅延、シリーズの最初のイメージをキャプチャしたら、前にフレーム間の時間に関係ありません。 Precapture 遅延なしに、このプロパティを 0 に設定

<a name="requirements"></a>要件
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>バージョン</p></td>
<td><p>Windows Vista 以降のオペレーティング システムで古いものであり使用できなくする必要があります。 ただし、アプリケーションやデバイス向けの Windows Server 2003、Windows XP、および Windows の以前のバージョンと互換性のこのプロパティが現在も Windows Vista で定義します。</p></td>
</tr>
<tr class="even">
<td><p>Header</p></td>
<td>Wiadef.h (Wiadef.h を含む)</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>関連項目


[**WIA\_DPC\_バースト\_間隔**](wia-dpc-burst-interval.md)

[**WIA\_DPC\_TIMELAPSE\_間隔**](wia-dpc-timelapse-interval.md)

 

 






