---
title: KSPROPERTY\_CAMERACONTROL\_拡張\_FOCUSPRIORITY
description: KSPROPERTY\_CAMERACONTROL\_拡張\_FOCUSPRIORITY プロパティ ID は、KSPROPERTY で定義されている\_CAMERACONTROL\_拡張\_プロパティの列挙は、構成に使用されますフォーカスの優先順位。
ms.assetid: 7E3558A1-0D0D-4470-B9C9-61EA359E92C5
keywords:
- KSPROPERTY_CAMERACONTROL_EXTENDED_FOCUSPRIORITY ストリーミング メディア デバイス
topic_type:
- apiref
api_name:
- KSPROPERTY_CAMERACONTROL_EXTENDED_FOCUSPRIORITY
api_location:
- Ksmedia.h
api_type:
- HeaderDef
ms.date: 09/10/2018
ms.localizationpriority: medium
ms.openlocfilehash: 5f31403dd9d5d5c4bd0afd6e1400428508547ed8
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56529242"
---
# <a name="kspropertycameracontrolextendedfocuspriority"></a>KSPROPERTY\_CAMERACONTROL\_拡張\_FOCUSPRIORITY


**KSPROPERTY\_CAMERACONTROL\_拡張\_FOCUSPRIORITY**プロパティで定義されている ID、 [ **KSPROPERTY\_CAMERACONTROL\_拡張\_プロパティ**](https://msdn.microsoft.com/library/windows/hardware/dn917962)列挙体を使用して、フォーカスの優先順位を構成します。 フォーカスの優先度を設定すると、ときに重点を置いてよりも優先されます、画像を撮影した画像は常にフォーカスがあることを確認します。 それ以外の場合、画像をすぐに表示画像がフォーカスをされているかどうかに関係なくされます。 失敗したフォーカスとタイムアウトを指定しているかどうかの処理の動作は、ドライバーと oem は内部です。

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

 

フォーカスの優先順位を構成する、 **KSPROPERTY\_CAMERACONTROL\_拡張\_FOCUSPRIORITY**プロパティ ID を使用する必要があります。 フォーカスの優先度を設定すると、ときに重点を置いてよりも優先されます写真の撮影を撮影した画像は常にフォーカスがあることを確認します。 フォーカスの優先順位が設定されていない場合、画像が、画像がフォーカスされたかどうかに関係なく即座に表示されます。 失敗したフォーカスの処理の動作が失敗し、タイムアウトは、OEM によって決定され、ドライバーの内部します。

[ **KSCAMERA\_EXTENDEDPROP\_ヘッダー**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-tagkscamera_extendedprop_header)、値として、次のフラグが定義されます。 Get 呼び出しでは、カメラのドライバーは、現在フォーカスの優先順位の構成を使用してこれらのフラグのいずれかを返します。 設定の呼び出しでは、カメラのドライバーは、これらのフラグのいずれかを使用して新しいフォーカス優先順位の構成を設定します。

```cpp
#define KSCAMERA_EXTENDEDPROP_FOCUSPRIORITY_OFF     0x0000000000000000
#define KSCAMERA_EXTENDEDPROP_FOCUSPRIORITY_ON      0x0000000000000001
```

**注**  これは、同期のコントロールと、このコントロールに対して定義されている機能はありません。

 

次の表には、説明と要件が含まれています、 **KSCAMERA\_EXTENDEDPROP\_ヘッダー**フォーカスの優先順位の管理を使用する場合は、フィールドを構造体します。

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
<td><p>これは、1、</p></td>
</tr>
<tr class="even">
<td><p>PinId</p></td>
<td><p>KSCAMERA_EXTENDEDPROP_FILTERSCOPE (0 xffffffff) 必要があります。</p></td>
</tr>
<tr class="odd">
<td><p>サイズ</p></td>
<td><p>Sizeof 必要があります (<strong>KSCAMERA_EXTENDEDPROP_HEADER</strong>) + sizeof (<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-tagkscamera_extendedprop_value" data-raw-source="[&lt;strong&gt;KSCAMERA_EXTENDEDPROP_VALUE&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-tagkscamera_extendedprop_value)"><strong>KSCAMERA_EXTENDEDPROP_VALUE</strong></a>)、</p></td>
</tr>
<tr class="even">
<td><p>結果</p></td>
<td><p>これはエラーの結果を示します</p></td>
</tr>
<tr class="odd">
<td><p>機能</p></td>
<td><p>これは 0 を指定する必要があります。</p></td>
</tr>
<tr class="even">
<td><p>フラグ</p></td>
<td><p>これは、読み取り/書き込みフィールドです。 上記で定義された KSCAMERA_EXTENDEDPROP_FOCUSPRIORITY_Xxx フラグのいずれかにできます。</p></td>
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
