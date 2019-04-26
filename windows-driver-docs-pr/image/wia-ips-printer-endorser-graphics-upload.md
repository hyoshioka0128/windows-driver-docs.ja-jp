---
title: WIA\_IP\_プリンター\_裏書き\_グラフィックス\_アップロード
description: WIA\_IP\_プリンター\_裏書き\_グラフィックス\_アップロード プロパティは・ インプリント ・/裏書き項目のサポートがイメージ (グラフィック) データ転送をアップロードするかどうかを報告するために使用します。 このプロパティは初期化され、WIA ミニドライバーで維持されます。
ms.assetid: BCA1F340-5BF8-429A-90B9-9638E52E61DE
keywords:
- WIA_IPS_PRINTER_ENDORSER_GRAPHICS_UPLOAD イメージング デバイス
topic_type:
- apiref
api_name:
- WIA_IPS_PRINTER_ENDORSER_GRAPHICS_UPLOAD
api_location:
- Wiadef.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: d1271c01b4b643fcb128d8e834b1f19f36d86c89
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63352087"
---
# <a name="wiaipsprinterendorsergraphicsupload"></a>WIA\_IP\_プリンター\_裏書き\_グラフィックス\_アップロード


**WIA\_IP\_プリンター\_裏書き\_グラフィックス\_アップロード**・ インプリント ・/裏書き項目がイメージをアップロード (グラフィック) をサポートしているかどうかを報告するプロパティを使用データを転送します。 このプロパティは初期化され、WIA ミニドライバーで維持されます。




プロパティの種類:VT\_I4 (ブール値)

有効な値 :WIA\_PROP\_NONE

アクセス権:読み取り専用かどうか

<a name="remarks"></a>注釈
-------

このプロパティの現在の値が 0 以外の値 (True) に設定されている場合は、WIA ミニドライバーが WIA アプリケーションのクライアントによってアップロードされたイメージ データの受信をサポートしていることを意味します。 転送ファイルの形式は、 [ **WIA\_IPA\_形式**](wia-ipa-format.md)と[ **WIA\_IPA\_TYMED**](wia-ipa-tymed.md)同じ・ インプリント ・/裏書き項目で実装されるプロパティ。

このプロパティは、必要なの 0 以外の値 (True) を報告するすべての・ インプリント ・/裏書き項目に対して有効な[ **WIA\_IP\_プリンター\_裏書き\_グラフィックス**](wia-ips-printer-endorser-graphics.md)、常にレポートが 0 の値 (False) を実装することができます。 プロパティはそれ以外の場合有効ではありません。

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

 

 





