---
title: WIA\_IPA\_TYMED
description: WIA\_IPA\_TYMED プロパティには画像の転送方法の設定が含まれています。 WIA ミニドライバーは、作成し、このプロパティを保持します。
ms.assetid: 3490f4b8-a1ed-4ab3-b621-ed87ce8ae9ea
keywords:
- WIA_IPA_TYMED イメージング デバイス
topic_type:
- apiref
api_name:
- WIA_IPA_TYMED
api_location:
- Wiadef.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 55aa275754a5fad95cb53828f8b8080438096255
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63365969"
---
# <a name="wiaipatymed"></a>WIA\_IPA\_TYMED


WIA\_IPA\_TYMED プロパティには画像の転送方法の設定が含まれています。 WIA ミニドライバーは、作成し、このプロパティを保持します。

## <span id="ddk_wia_ipa_tymed_si"></span><span id="DDK_WIA_IPA_TYMED_SI"></span>


プロパティの種類:VT\_I4

有効な値 :WIA\_PROP\_一覧

アクセス権:読み取り/書き込み

<a name="remarks"></a>注釈
-------

アプリケーションの読み取り、WIA\_IPA\_TYMED プロパティのデータ転送のミニドライバーの方法を決定します。

次の表に、WIA で有効な定数\_IPA\_TYMED します。

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
<td><p>TYMED_CALLBACK</p></td>
<td><p>バンド内のメモリには、イメージを転送します。</p>
<p>この定数は、Windows Vista およびそれ以降のオペレーティング システムの廃止されています。</p></td>
</tr>
<tr class="even">
<td><p>TYMED_FILE</p></td>
<td><p>ファイルには、イメージを転送します。</p></td>
</tr>
<tr class="odd">
<td><p>TYMED_MULTIPAGE_CALLBACK</p></td>
<td><p>バンド内のメモリには、複数のイメージを転送します。</p>
<p>この定数は、Windows Vista およびそれ以降のオペレーティング システムの廃止されています。</p></td>
</tr>
<tr class="even">
<td><p>TYMED_MULTIPAGE_FILE</p></td>
<td><p>ファイルに複数のイメージを転送します。</p></td>
</tr>
</tbody>
</table>

 

すべての WIA 2.0 ミニドライバーは TYMED は、既定値にこのプロパティの初期値を設定する必要があります\_ファイル。

<a name="requirements"></a>要件
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>Header</p></td>
<td>Wiadef.h (Wiadef.h を含む)</td>
</tr>
</tbody>
</table>

 

 





