---
title: KSK プロパティ\_CAMERACONTROL\_拡張\_プロファイル
description: KSK プロパティ\_CAMERACONTROL\_拡張\_プロファイルを使用して、キャプチャフレームワークが、選択されたプロファイルをカメラドライバーに通知できるようにします。 の順に移動します。
ms.assetid: 15467152-E514-4DAA-9905-2804802291A5
keywords:
- KSPROPERTY_CAMERACONTROL_EXTENDED_PROFILE ストリーミングメディアデバイス
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
ms.openlocfilehash: 4ff90b69dcaba0a6baccfd7698441d868b74820e
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72824008"
---
# <a name="ksproperty_cameracontrol_extended_profile"></a>KSK プロパティ\_CAMERACONTROL\_拡張\_プロファイル

KSK プロパティ\_CAMERACONTROL\_拡張\_プロファイルを使用して、キャプチャフレームワークが、選択されたプロファイルをカメラドライバーに通知できるようにします。

## <a name="usage-summary-table"></a>使用状況の概要テーブル

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<thead>
<tr class="header">
<th>適用範囲</th>
<th>コントロール</th>
<th>タスクバーの検索ボックスに</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>バージョン 1</p></td>
<td><p>フィルター</p></td>
<td><p>非同期 (キャンセル不可)</p></td>
</tr>
</tbody>
</table>

次の表に、コントロールを使用する場合の[**KSCAMERA\_EXTENDEDPROP\_ヘッダー**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-tagkscamera_extendedprop_header)構造体のフィールドの説明と要件を示します。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>メンバー</th>
<th>説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>バージョン</p></td>
<td><p>これは1である必要があります。</p></td>
</tr>
<tr class="even">
<td><p>PinId</p></td>
<td><p>KSCAMERA_EXTENDEDPROP_FILTERSCOPE (0xFFFFFFFF) である必要があります。</p></td>
</tr>
<tr class="odd">
<td><p>Size</p></td>
<td><p>これは sizeof (KSCAMERA_EXTENDEDPROP_HEADER) + sizeof (KSCAMERA_EXTENDEDPROP_PROFILE) である必要があります。</p></td>
</tr>
<tr class="even">
<td><p>結果</p></td>
<td><p>最後の設定操作のエラー結果を示します。 設定操作が行われていない場合は、0にする必要があります。</p></td>
</tr>
<tr class="odd">
<td><p>機能</p></td>
<td><p>KSCAMERA_EXTENDEDPROP_CAPS_ASYNCCONTROL である必要があります。 他のモードはサポートされていません。</p></td>
</tr>
<tr class="even">
<td><p>フラグ</p></td>
<td><p>0にする必要があります。</p></td>
</tr>
</tbody>
</table>

## <a name="requirements"></a>要件

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
