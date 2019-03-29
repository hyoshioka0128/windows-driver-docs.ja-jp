---
title: KSPROPERTY\_CAMERACONTROL\_拡張\_プロファイル
description: KSPROPERTY\_CAMERACONTROL\_拡張\_プロファイルを使用すると、どのプロファイルが選択されているカメラのドライバーに通知するためにキャプチャ フレームワークを許可します。 .
ms.assetid: 15467152-E514-4DAA-9905-2804802291A5
keywords:
- KSPROPERTY_CAMERACONTROL_EXTENDED_PROFILE ストリーミング メディア デバイス
topic_type:
- apiref
api_name:
- KSPROPERTY_CAMERACONTROL_EXTENDED_PROFILE
api_location:
- Ksmedia.h
api_type:
- HeaderDef
ms.date: 09/11/2018
ms.localizationpriority: medium
ms.openlocfilehash: fb3a15ff015592a8e4e11a6fdb2b76c43bf67ee0
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56573924"
---
# <a name="kspropertycameracontrolextendedprofile"></a>KSPROPERTY\_CAMERACONTROL\_拡張\_プロファイル

KSPROPERTY\_CAMERACONTROL\_拡張\_プロファイルを使用すると、どのプロファイルが選択されているカメラのドライバーに通知するためにキャプチャ フレームワークを許可します。

## <a name="usage-summary-table"></a>使用状況の概要テーブル

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<thead>
<tr class="header">
<th>Scope</th>
<th>コントロール</th>
<th>型</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>バージョン 1</p></td>
<td><p>フィルター</p></td>
<td><p>非同期のキャンセルされません。</p></td>
</tr>
</tbody>
</table>

次の表には、説明と要件が含まれています、 [ **KSCAMERA\_EXTENDEDPROP\_ヘッダー** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-tagkscamera_extendedprop_header)コントロールを使用する場合は、フィールドを構造体します。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>Member</th>
<th>説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>バージョン</p></td>
<td><p>これは、1 でなければなりません。</p></td>
</tr>
<tr class="even">
<td><p>PinId</p></td>
<td><p>KSCAMERA_EXTENDEDPROP_FILTERSCOPE (0 xffffffff) 必要があります。</p></td>
</tr>
<tr class="odd">
<td><p>サイズ</p></td>
<td><p>これは、sizeof(KSCAMERA_EXTENDEDPROP_HEADER) + sizeof(KSCAMERA_EXTENDEDPROP_PROFILE) である必要があります。</p></td>
</tr>
<tr class="even">
<td><p>結果</p></td>
<td><p>最後の設定操作のエラーの結果を示します。 設定操作が行われていない場合は必ず 0。</p></td>
</tr>
<tr class="odd">
<td><p>機能</p></td>
<td><p>KSCAMERA_EXTENDEDPROP_CAPS_ASYNCCONTROL 必要があります。 その他のモードがサポートされていません。</p></td>
</tr>
<tr class="even">
<td><p>フラグ</p></td>
<td><p>これは、0 でなければなりません。</p></td>
</tr>
</tbody>
</table>

## <a name="requirements"></a>必要条件

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>Header</p></td>
<td>Ksmedia.h</td>
</tr>
</tbody>
</table>
