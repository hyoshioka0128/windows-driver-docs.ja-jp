---
title: WIA\_DPC\_露出\_メータリング\_モード
description: WIA\_DPC\_露出\_メータリング\_モード プロパティは、カメラを使用して、危険度の設定を自動的に調整するモードを指定します。
ms.assetid: f1340ba2-984e-41a1-a6f2-56639f60d94a
keywords:
- WIA_DPC_EXPOSURE_METERING_MODE イメージング デバイス
topic_type:
- apiref
api_name:
- WIA_DPC_EXPOSURE_METERING_MODE
api_location:
- Wiadef.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 518ad08cb786126c1554001f8e877418932169dc
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63379605"
---
# <a name="wiadpcexposuremeteringmode"></a>WIA\_DPC\_露出\_メータリング\_モード


WIA\_DPC\_露出\_メータリング\_モード プロパティは、カメラを使用して、危険度の設定を自動的に調整するモードを指定します。

## <span id="ddk_wia_dpc_exposure_metering_mode_si"></span><span id="DDK_WIA_DPC_EXPOSURE_METERING_MODE_SI"></span>


プロパティの種類:VT\_I4

有効な値 :WIA\_PROP\_一覧

アクセス権:読み取り/書き込み

<a name="remarks"></a>注釈
-------

次の表は、WIA で有効な定数\_DPC\_露出\_メータリング\_モード プロパティです。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>値</th>
<th>定義</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>EXPOSUREMETERING_AVERAGE</p></td>
<td><p>シーン全体の平均に基づいて露出を設定します。</p></td>
</tr>
<tr class="even">
<td><p>EXPOSUREMETERING_CENTERSPOT</p></td>
<td><p>センターの場所に基づく露出を設定します。</p></td>
</tr>
<tr class="odd">
<td><p>EXPOSUREMETERING_CENTERWEIGHT</p></td>
<td><p>Center 加重平均値に基づいて露出を設定します。</p></td>
</tr>
<tr class="even">
<td><p>EXPOSUREMETERING_MULTISPOT</p></td>
<td><p>Multispot パターンに基づく露出を設定します。</p></td>
</tr>
</tbody>
</table>

 

<a name="requirements"></a>必要条件
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

 

 





