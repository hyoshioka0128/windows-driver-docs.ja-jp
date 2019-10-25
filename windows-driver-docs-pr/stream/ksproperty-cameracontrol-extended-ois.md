---
title: KSK プロパティ\_CAMERACONTROL\_EXTENDED\_OIS
description: KSK プロパティ\_CAMERACONTROL\_EXTENDED\_OIS は、ドライバー上の光学イメージ安定化 (OIS) の制御に使用されるプロパティ ID です。
ms.assetid: CF4F1283-1517-4F93-8554-FBD4B068A655
keywords:
- KSPROPERTY_CAMERACONTROL_EXTENDED_OIS ストリーミングメディアデバイス
topic_type:
- apiref
api_name:
- KSPROPERTY_CAMERACONTROL_EXTENDED_OIS
api_location:
- Ksmedia.h
api_type:
- HeaderDef
ms.date: 09/11/2018
ms.localizationpriority: medium
ms.openlocfilehash: 51f26d1ba657d335bc5b58510549ad06827836a8
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72841594"
---
# <a name="ksproperty_cameracontrol_extended_ois"></a>KSK プロパティ\_CAMERACONTROL\_EXTENDED\_OIS

**Ksk プロパティ\_CAMERACONTROL\_EXTENDED\_OIS**は、ドライバー上の光学イメージ安定化 (ois) の制御に使用されるプロパティ ID です。

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
<td><p>同期</p></td>
</tr>
</tbody>
</table>

次のフラグは、 **KSCAMERA\_EXTENDEDPROP\_ヘッダーに配置できます。** 光学式イメージの安定化を制御するフラグフィールド。 AUTO がサポートされている場合は、既定値は AUTO、それ以外の場合はになります。

```cpp
#define KSCAMERA_EXTENDEDPROP_OIS_OFF   0x0000000000000000
#define KSCAMERA_EXTENDEDPROP_OIS_ON    0x0000000000000001
#define KSCAMERA_EXTENDEDPROP_OIS_AUTO  0x0000000000000002 
```

ドライバーがこのコントロールをサポートしている場合は、OIS\_ON をサポートし、OIS\_OFF をサポートする必要があります。

ドライバーで光学イメージの安定化がサポートされていない場合、ドライバーはこのコントロールを実装しないでください。

このコントロールの SET 呼び出しは、ビデオまたはフォトピンが KSK 状態\_実行状態の場合には効果がありません。 ビデオまたはフォト pin が実行中状態の場合、ドライバーは受信した設定呼び出しを拒否し、デバイス\_状態\_無効\_状態を返します。 GET 呼び出しでは、ドライバーは Flags フィールドの現在の設定を返します。

次の表では、フラグ機能について説明します。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>Flag</th>
<th>説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>KSCAMERA_EXTENDEDPROP_OIS_OFF</p></td>
<td><p>これは必須の機能です。 指定した場合、ドライバーでは光学イメージの安定化が無効になります。</p></td>
</tr>
<tr class="even">
<td><p>KSCAMERA_EXTENDEDPROP_OIS_ON</p></td>
<td><p>これは必須の機能です。 指定すると、ドライバーで光学イメージの安定化が有効になります。 このフラグは、OIS_AUTO および OIS_OFF フラグと同時に指定することはできません。</p></td>
</tr>
<tr class="odd">
<td><p>KSCAMERA_EXTENDEDPROP_OIS_AUTO</p></td>
<td><p>この機能は省略可能です。 指定した場合、このような機能をサポートするドライバーは、光学イメージの安定化をオンまたはオフにする必要があるかどうかを判断します。 このフラグは、OIS_ON および OIS_OFF フラグと同時に指定することはできません。</p></td>
</tr>
</tbody>
</table>

次の表には、コントロールを使用する場合の[**KSCAMERA\_EXTENDEDPROP\_ヘッダー**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-tagkscamera_extendedprop_header)構造のフィールドの説明と要件が含まれています。

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
<td><p>これは KSCAMERA_EXTENDEDPROP_FILTERSCOPE (0xFFFFFFFF) である必要があります。</p></td>
</tr>
<tr class="odd">
<td><p>Size</p></td>
<td><p>これは sizeof (KSCAMERA_EXTENDEDPROP_HEADER) + sizeof (KSCAMERA_EXTENDEDPROP_VALUE) である必要があります。</p></td>
</tr>
<tr class="even">
<td><p>結果</p></td>
<td><p>最後の設定操作のエラー結果を示します。 設定操作が行われていない場合は、0にする必要があります。</p></td>
</tr>
<tr class="odd">
<td><p>機能</p></td>
<td><p>は、上で定義された、サポートされている KSCAMERA_EXTENDEDPROP_OIS_ * フラグのビットごとの OR である必要があります。</p></td>
</tr>
<tr class="even">
<td><p>フラグ</p></td>
<td><p>これは、読み取り/書き込みフィールドです。 これには、上記で定義されている KSCAMERA_EXTENDEDPROP_OIS_ * フラグのいずれかを指定できます。</p></td>
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
