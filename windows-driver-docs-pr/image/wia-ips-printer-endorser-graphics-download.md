---
title: WIA\_IP\_プリンター\_裏書き\_グラフィックス\_ダウンロード
description: WIA\_IP\_プリンター\_裏書き\_グラフィックス\_・ インプリント ・/裏書き項目のサポートがイメージ (グラフィック) データ転送をダウンロードするかどうかを報告するダウンロードのプロパティを使用します。 このプロパティは初期化され、WIA ミニドライバーで維持されます。
ms.assetid: AE58548B-CB0A-45FE-A1C6-5C476061B89D
keywords:
- WIA_IPS_PRINTER_ENDORSER_GRAPHICS_DOWNLOAD イメージング デバイス
topic_type:
- apiref
api_name:
- WIA_IPS_PRINTER_ENDORSER_GRAPHICS_DOWNLOAD
api_location:
- Wiadef.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2bedbdc2d186a4352c7aaa19bbc29861fbf38220
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63388773"
---
# <a name="wiaipsprinterendorsergraphicsdownload"></a>WIA\_IP\_プリンター\_裏書き\_グラフィックス\_ダウンロード


**WIA\_IP\_プリンター\_裏書き\_グラフィックス\_ダウンロード**・ インプリント ・/裏書き項目がダウンロードをサポートしているかどうかを報告するプロパティが使用されるイメージ (グラフィック) データを転送します。 このプロパティは初期化され、WIA ミニドライバーで維持されます。




プロパティの種類:VT\_I4 (ブール値)

有効な値 :WIA\_PROP\_NONE

アクセス権:読み取り専用かどうか

<a name="remarks"></a>注釈
-------

このプロパティの現在の値が 0 以外の値 (True) に設定されている場合に WIA アプリケーションのクライアントによってダウンロードされたイメージ データを転送する WIA ミニドライバーをサポートしていることを意味します。 転送ファイルの形式は、 [ **WIA\_IPA\_形式**](wia-ipa-format.md)と[ **WIA\_IPA\_TYMED**](wia-ipa-tymed.md)同じ・ インプリント ・/裏書き項目で実装されるプロパティ。

このプロパティは、必要なの 0 以外の値 (True) を報告するすべての・ インプリント ・/裏書き項目に対して有効な[ **WIA\_IP\_プリンター\_裏書き\_グラフィックス**](wia-ips-printer-endorser-graphics.md)、常にレポートが 0 の値 (False) を実装することができます。 プロパティはそれ以外の場合有効ではありません。

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

 

 





