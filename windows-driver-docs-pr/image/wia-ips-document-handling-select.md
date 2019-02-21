---
title: WIA\_IP\_ドキュメント\_処理\_を選択します
description: WIA\_IP\_ドキュメント\_処理\_プロパティ選択にはでは、現在のスキャナーの取得元とモードが含まれています。
ms.assetid: f148e91f-847c-4db2-8459-9f52892cd703
keywords:
- WIA_IPS_DOCUMENT_HANDLING_SELECT イメージング デバイス
topic_type:
- apiref
api_name:
- WIA_IPS_DOCUMENT_HANDLING_SELECT
api_location:
- Wiadef.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 387850c5e7a7baab4af22e4e4dd2ddcfdec59fa4
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56532142"
---
# <a name="wiaipsdocumenthandlingselect"></a>WIA\_IP\_ドキュメント\_処理\_を選択します


WIA\_IP\_ドキュメント\_処理\_プロパティ選択にはでは、現在のスキャナーの取得元とモードが含まれています。

プロパティの種類:VT\_I4

有効な値 :WIA\_PROP\_フラグ

アクセス権:読み取り/書き込み

<a name="remarks"></a>注釈
-------

アプリケーションの読み取り、WIA\_IP\_ドキュメント\_処理\_スキャナー、またはアプリケーションの現在の取得のソースを決定するプロパティの選択元のモードを設定するには、このプロパティの書き込み、スキャナーです。 さらに、アプリケーションは、このプロパティを使用を有効にし、両面印刷機能を無効にします。 WIA ミニドライバーは、作成し、このプロパティを保持します。

次の表では、Windows vista では有効であり、以降のみである定数について説明します。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>Value</th>
<th>定義</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>ADVANCED_DUPLEX</p></td>
<td><p>各子フィーダー項目 (WIA_CATEGORY_FEEDER_FRONT および WIA_CATEGORY_FEEDER_BACK) の個々 の構成設定を使用してスキャンします。 このフラグは、二重と共に設定することはできません。</p>
<p>さまざまなサポートが前面の設定をスキャンし、項目のバックアップ デバイスは、省略可能な ADF の前面を実装する必要がある、バック項目とは、双方向と ADVANCED_DUPLEX の両方をサポートする必要があります。</p></td>
</tr>
</tbody>
</table>

 

次の表では、Windows Vista と Windows XP の有効な定数について説明します。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>Value</th>
<th>定義</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>BACK_FIRST</p></td>
<td><p>まず、ドキュメントの背面をスキャンします。 この値は、双方向に設定されている場合にのみ有効です。</p></td>
</tr>
<tr class="even">
<td><p>BACK_ONLY</p></td>
<td><p>背面のスキャン<em>のみ</em>します。 この値は、双方向に設定されている場合にのみ有効です。</p></td>
</tr>
<tr class="odd">
<td><p>双方向</p></td>
<td><p>両面印刷ユニット操作を使用してスキャンします。</p></td>
</tr>
<tr class="even">
<td><p>FRONT_FIRST</p></td>
<td><p>まず、ドキュメントの先頭をスキャンします。 この値は、双方向に設定されている場合にのみ有効です。</p></td>
</tr>
<tr class="odd">
<td><p>FRONT_ONLY</p></td>
<td><p>スキャン<em>のみ</em>します。</p></td>
</tr>
</tbody>
</table>

 

二重、前面の値\_のみが相互に排他的--セット 1 つまたは両方ではなく、その他。

WIA 2.0 ミニドライバーは、既定値は前面にこのプロパティの初期値を設定する必要があります\_のみです。 この要件の確認に失敗した、ミニドライバーは WIA 1.0 の一般的なスキャン ダイアログと一部の WIA 1.0 アプリケーション互換性のないことがあります。

次の表は Windows XP では有効ですが、以降は Windows Vista で廃止されましたされる定数について説明します。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>Value</th>
<th>定義</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>AUTO_ADVANCE</p></td>
<td><p>スキャン後、次のドキュメントの供給を自動有効にします。</p></td>
</tr>
<tr class="even">
<td><p>フィーダー</p></td>
<td><p>ドキュメント フィーダーを使用してスキャンします。</p></td>
</tr>
<tr class="odd">
<td><p>フラット ベッド</p></td>
<td><p>フラット ベッドを使用してスキャンします。</p></td>
</tr>
<tr class="even">
<td><p>NEXT_PAGE</p></td>
<td><p>ドキュメントの次のページをスキャンします。</p></td>
</tr>
<tr class="odd">
<td><p>PREFEED</p></td>
<td><p>事前にフィードのモードを有効にします。 スキャン中に次のドキュメントの位置。</p></td>
</tr>
</tbody>
</table>

 

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
<td><p>Windows Vista およびそれ以降のオペレーティング システムで使用できます。 Windows xp では、同じ WIA_DPS_DOCUMENT_HANDLING_SELECT プロパティを使用します。</p></td>
</tr>
<tr class="even">
<td><p>Header</p></td>
<td>Wiadef.h (Wiadef.h を含む)</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>関連項目


[**WIA\_DPS\_ドキュメント\_処理\_を選択します**](wia-dps-document-handling-select.md)

 

 






