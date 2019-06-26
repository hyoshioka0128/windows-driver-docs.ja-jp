---
title: WIA\_IPA\_項目\_サイズ
description: WIA\_IPA\_項目\_WIA 項目に関連付けられているデータのバイト単位で、現在のサイズが SIZE プロパティに含まれています。 WIA ミニドライバーは、作成し、このプロパティを保持します。
ms.assetid: af019c00-715b-43d1-ba14-f20c01871f35
keywords:
- WIA_IPA_ITEM_SIZE イメージング デバイス
topic_type:
- apiref
api_name:
- WIA_IPA_ITEM_SIZE
api_location:
- Wiadef.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2531c541d8af30d183952c9cd73e26d33a6bd69c
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67377318"
---
# <a name="wiaipaitemsize"></a>WIA\_IPA\_項目\_サイズ


WIA\_IPA\_項目\_WIA 項目に関連付けられているデータのバイト単位で、現在のサイズが SIZE プロパティに含まれています。 WIA ミニドライバーは、作成し、このプロパティを保持します。

## <span id="ddk_wia_ipa_item_size_si"></span><span id="DDK_WIA_IPA_ITEM_SIZE_SI"></span>


プロパティの種類:VT\_I4

有効な値 :WIA\_PROP\_NONE

アクセス権:読み取り専用かどうか

<a name="remarks"></a>注釈
-------

値を WIA\_IPA\_項目\_サイズ プロパティが含まれていますが転送されているデータの合計サイズです。 この値が 0 の場合は、WIA ミニドライバーは、データの正確なサイズに関する情報がありません。 (このような状況は、圧縮されたデータに対する共通)。

アプリケーションの読み取り WIA\_IPA\_項目\_で転送される前に、データのサイズを決定するサイズ。 WIA サービスは、データ転送のメモリの割り当てを支援するには、このプロパティを読み取ります。 データ転送の詳細については、次を参照してください。 [WIA アプリケーションにデータを転送する](https://docs.microsoft.com/windows-hardware/drivers/image/transferring-data-to-a-wia-application)します。

場合 WIA\_IPA\_項目\_サイズが 0 に設定されているとファイル転送するため TYMED が構成されている、WIA サービスが WIA ミニドライバーを任意のメモリを割り当てられません。

**注**   、WIA 設定だけで Windows Vista およびそれ以降のバージョンのオペレーティング システム\_IPA\_項目\_サイズ プロパティを自動ドキュメント サイズの検出が有効にすると、ADF 項目の 0 にします。

 

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

 

 





