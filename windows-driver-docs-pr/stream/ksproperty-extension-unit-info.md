---
title: KSK プロパティ\_拡張機能\_ユニット\_情報
description: KSK プロパティ\_EXTENSION\_UNIT\_INFO プロパティは、拡張機能の単位記述子の guidExtensionCode、bNumControls、bNrInPins、および baSourceID の各メンバーを取得します。
ms.assetid: a7a2f655-8df7-4260-883f-53d6f5a7c6f3
keywords:
- KSPROPERTY_EXTENSION_UNIT_INFO ストリーミングメディアデバイス
topic_type:
- apiref
api_name:
- KSPROPERTY_EXTENSION_UNIT_INFO
api_location:
- Ksmedia.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0d417ced4a20bec54a3451a8fe0318d322bf6633
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72837953"
---
# <a name="ksproperty_extension_unit_info"></a>KSK プロパティ\_拡張機能\_ユニット\_情報


KSK プロパティ\_EXTENSION\_UNIT\_INFO プロパティは、拡張機能の単位記述子の guidExtensionCode、bNumControls、bNrInPins、および baSourceID の各メンバーを取得します。

## <span id="ddk_ksproperty_extension_unit_info_ks"></span><span id="DDK_KSPROPERTY_EXTENSION_UNIT_INFO_KS"></span>


### <a name="usage-summary-table"></a>使用状況の概要テーブル

<table>
<colgroup>
<col width="20%" />
<col width="20%" />
<col width="20%" />
<col width="20%" />
<col width="20%" />
</colgroup>
<thead>
<tr class="header">
<th>[購入]</th>
<th>設定</th>
<th>対象</th>
<th>プロパティ記述子の型</th>
<th>プロパティ値の型</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>[はい]</p></td>
<td><p>必須ではない</p></td>
<td><p>ノードのフィルター</p></td>
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-ksp_node" data-raw-source="[&lt;strong&gt;KSP_NODE&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-ksp_node)"><strong>KSP_NODE</strong></a></p></td>
<td><p>PVOID</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>注釈
-------

このプロパティは、Windows Vista 以降、および Microsoft DirectX 9.2 以降のバージョンの SDK で使用できます。

デバイスの起動時に、システムによって提供される USB ビデオクラスドライバー (*usbvideo .sys*) によって、デバイスの拡張機能の単位記述子から情報がキャッシュされます。 次に、 *Usbvideo*は、このキャッシュされた情報を使用して、ksk プロパティ\_拡張機能\_単位\_情報に応答します。

このため、このプロパティによって返されるフィールドは、拡張機能の単位記述子のデバイスによって提供されるフィールドと同じです。 このような記述子の例については、「[サンプルの拡張機能単位記述子](https://docs.microsoft.com/windows-hardware/drivers/stream/sample-extension-unit-descriptor)」を参照してください。

具体的には、KSK プロパティ\_EXTENSION\_UNIT\_INFO は、次の表に示すように、記述子のデータフィールドをその後に返します。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>bNumControls</p></td>
<td><p>この拡張単位内のコントロールの数。</p></td>
</tr>
<tr class="even">
<td><p>bNrInPins</p></td>
<td><p>拡張単位の入力ピンの数。</p></td>
</tr>
<tr class="odd">
<td><p>baSourceID (n)</p></td>
<td><p>この拡張ユニットのピン<em>n</em>が接続されているユニットまたはターミナルの識別子。 これは、DirectShow 識別子ではなく、ハードウェア識別子です。</p></td>
</tr>
</tbody>
</table>

 

次のコード例は、[サンプルの拡張機能単体プラグイン DLL](https://docs.microsoft.com/windows-hardware/drivers/stream/sample-extension-unit-plug-in-dll)に示されている完全なサンプルから取得した、ksk プロパティ\_EXTENSION\_UNIT\_INFO を送信する方法を示しています。

```cpp
ExtensionProp.Property.Set = PROPSETID_VIDCAP_EXTENSION_UNIT;
    ExtensionProp.Property.Id = KSPROPERTY_EXTENSION_UNIT_INFO;
    ExtensionProp.Property.Flags = KSPROPERTY_TYPE_GET | 
                                   KSPROPERTY_TYPE_TOPOLOGY;
    ExtensionProp.NodeId = m_dwNodeId;

    hr = m_pKsControl->KsProperty(
        (PKSPROPERTY) &ExtensionProp,
        sizeof(ExtensionProp),
        NULL,
        0,
        &ulBytesReturned);
```

<a name="requirements"></a>要件
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>バージョン</p></td>
<td><p>Windows Vista 以降のバージョンのオペレーティングシステムおよび SDK for Microsoft DirectX 9.2 以降のバージョンで使用できます。</p></td>
</tr>
<tr class="even">
<td><p>Header</p></td>
<td>Ksmedia .h (Ksk を含む)</td>
</tr>
</tbody>
</table>
