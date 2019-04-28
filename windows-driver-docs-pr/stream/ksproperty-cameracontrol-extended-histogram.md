---
title: KSPROPERTY\_CAMERACONTROL\_拡張\_ヒストグラム
description: KSPROPERTY\_CAMERACONTROL\_拡張\_ヒストグラムは、ドライバーによって生成されたヒストグラム メタデータを制御するために使用するプロパティ ID。 これは、暗証番号 (pin) レベルの制御のプレビューのピン留めだけです。
ms.assetid: 638AA1AA-F8E5-4FD7-9283-CF1F23266474
keywords:
- KSPROPERTY_CAMERACONTROL_EXTENDED_HISTOGRAM ストリーミング メディア デバイス
topic_type:
- apiref
api_name:
- KSPROPERTY_CAMERACONTROL_EXTENDED_HISTOGRAM
api_location:
- Ksmedia.h
api_type:
- HeaderDef
ms.date: 09/10/2018
ms.localizationpriority: medium
ms.openlocfilehash: b8d49557c2d767d44bb3e58bc75091be2e2f7719
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63364096"
---
# <a name="kspropertycameracontrolextendedhistogram"></a>KSPROPERTY\_CAMERACONTROL\_拡張\_ヒストグラム


**KSPROPERTY\_CAMERACONTROL\_拡張\_ヒストグラム**はドライバーによって生成されたヒストグラム メタデータを制御するために使用するプロパティ ID です。 これは、暗証番号 (pin) レベルの制御のプレビューのピン留めだけです。

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
<td><p>Pin</p></td>
<td><p>同期</p></td>
</tr>
</tbody>
</table>

 

次のフラグを配置することができます、 **KSCAMERA\_EXTENDEDPROP\_ヘッダー。フラグ**ドライバーのヒストグラムのメタデータを制御するフィールド。 既定値は**ヒストグラム\_OFF**します。

```cpp
#define KSCAMERA_EXTENDEDPROP_HISTOGRAM_OFF      0x0000000000000000
#define KSCAMERA_EXTENDEDPROP_HISTOGRAM_ON       0x0000000000000001
```

このコントロールは、前に使用する必要があります、 [ **KSPROPERTY\_CAMERACONTROL\_拡張\_メタデータ**](ksproperty-cameracontrol-extended-metadata.md)コントロール、サイズ、適切なメタデータ バッファーことを確認するには割り当てられます。

場合設定**ヒストグラム\_OFF**ドライバーはプレビューの暗証番号 (pin) のヒストグラムのメタデータを配信できません。 ドライバーは、そのメタデータのバッファーのサイズ要件に、ヒストグラムのメタデータのサイズを含めないでください。

場合設定**ヒストグラム\_ON**ドライバーはプレビューの暗証番号 (pin) のヒストグラムのメタデータを提供するものとします。 ドライバーは、そのメタデータのバッファーのサイズ要件に、ヒストグラムのメタデータのサイズを含める必要があります。

ドライバーでは、ヒストグラムのメタデータを生成するために機能することはありません、ドライバーでは、このコントロールは実装しないでください。 サポートする必要がありますも、ドライバーは、このコントロールをサポートする場合[ **KSPROPERTY\_CAMERACONTROL\_拡張\_メタデータ**](ksproperty-cameracontrol-extended-metadata.md)コントロール。

**設定**このコントロールの呼び出しも何も起こりませんプレビューの暗証番号 (pin) が、状態、KSSTATE よりも高い\_停止状態です。 ドライバーは元に戻す、**設定**プレビューが停止状態ではない、返された場合に受信した呼び出し**状態\_無効な\_デバイス\_状態**。 **取得**呼び出し、ドライバーは現在の設定を返す必要があります**フラグ**フィールド。

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
<td><p>必要がありますが、暗証番号 (pin) の ID に関連付けられているプレビューの暗証番号 (pin)。</p></td>
</tr>
<tr class="odd">
<td><p>サイズ</p></td>
<td><p>Sizeof 必要があります (<strong>KSCAMERA_EXTENDEDPROP_HEADER</strong>) + sizeof (<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-tagkscamera_extendedprop_value" data-raw-source="[&lt;strong&gt;KSCAMERA_EXTENDEDPROP_VALUE&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-tagkscamera_extendedprop_value)"><strong>KSCAMERA_EXTENDEDPROP_VALUE</strong></a>)。</p></td>
</tr>
<tr class="even">
<td><p>結果</p></td>
<td><p>前回のエラーの結果を示す<strong>設定</strong>操作。 ない場合は<strong>設定</strong>操作が行われた、0 があります。</p></td>
</tr>
<tr class="odd">
<td><p>機能</p></td>
<td><p>0 を指定する必要があります。</p></td>
</tr>
<tr class="even">
<td><p>フラグ</p></td>
<td><p>これは、読み取り/書き込みフィールドです。 これのいずれを指定することができます、 <strong>KSCAMERA_EXTENDEDPROP_HISTOGRAM_ *</strong>上記で定義されたフラグ。</p></td>
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
