---
title: WIA\_IP\_プリンター\_裏書き\_テキスト\_ダウンロード
description: WIA\_IP\_プリンター\_裏書き\_テキスト\_・ インプリント ・/裏書き項目のサポートがテキスト データの転送をダウンロードするかどうかを報告するダウンロードのプロパティを使用します。 WIA ミニドライバーは、作成し、このプロパティを保持します。
ms.assetid: AEFF6C6F-8DA9-4AFF-8614-A1134C7C499C
keywords:
- WIA_IPS_PRINTER_ENDORSER_TEXT_DOWNLOAD イメージング デバイス
topic_type:
- apiref
api_name:
- WIA_IPS_PRINTER_ENDORSER_TEXT_DOWNLOAD
api_location:
- Wiadef.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: f6438233e31552ef13b1118a2972c30e276eb36e
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63351097"
---
# <a name="wiaipsprinterendorsertextdownload"></a>WIA\_IP\_プリンター\_裏書き\_テキスト\_ダウンロード


WIA\_IP\_プリンター\_裏書き\_テキスト\_・ インプリント ・/裏書き項目のサポートがテキスト データの転送をダウンロードするかどうかを報告するダウンロードのプロパティを使用します。 WIA ミニドライバーは、作成し、このプロパティを保持します。




プロパティの種類:VT\_I4 (ブール値)

有効な値 :WIA\_PROP\_NONE

アクセス権:読み取り専用かどうか

<a name="remarks"></a>注釈
-------

このプロパティの現在の値がの値に設定されている場合は、True (0 以外)、WIA ミニドライバーは、アプリケーションのクライアントによってアップロードされるテキスト データの受信をサポートしています。 転送ファイルの形式は、 [ **WIA\_IPA\_形式**](wia-ipa-format.md)と[ **WIA\_IPA\_TYMED**](wia-ipa-tymed.md)同じ・ インプリント ・/裏書き項目で実装されるプロパティ。

このプロパティが必要ですが・ インプリント ・/裏書きのすべての項目の値を 0 (False) を常に報告を実装できます。

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

 

 





