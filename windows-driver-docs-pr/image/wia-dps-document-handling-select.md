---
title: WIA\_DPS\_ドキュメント\_処理\_を選択します
description: WIA\_DPS\_ドキュメント\_処理\_プロパティ選択にはでは、現在のスキャナーの取得元とモードが含まれています。
ms.assetid: 17964dc5-8008-4f9c-abcd-cc72c1d6c398
keywords:
- WIA_DPS_DOCUMENT_HANDLING_SELECT イメージング デバイス
topic_type:
- apiref
api_name:
- WIA_DPS_DOCUMENT_HANDLING_SELECT
api_location:
- Wiadef.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: b75d37f14a8a533f0b95ac85b809839faf7bb9fe
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56572471"
---
# <a name="wiadpsdocumenthandlingselect"></a>WIA\_DPS\_ドキュメント\_処理\_を選択します


WIA\_DPS\_ドキュメント\_処理\_プロパティ選択にはでは、現在のスキャナーの取得元とモードが含まれています。

## <span id="ddk_wia_dps_document_handling_select_si"></span><span id="DDK_WIA_DPS_DOCUMENT_HANDLING_SELECT_SI"></span>


プロパティの種類:VT\_I4

有効な値 :WIA\_PROP\_フラグ

アクセス権:読み取り/書き込み

<a name="remarks"></a>コメント
-------

アプリケーションの読み取り、WIA\_DPS\_ドキュメント\_処理\_スキャナー、またはアプリケーションの現在の取得のソースを決定するプロパティを選択しますが、ソースとのモードを設定するには、このプロパティを書き込み、スキャナーです。 さらに、アプリケーションは、このプロパティを使用を有効にし、両面印刷機能を無効にします。 WIA ミニドライバーは、作成し、このプロパティを保持します。

次の表に、WIA で有効な定数\_DPS\_ドキュメント\_処理\_を選択します。

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

次の表は Microsoft Windows XP では、このプロパティで有効ですが、Windows Vista で廃止され、以降では、定数について説明します。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>[値]</th>
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
<td><p>事前にフィードのモードを有効にします。 スキャン中に次のドキュメントを前置詞します。</p></td>
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
<td><p>Microsoft Windows XP で使用できます。 Windows Vista 以降では、WIA_IPS_DOCUMENT_HANDLING_SELECT プロパティを使用します。</p></td>
</tr>
<tr class="even">
<td><p>Header</p></td>
<td>Wiadef.h (Wiadef.h を含む)</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>関連項目


[**WIA\_IP\_ドキュメント\_処理\_を選択します**](wia-ips-document-handling-select.md)

 

 






