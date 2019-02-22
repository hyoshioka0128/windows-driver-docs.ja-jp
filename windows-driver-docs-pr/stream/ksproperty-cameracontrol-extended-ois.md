---
title: KSPROPERTY\_CAMERACONTROL\_拡張\_OIS
description: KSPROPERTY\_CAMERACONTROL\_拡張\_OIS はドライバーの光ディスク イメージの安定化 (OIS) を制御するために使用するプロパティ ID。
ms.assetid: CF4F1283-1517-4F93-8554-FBD4B068A655
keywords:
- KSPROPERTY_CAMERACONTROL_EXTENDED_OIS ストリーミング メディア デバイス
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
ms.openlocfilehash: fa074271d224a9309abe496dab95a2ab1fa68fd3
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56539354"
---
# <a name="kspropertycameracontrolextendedois"></a>KSPROPERTY\_CAMERACONTROL\_拡張\_OIS

**KSPROPERTY\_CAMERACONTROL\_拡張\_OIS**のドライバの光ディスク イメージの安定化 (OIS) を制御するために使用するプロパティ id。

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
<th>種類</th>
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

次のフラグを配置することができます、 **KSCAMERA\_EXTENDEDPROP\_ヘッダー。フラグ**コントロール光ディスク イメージの安定化するフィールド。 既定値は、それ以外の場合自動がサポートされている場合、自動または ON する必要があります。

```cpp
#define KSCAMERA_EXTENDEDPROP_OIS_OFF   0x0000000000000000
#define KSCAMERA_EXTENDEDPROP_OIS_ON    0x0000000000000001
#define KSCAMERA_EXTENDEDPROP_OIS_AUTO  0x0000000000000002 
```

OIS をサポートする必要があります、ドライバーは、このコントロールをサポートする場合\_ON および OIS\_OFF。

ドライバーが光学イメージの安定化をサポートしていない場合、ドライバーはこのコントロールを実装しないでください。

このコントロールの設定の呼び出しも何も起こりませんビデオや写真の pin が KSSTATE とき\_の実行の状態。 ドライバーはビデオや写真のいずれかの暗証番号 (pin) が実行状態とステータスを返しますが受信設定の呼び出し元に戻す\_無効な\_デバイス\_状態。 ドライバーは、GET 呼び出しで、フラグ フィールドの現在の設定を返す必要があります。

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
<td><p>KSCAMERA_EXTENDEDPROP_OIS_OFF</p></td>
<td><p>これは、必須の機能です。 指定した場合、ドライバーでは、光ディスク イメージの安定化は無効になっています。</p></td>
</tr>
<tr class="even">
<td><p>KSCAMERA_EXTENDEDPROP_OIS_ON</p></td>
<td><p>これは、必須の機能です。 指定した場合、ドライバーでは、光ディスク イメージの安定化は有効になっています。 このフラグは OIS_AUTO と OIS_OFF フラグで相互に排他的です。</p></td>
</tr>
<tr class="odd">
<td><p>KSCAMERA_EXTENDEDPROP_OIS_AUTO</p></td>
<td><p>この機能は省略可能です。 指定した場合、このような機能をサポートするドライバーは光ディスク イメージの安定化をオンまたはオフにするかどうかを決定します。 このフラグは OIS_ON と OIS_OFF フラグで相互に排他的です。</p></td>
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
<th>メンバー</th>
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
<td><p>これは、sizeof(KSCAMERA_EXTENDEDPROP_HEADER) + sizeof(KSCAMERA_EXTENDEDPROP_VALUE) である必要があります。</p></td>
</tr>
<tr class="even">
<td><p>結果</p></td>
<td><p>最後の設定操作のエラーの結果を示します。 設定操作が行われていない場合は必ず 0。</p></td>
</tr>
<tr class="odd">
<td><p>機能</p></td>
<td><p>ビットごとの OR、サポートされている KSCAMERA_EXTENDEDPROP_OIS_ * フラグの上に定義されている必要があります。</p></td>
</tr>
<tr class="even">
<td><p>フラグ</p></td>
<td><p>これは、読み取り/書き込みフィールドです。 上記で定義された KSCAMERA_EXTENDEDPROP_OIS_ * フラグのいずれかにできます。</p></td>
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
