---
title: WIA\_IP\_プリンター\_裏書き\_テキスト\_アップロード
description: WIA\_IP\_プリンター\_裏書き\_テキスト\_アップロード プロパティは・ インプリント ・/裏書き項目のサポートがテキスト データの転送をアップロードするかどうかを報告するために使用します。 WIA ミニドライバーは、作成し、このプロパティを保持します。
ms.assetid: FE239B61-6656-462B-A962-2101A1F0C683
keywords:
- WIA_IPS_PRINTER_ENDORSER_TEXT_UPLOAD イメージング デバイス
topic_type:
- apiref
api_name:
- WIA_IPS_PRINTER_ENDORSER_TEXT_UPLOAD
api_location:
- Wiadef.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: def9f8c1db230865a5da8d76644a6a9a1a74248a
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63387229"
---
# <a name="wiaipsprinterendorsertextupload"></a>WIA\_IP\_プリンター\_裏書き\_テキスト\_アップロード


**WIA\_IP\_プリンター\_裏書き\_テキスト\_アップロード**・ インプリント ・/裏書き項目のサポートがテキスト データの転送をアップロードするかどうかを報告するプロパティを使用します。 WIA ミニドライバーは、作成し、このプロパティを保持します。




プロパティの種類:VT\_I4 (ブール値)

有効な値 :WIA\_PROP\_NONE

アクセス権:読み取り専用かどうか

<a name="remarks"></a>注釈
-------

このプロパティの現在の値がの値に設定されている場合は、True (0 以外)、WIA ミニドライバーは、アプリケーションのクライアントによってアップロードされるテキスト データの受信をサポートしています。 転送ファイルの形式は、 [ **WIA\_IPA\_形式**](wia-ipa-format.md)と[ **WIA\_IPA\_TYMED**](wia-ipa-tymed.md)同じ・ インプリント ・/裏書き項目で実装されるプロパティ。

このプロパティは必須のすべての・ インプリント ・/裏書き項目が常に 0 (False) の値をレポートに実装できます。 また、WiaItemTypeFile と WiaItemTypeTransfer ・ インプリント ・/裏書き項目を報告する場合このプロパティが必要です (True)、0 以外の値を報告する必要があります。

<a name="requirements"></a>必要条件
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

 

 





