---
title: KSPROPERTY\_拡張子\_単位\_情報
description: KSPROPERTY\_拡張子\_単位\_情報プロパティが拡張機能単位の記述子の guidExtensionCode、bNumControls、bNrInPins、および baSourceID メンバーを取得します。
ms.assetid: a7a2f655-8df7-4260-883f-53d6f5a7c6f3
keywords:
- KSPROPERTY_EXTENSION_UNIT_INFO ストリーミング メディア デバイス
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
ms.openlocfilehash: 1968ea5fcdc16292c287b65afb38461753af9f53
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67354857"
---
# <a name="kspropertyextensionunitinfo"></a>KSPROPERTY\_拡張子\_単位\_情報


KSPROPERTY\_拡張子\_単位\_情報プロパティが拡張機能単位の記述子の guidExtensionCode、bNumControls、bNrInPins、および baSourceID メンバーを取得します。

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
<th>取得</th>
<th>設定</th>
<th>対象</th>
<th>プロパティ記述子の型</th>
<th>プロパティ値の型</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>〇</p></td>
<td><p>X</p></td>
<td><p>フィルター ノード</p></td>
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/ns-ks-ksp_node" data-raw-source="[&lt;strong&gt;KSP_NODE&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/ns-ks-ksp_node)"><strong>KSP_NODE</strong></a></p></td>
<td><p>PVOID</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>注釈
-------

このプロパティは、Windows Vista で利用できる以降および Microsoft DirectX 9.2、以降のバージョンの SDK です。

システム提供の USB ビデオ クラス ドライバー、デバイスの起動中に (*Usbvideo.sys*) は、デバイスの拡張単位記述子から情報をキャッシュします。 *Usbvideo.sys*では情報 KSPROPERTY に応答をキャッシュし、\_拡張子\_単位\_情報。

そのため、このプロパティによって返されるフィールドは、拡張機能ユニット記述子のデバイスで提供されるものと同じです。 このような記述子の例は、次を参照してください。[サンプル拡張機能ユニット記述子](https://docs.microsoft.com/windows-hardware/drivers/stream/sample-extension-unit-descriptor)します。

具体的には、KSPROPERTY\_拡張機能\_単位\_GUID の次の表に示すように、記述子から、データ フィールドを続けて拡張単位が情報を返します。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>bNumControls</p></td>
<td><p>この拡張機能ユニット内のコントロールの数。</p></td>
</tr>
<tr class="even">
<td><p>bNrInPins</p></td>
<td><p>拡張機能単位で入力ピンの数。</p></td>
</tr>
<tr class="odd">
<td><p>baSourceID(n)</p></td>
<td><p>識別子の単位またはターミナルをピン留めする<em>n</em>この拡張機能のユニットが接続されています。 これは、ハードウェア id および DirectShow id ではありません。</p></td>
</tr>
</tbody>
</table>

 

次のコード例は、KSPROPERTY を送信する方法を示しています\_拡張子\_単位\_に示すように、完全なサンプルについては、[サンプル拡張ユニット プラグイン DLL](https://docs.microsoft.com/windows-hardware/drivers/stream/sample-extension-unit-plug-in-dll):。

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
<td><p>Windows Vista 以降のバージョンのオペレーティング システムでは、および Microsoft DirectX 9.2 の SDK またはそれ以降のバージョンで利用できます。</p></td>
</tr>
<tr class="even">
<td><p>Header</p></td>
<td>Ksmedia.h (Ksmedia.h を含む)</td>
</tr>
</tbody>
</table>
