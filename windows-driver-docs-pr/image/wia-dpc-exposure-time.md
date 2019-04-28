---
title: WIA\_DPC\_露出\_時間
description: WIA\_DPC\_露出\_を 10,000 でスケールを秒単位で時間プロパティは、シャッター スピードに対応します。
ms.assetid: 78f12aaa-4b7b-4ba3-a6af-791e97581d26
keywords:
- WIA_DPC_EXPOSURE_TIME イメージング デバイス
topic_type:
- apiref
api_name:
- WIA_DPC_EXPOSURE_TIME
api_location:
- Wiadef.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 63bd9173546332a2e795d2d7f79aea59d0c27f50
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63379599"
---
# <a name="wiadpcexposuretime"></a>WIA\_DPC\_露出\_時間


WIA\_DPC\_露出\_を 10,000 でスケールを秒単位で時間プロパティは、シャッター スピードに対応します。

## <span id="ddk_wia_dpc_exposure_time_si"></span><span id="DDK_WIA_DPC_EXPOSURE_TIME_SI"></span>


プロパティの種類:VT\_I4

有効な値 :WIA\_PROP\_範囲または WIA\_PROP\_一覧

アクセス権:読み取り/書き込み

<a name="remarks"></a>注釈
-------

通常、デバイスを使用、WIA\_DPC\_露出\_時間プロパティ場合にのみ、 [ **WIA\_DPC\_露出\_モード**](wia-dpc-exposure-mode.md)プロパティ EXPOSUREMODE\_手動] または [EXPOSUREMODE\_シャッター\_優先順位。

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


[**WIA\_DPC\_露出\_モード**](wia-dpc-exposure-mode.md)

 

 






