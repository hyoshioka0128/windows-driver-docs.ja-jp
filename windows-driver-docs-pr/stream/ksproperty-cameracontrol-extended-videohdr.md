---
title: KSPROPERTY\_CAMERACONTROL\_拡張\_VIDEOHDR
description: KSPROPERTY\_CAMERACONTROL\_拡張\_VIDEOHDR の使用を有効または、動的範囲の上限 (HDR) のビデオ ドライバーを無効にします。 これは、暗証番号 (pin) レベルの制御のビデオ ピン留めするだけです。
ms.assetid: AC798BF1-4E1A-48D8-8F56-986F89D9C153
keywords:
- KSPROPERTY_CAMERACONTROL_EXTENDED_VIDEOHDR ストリーミング メディア デバイス
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
ms.openlocfilehash: 0e8b124f0d13ce5e5ba68c3db7037b68db2c8d80
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56573087"
---
# <a name="kspropertycameracontrolextendedvideohdr"></a>KSPROPERTY\_CAMERACONTROL\_拡張\_VIDEOHDR

KSPROPERTY\_CAMERACONTROL\_拡張\_VIDEOHDR の使用を有効または、動的範囲の上限 (HDR) のビデオ ドライバーを無効にします。 これは、暗証番号 (pin) レベルの制御のビデオ ピン留めするだけです。

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

次のフラグは、KSCAMERA に配置できる\_EXTENDEDPROP\_ヘッダー。ビデオ HDR を制御するフラグ フィールドです。 既定では、ドライバーを VIDEOHDR に設定する必要があります\_OFF。

```cpp
#define KSCAMERA_EXTENDEDPROP_VIDEOHDR_OFF      0x0000000000000000
#define KSCAMERA_EXTENDEDPROP_VIDEOHDR_ON       0x0000000000000001 
#define KSCAMERA_EXTENDEDPROP_VIDEOHDR_AUTO     0x0000000000000002 
```

VIDEOHDR をサポートする必要があります、ドライバーは、このコントロールをサポートする場合\_ON/VIDEOHDR\_OFF。

ドライバーがビデオ HDR をサポートしていない場合、ドライバーはこのコントロールを実装しないでください。

このコントロールは、ドライバーにヒントとして機能します。 VIDEOHDR に設定すると\_ドライバーはベスト エフォートとしてビデオ HDR を実行する必要があります。

このコントロールの設定の呼び出しも何も起こりませんビデオ ピンが KSSTATE\_の実行の状態。 ドライバーはビデオの暗証番号 (pin) が実行中の状態とステータスを返しますが受信設定の呼び出し元に戻す\_無効な\_デバイス\_状態。 GET 呼び出しでは、ドライバーは、フラグ フィールドの現在の設定を返す必要があります。

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
<td><p>KSCAMERA_EXTENDEDPROP_VIDEOHDR_OFF</p></td>
<td><p>これは、必須の機能です。 指定した場合、HDR がドライバーとドライバーで無効になっているビデオのビデオ ストリームにビデオ HDR は実行されません。</p></td>
</tr>
<tr class="even">
<td><p>KSCAMERA_EXTENDEDPROP_VIDEOHDR_ON</p></td>
<td><p>これは、必須の機能です。 指定した場合、HDR になって、ドライバーとドライバー、ビデオはベスト エフォートとしてビデオ HDR を実施するものとします。 このフラグは VIDEOHDR_AUTO と VIDEOHDR_OFF フラグで相互に排他的です。</p></td>
</tr>
<tr class="odd">
<td><p>KSCAMERA_EXTENDEDPROP_VIDEOHDR_AUTO</p></td>
<td><p>この機能は省略可能です。 指定した場合、このような機能をサポートするドライバーはビデオ HDR をシーン分析に基づいて実行するかどうかを決定します。 このフラグは VIDEOHDR_ON と VIDEOHDR_OFF フラグで相互に排他的です。</p></td>
</tr>
</tbody>
</table>

次の表には、説明と要件が含まれています、 [KSCAMERA\_EXTENDEDPROP\_ヘッダー](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-tagkscamera_extendedprop_header)コントロールを使用する場合は、フィールドを構造体します。

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
<td><p>必要がある、暗証番号 (pin) の ID に関連付けられているビデオ ピン留めします。</p></td>
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
<td><p>ビットごとの OR、サポートされている KSCAMERA_EXTENDEDPROP_VIDEOHDR_ * フラグの上に定義されている必要があります。</p></td>
</tr>
<tr class="even">
<td><p>フラグ</p></td>
<td><p>これは、読み取り/書き込みフィールドです。 上記で定義された KSCAMERA_EXTENDEDPROP_VIDEOHDR_ * フラグのいずれかにできます。</p></td>
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
