---
title: WIA\_IP\_ページ\_幅
description: WIA\_IP\_ページ\_WIDTH プロパティには、選択した状態で 1/1000 インチの現在のページの幅が含まれています (. 001)。 WIA ミニドライバーは、作成し、このプロパティを保持します。
ms.assetid: b72d32bf-6f1b-4eb2-8f7c-f0de4e2caf26
keywords:
- WIA_IPS_PAGE_WIDTH イメージング デバイス
topic_type:
- apiref
api_name:
- WIA_IPS_PAGE_WIDTH
api_location:
- Wiadef.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 15d587ea9ab9ff4985d8004e4024044999a77a3d
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56580214"
---
# <a name="wiaipspagewidth"></a>WIA\_IP\_ページ\_幅


WIA\_IP\_ページ\_WIDTH プロパティには、選択した状態で 1/1000 インチの現在のページの幅が含まれています (. 001)。 WIA ミニドライバーは、作成し、このプロパティを保持します。

プロパティの種類:VT\_I4

有効な値 :WIA\_PROP\_NONE

アクセス権:読み取り専用です。

<a name="remarks"></a>コメント
-------

アプリケーションは、WIA を読み取ります\_IP\_ページ\_スキャンされているページの物理的なサイズを決定する幅。 エクステント設定が既知のページ サイズと異なる場合、このプロパティは、ページの幅を報告が[ **WIA\_IP\_ページ\_サイズ**](wia-ips-page-size.md)プロパティに設定WIA\_ページ\_カスタム。

WIA\_IP\_ページ\_幅は、WIA の値と同期する必要があります\_IP\_XEXTENT、ピクセル単位にスキャンするページの幅を報告します。

**注**   WIA サービス内で互換レイヤーは、WIA のサポートを追加していない\_IP\_ページ\_幅プロパティの場合は、Windows XP WIA デバイスから変換されたです、ADF 項目をプロパティデバイスの子項目ではサポートされません。 アプリケーションでは常に WIA をサポートするために ADF 項目は期待できません\_IP\_ページ\_幅かどうかは、実行時にサポートを常に確認する必要があります。 (通常は、アプリケーションが確認をネゴシエートする任意のプロパティのサポート)。

 

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
<td><p>Windows Vista およびそれ以降のオペレーティング システムで使用できます。 Windows XP では、代わりに WIA_DPS_PAGE_WIDTH プロパティを使用します。</p></td>
</tr>
<tr class="even">
<td><p>Header</p></td>
<td>Wiadef.h (Wiadef.h を含む)</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>関連項目


[**WIA\_DPS\_ページ\_幅**](wia-dps-page-width.md)

[**WIA\_IP\_ページ\_高さ**](wia-ips-page-height.md)

[**WIA\_IP\_ページ\_サイズ**](wia-ips-page-size.md)

 

 






