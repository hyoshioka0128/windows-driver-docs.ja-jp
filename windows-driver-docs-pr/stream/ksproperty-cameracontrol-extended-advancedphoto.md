---
title: KSPROPERTY\_CAMERACONTROL\_拡張\_ADVANCEDPHOTO
description: KSPROPERTY\_CAMERACONTROL\_拡張\_ADVANCEDPHOTO は、フォト HDR の制御、ドライバーで flash、および超低ライト fusion flash なしに使用されます。 これは、暗証番号 (pin) レベルの制御の写真のピン留めだけです。
ms.assetid: 88C14C9E-8675-42BF-A606-64232ABD4FD1
keywords:
- KSPROPERTY_CAMERACONTROL_EXTENDED_ADVANCEDPHOTO ストリーミング メディア デバイス
topic_type:
- apiref
api_name:
- KSPROPERTY_CAMERACONTROL_EXTENDED_ADVANCEDPHOTO
api_location:
- Ksmedia.h
api_type:
- HeaderDef
ms.date: 09/10/2018
ms.localizationpriority: medium
ms.openlocfilehash: 840fa4452e61c1725555dcbfdcc1725204c93c3b
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56580871"
---
# <a name="kspropertycameracontrolextendedadvancedphoto"></a>KSPROPERTY\_CAMERACONTROL\_拡張\_ADVANCEDPHOTO


KSPROPERTY\_CAMERACONTROL\_拡張\_ADVANCEDPHOTO は、フォト HDR の制御、ドライバーで flash、および超低ライト fusion flash なしに使用されます。 これは、暗証番号 (pin) レベルの制御の写真のピン留めだけです。

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
<td><p>Pin</p></td>
<td><p>同期</p></td>
</tr>
</tbody>
</table>

 

次に、KSCAMERA に配置できるフラグ\_EXTENDEDPROP\_ヘッダー。コントロールの写真、HDR に flags フィールドには、flash、および超低ライト fusion flash ありません。 既定値は KSCAMERA をする必要があります\_EXTENDEDPROP\_ADVANCEDPHOTO\_OFF。

```cpp
#define KSCAMERA_EXTENDEDPROP_ADVANCEDPHOTO_OFF             0x0000000000000000
#define KSCAMERA_EXTENDEDPROP_ADVANCEDPHOTO_AUTO            0x0000000000000001
#define KSCAMERA_EXTENDEDPROP_ADVANCEDPHOTO_HDR             0x0000000000000002
#define KSCAMERA_EXTENDEDPROP_ADVANCEDPHOTO_FNF             0x0000000000000004
#define KSCAMERA_EXTENDEDPROP_ADVANCEDPHOTO_ULTRALOWLIGHT   0x0000000000000008
```

KSCAMERA をサポートする必要があります、ドライバーは、このコントロールをサポートする場合\_EXTENDEDPROP\_ADVANCEDPHOTO\_OFF。

ドライバーがサポートされていない場合は、高度な写真のいずれかをキャプチャ、ドライバーは、このコントロールを実装しないでください。

このコントロールの設定の呼び出しも何も起こりません写真の暗証番号 (pin) が KSSTATE\_の実行の状態。 ドライバーは写真の暗証番号 (pin) が実行状態とステータスを返しますが受信設定の呼び出し元に戻す\_無効な\_デバイス\_状態。 ドライバーは、GET 呼び出しで、フラグ フィールドの現在の設定を返す必要があります。

次の表では、フラグの機能について説明します。

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
<td><p>KSCAMERA_EXTENDEDPROP_ADVANCEDPHOTO_OFF</p></td>
<td><p>これは、必須の機能です。 指定すると、ドライバーで高度な写真を実行する必要がありますはありません。</p></td>
</tr>
<tr class="even">
<td><p>KSCAMERA_EXTENDEDPROP_ADVANCEDPHOTO_AUTO</p></td>
<td><p>この機能は省略可能です。 単独で指定した場合、このような機能をサポートするドライバーは写真 HDR、Flash Flash や超低ライト fusion は実行されませんが、シーンの分析に基づくかどうかを決定します。 このフラグは OFF フラグで相互に排他的では、他のフラグで使用できます。</p></td>
</tr>
<tr class="odd">
<td><p>KSCAMERA_EXTENDEDPROP_ADVANCEDPHOTO_HDR</p></td>
<td><p>この機能は省略可能です。 単独で指定した場合、このような機能をサポートするドライバーは写真 HDR を実行します。 このフラグは、自動を除くその他のフラグで相互に排他的です。 自動と共に指定した場合、ドライバーは写真 HDR を実行する必要がありますが、シーンの分析に基づくかどうかを決定します。</p></td>
</tr>
<tr class="even">
<td><p>KSCAMERA_EXTENDEDPROP_ADVANCEDPHOTO_FNF</p></td>
<td><p>この機能は省略可能です。 このような機能の実行をサポートしていますが flash をフラッシュしないドライバーを単独で、指定した場合。 このフラグは、自動を除くその他のフラグで相互に排他的です。 自動と共に指定した場合、ドライバーはフラッシュのフラッシュを実行できませんが、シーンの分析に基づくかどうかを決定します。</p></td>
</tr>
<tr class="odd">
<td><p>KSCAMERA_EXTENDEDPROP_ADVANCEDPHOTO_ULTRALOWLIGHT</p></td>
<td><p>この機能は省略可能です。 単独で指定した場合、このような機能をサポートするドライバーは超低ライト fusion を実行します。 このフラグは、自動を除くその他のフラグで相互に排他的です。 自動と共に指定した場合、ドライバーは超低ライト fusion をシーン分析に基づいて実行するかどうかを決定します。</p></td>
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
<td><p>必要がありますが、暗証番号 (pin) の ID に関連付けられている写真の暗証番号 (pin)。</p></td>
</tr>
<tr class="odd">
<td><p>サイズ</p></td>
<td><p>これは、sizeof(KSCAMERA_EXTENDEDPROP_HEADER) + sizeof(KSCAMERA_EXTENDEDPROP_VALUE) である必要があります。</p></td>
</tr>
<tr class="even">
<td><p>結果</p></td>
<td><p>最後の設定操作のエラーの結果を示します。 設定操作が行われていない場合は必ず 0。</p></td>
</tr>
<tr class="odd">
<td><p>機能</p></td>
<td><p>ビットごとの OR、サポートされている KSCAMERA_EXTENDEDPROP_ADVANCEDPHOTO_ * フラグの上に定義されている必要があります。</p></td>
</tr>
<tr class="even">
<td><p>フラグ</p></td>
<td><p>これは、読み取り/書き込みフィールドです。 上記で定義された KSCAMERA_EXTENDEDPROP_ADVANCEDPHOTO_ * フラグのいずれかにできます。</p></td>
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
