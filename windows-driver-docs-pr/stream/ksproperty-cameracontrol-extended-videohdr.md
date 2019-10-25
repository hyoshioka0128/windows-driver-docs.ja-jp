---
title: KSK プロパティ\_CAMERACONTROL\_EXTENDED\_VIDEOHDR
description: KSK プロパティ\_CAMERACONTROL\_EXTENDED\_VIDEOHDR は、ドライバーの高ダイナミックレンジ (HDR) ビデオを有効または無効にするために使用されます。 これは、ビデオ pin の pin レベルコントロールです。
ms.assetid: AC798BF1-4E1A-48D8-8F56-986F89D9C153
keywords:
- KSPROPERTY_CAMERACONTROL_EXTENDED_VIDEOHDR ストリーミングメディアデバイス
topic_type:
- apiref
api_name:
- KSPROPERTY_CAMERACONTROL_EXTENDED_VIDEOHDR
api_location:
- Ksmedia.h
api_type:
- HeaderDef
ms.date: 09/11/2018
ms.localizationpriority: medium
ms.openlocfilehash: 050e2dcc7cf7315ceae4cabb6da3ae17cc910a36
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72826201"
---
# <a name="ksproperty_cameracontrol_extended_videohdr"></a>KSK プロパティ\_CAMERACONTROL\_EXTENDED\_VIDEOHDR

KSK プロパティ\_CAMERACONTROL\_EXTENDED\_VIDEOHDR は、ドライバーの高ダイナミックレンジ (HDR) ビデオを有効または無効にするために使用されます。 これは、ビデオ pin の pin レベルコントロールです。

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
<td><p>Pin</p></td>
<td><p>同期</p></td>
</tr>
</tbody>
</table>

次のフラグは、KSCAMERA\_EXTENDEDPROP\_ヘッダーに配置できます。ビデオの HDR を制御するフラグフィールド。 既定では、ドライバーは VIDEOHDR\_OFF に設定する必要があります。

```cpp
#define KSCAMERA_EXTENDEDPROP_VIDEOHDR_OFF      0x0000000000000000
#define KSCAMERA_EXTENDEDPROP_VIDEOHDR_ON       0x0000000000000001 
#define KSCAMERA_EXTENDEDPROP_VIDEOHDR_AUTO     0x0000000000000002 
```

ドライバーがこのコントロールをサポートしている場合は、VIDEOHDR\_ON/VIDEOHDR\_OFF をサポートする必要があります。

ドライバーでビデオの HDR がサポートされていない場合、ドライバーはこのコントロールを実装しないでください。

このコントロールは、ドライバーのヒントとして機能します。 VIDEOHDR\_に設定すると、ドライバーはビデオ HDR をベストエフォートとして実行する必要があります。

ビデオ pin が KSK 状態\_実行状態の場合、このコントロールの SET 呼び出しは効果がありません。 ビデオの pin が実行中の状態である場合、ドライバーは受信したセットの呼び出しを拒否し、デバイス\_状態\_無効\_状態を返します。 GET 呼び出しでは、ドライバーは Flags フィールドの現在の設定を返します。

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
<td><p>KSCAMERA_EXTENDEDPROP_VIDEOHDR_OFF</p></td>
<td><p>これは必須の機能です。 指定した場合、ドライバーでビデオの HDR が無効になり、ドライバーはビデオストリームでビデオの HDR を実行しません。</p></td>
</tr>
<tr class="even">
<td><p>KSCAMERA_EXTENDEDPROP_VIDEOHDR_ON</p></td>
<td><p>これは必須の機能です。 指定した場合、ドライバーでビデオの HDR が有効になり、ドライバーはビデオの HDR をベストエフォートとして実行します。 このフラグは、VIDEOHDR_AUTO および VIDEOHDR_OFF フラグと同時に指定することはできません。</p></td>
</tr>
<tr class="odd">
<td><p>KSCAMERA_EXTENDEDPROP_VIDEOHDR_AUTO</p></td>
<td><p>この機能は省略可能です。 指定した場合、このような機能をサポートするドライバーは、シーン分析に基づいてビデオの HDR を実行するかどうかを決定します。 このフラグは、VIDEOHDR_ON および VIDEOHDR_OFF フラグと同時に指定することはできません。</p></td>
</tr>
</tbody>
</table>

次の表には、コントロールを使用する場合の[KSCAMERA\_EXTENDEDPROP\_ヘッダー](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-tagkscamera_extendedprop_header)構造のフィールドの説明と要件が含まれています。

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
<td><p>は、ビデオ pin に関連付けられている Pin ID である必要があります。</p></td>
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
<td><p>は、上で定義された、サポートされている KSCAMERA_EXTENDEDPROP_VIDEOHDR_ * フラグのビットごとの OR である必要があります。</p></td>
</tr>
<tr class="even">
<td><p>フラグ</p></td>
<td><p>これは、読み取り/書き込みフィールドです。 これには、上記で定義されている KSCAMERA_EXTENDEDPROP_VIDEOHDR_ * フラグのいずれかを指定できます。</p></td>
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
