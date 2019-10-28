---
title: KSK プロパティ\_CAMERACONTROL\_EXTENDED\_の詳細写真
description: KSK プロパティ\_CAMERACONTROL\_拡張\_詳細写真を使用して、ドライバーの写真 HDR、flash no flash、および ultra low light fusion を制御します。 これは、フォト pin の pin レベルコントロールです。
ms.assetid: 88C14C9E-8675-42BF-A606-64232ABD4FD1
keywords:
- KSPROPERTY_CAMERACONTROL_EXTENDED_ADVANCEDPHOTO ストリーミングメディアデバイス
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
ms.openlocfilehash: 5c33639634aa3be42a932e01fd0b7911e2bc0944
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72843246"
---
# <a name="ksproperty_cameracontrol_extended_advancedphoto"></a>KSK プロパティ\_CAMERACONTROL\_EXTENDED\_の詳細写真


KSK プロパティ\_CAMERACONTROL\_拡張\_詳細写真を使用して、ドライバーの写真 HDR、flash no flash、および ultra low light fusion を制御します。 これは、フォト pin の pin レベルコントロールです。

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

 

次に示すのは、KSCAMERA\_EXTENDEDPROP\_ヘッダーに配置できるフラグです。[フラグ] フィールドを指定して、写真の HDR、flash no flash、および超低光 fusion を制御します。 既定値は、KSCAMERA\_EXTENDEDPROP\_アドバンスフォト\_オフにする必要があります。

```cpp
#define KSCAMERA_EXTENDEDPROP_ADVANCEDPHOTO_OFF             0x0000000000000000
#define KSCAMERA_EXTENDEDPROP_ADVANCEDPHOTO_AUTO            0x0000000000000001
#define KSCAMERA_EXTENDEDPROP_ADVANCEDPHOTO_HDR             0x0000000000000002
#define KSCAMERA_EXTENDEDPROP_ADVANCEDPHOTO_FNF             0x0000000000000004
#define KSCAMERA_EXTENDEDPROP_ADVANCEDPHOTO_ULTRALOWLIGHT   0x0000000000000008
```

ドライバーがこのコントロールをサポートしている場合は、KSCAMERA\_EXTENDEDPROP\_アドバンスフォト\_オフをサポートする必要があります。

ドライバーが高度な写真キャプチャをサポートしていない場合、ドライバーはこのコントロールを実装しないでください。

フォト pin が KSK 状態\_実行状態である場合、このコントロールの SET 呼び出しは効果がありません。 このドライバーは、フォト pin が実行中の状態である場合に受信した設定呼び出しを拒否し、デバイス\_状態\_無効\_状態を返します。 GET 呼び出しでは、ドライバーは Flags フィールドの現在の設定を返します。

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
<td><p>KSCAMERA_EXTENDEDPROP_ADVANCEDPHOTO_OFF</p></td>
<td><p>これは必須の機能です。 指定した場合、ドライバーで高度な写真を実行する必要はありません。</p></td>
</tr>
<tr class="even">
<td><p>KSCAMERA_EXTENDEDPROP_ADVANCEDPHOTO_AUTO</p></td>
<td><p>この機能は省略可能です。 単独で指定した場合、このような機能をサポートするドライバーは、写真の HDR、Flash no Flash、または超低光 fusion をシーン分析に基づいて実行する必要があるかどうかを判断します。 このフラグは、OFF フラグと同時に指定することはできません。また、他のフラグと共に使用することもできます。</p></td>
</tr>
<tr class="odd">
<td><p>KSCAMERA_EXTENDEDPROP_ADVANCEDPHOTO_HDR</p></td>
<td><p>この機能は省略可能です。 このような機能をサポートするドライバーは、単独で指定した場合、写真の HDR を実行します。 このフラグは、AUTO 以外の他のフラグと同時には指定できません。 AUTO と共に指定した場合、ドライバーは、シーン分析に基づいてフォト HDR を実行するかどうかを決定します。</p></td>
</tr>
<tr class="even">
<td><p>KSCAMERA_EXTENDEDPROP_ADVANCEDPHOTO_FNF</p></td>
<td><p>この機能は省略可能です。 単独で指定すると、そのような機能をサポートするドライバーは flash no flash を実行します。 このフラグは、AUTO 以外の他のフラグと同時には指定できません。 AUTO と共に指定した場合、ドライバーは、シーン分析に基づいて flash no flash を実行するかどうかを決定します。</p></td>
</tr>
<tr class="odd">
<td><p>KSCAMERA_EXTENDEDPROP_ADVANCEDPHOTO_ULTRALOWLIGHT</p></td>
<td><p>この機能は省略可能です。 単独で指定した場合、このような機能をサポートするドライバーは、非常に低い軽 fusion を実行します。 このフラグは、AUTO 以外の他のフラグと同時には指定できません。 AUTO と共に指定すると、ドライバーは、シーン分析に基づいて超低光 fusion を実行するかどうかを決定します。</p></td>
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
<td><p>は、フォト pin に関連付けられている Pin ID である必要があります。</p></td>
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
<td><p>は、上で定義された、サポートされている KSCAMERA_EXTENDEDPROP_ADVANCEDPHOTO_ * フラグのビットごとの OR である必要があります。</p></td>
</tr>
<tr class="even">
<td><p>フラグ</p></td>
<td><p>これは、読み取り/書き込みフィールドです。 これには、上記で定義されている KSCAMERA_EXTENDEDPROP_ADVANCEDPHOTO_ * フラグのいずれかを指定できます。</p></td>
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
