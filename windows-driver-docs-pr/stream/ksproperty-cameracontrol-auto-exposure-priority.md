---
title: KSK プロパティ\_CAMERACONTROL\_自動\_露出\_優先度
description: KSK プロパティ\_CAMERACONTROL\_AUTO\_露光\_PRIORITY プロパティは、デバイスがフレームレートを動的に変化させることができるかどうかを指定します。
ms.assetid: 0e20a4ee-b672-4c9a-9003-c2defd378e7c
keywords:
- KSPROPERTY_CAMERACONTROL_AUTO_EXPOSURE_PRIORITY ストリーミングメディアデバイス
topic_type:
- apiref
api_name:
- KSPROPERTY_CAMERACONTROL_AUTO_EXPOSURE_PRIORITY
api_location:
- Ksmedia.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3e40dc4c4f7b5affe9ca8af05d134d5573720614
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72843251"
---
# <a name="ksproperty_cameracontrol_auto_exposure_priority"></a>KSK プロパティ\_CAMERACONTROL\_自動\_露出\_優先度


KSK プロパティ\_CAMERACONTROL\_AUTO\_露光\_PRIORITY プロパティは、デバイスがフレームレートを動的に変化させることができるかどうかを指定します。

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
<td><p>[はい]</p></td>
<td><p>フィルターまたはノード</p></td>
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksproperty_cameracontrol_s" data-raw-source="[&lt;strong&gt;KSPROPERTY_CAMERACONTROL_S&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksproperty_cameracontrol_s)"><strong>KSPROPERTY_CAMERACONTROL_S</strong></a>、 <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksproperty_cameracontrol_node_s" data-raw-source="[&lt;strong&gt;KSPROPERTY_CAMERACONTROL_NODE_S&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksproperty_cameracontrol_node_s)"> <strong>KSPROPERTY_CAMERACONTROL_NODE_S</strong></a></p></td>
<td><p>ULONG</p></td>
</tr>
</tbody>
</table>

 

プロパティ値 (操作データ) は、フレームレートがデバイスによって動的に変化するかどうかを指定する ULONG です。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>Value</th>
<th>説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>0</p></td>
<td><p>フレームレートは一定である必要があります。</p></td>
</tr>
<tr class="even">
<td><p>1</p></td>
<td><p>フレームレートは、デバイスによって動的に変化することがあります。</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>注釈
-------

自動露出の優先順位は、カメラが照明条件に応じてフレームレートを動的に変化させることができるかどうかを決定します。

自動露出を使用しない場合、たとえば、フレームレートが 30 fps の場合、露出時間は33ミリ秒を超えることはできません。

ただし、自動露出優先度を使用すると、カメラはフレームレートを下げることによって低照明を補正できます。 たとえば、カメラはフレームレートを 25 fps に減らすことができるため、公開時間が40ミリ秒に短縮されます。

KSK プロパティ\_CAMERACONTROL\_自動\_露出\_優先順位は、USB ビデオクラスのプロパティページの**低光の補正**チェックボックスにマップされます。

KSK プロパティ\_CAMERACONTROL\_自動\_露出\_優先度を使用するには、 [**Ksk プロパティ\_CAMERACONTROL\_露出**](ksproperty-cameracontrol-exposure.md)を auto に設定する必要があります。つまり、自動露出優先度モードが有効なオプションになるように、カメラが自動露出モードになっている必要があります。

KSK プロパティ\_CAMERACONTROL\_自動\_露出\_優先度の既定値は0です。

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
<td><p>Windows Vista 以降のバージョンの Windows オペレーティングシステムで使用できます。</p></td>
</tr>
<tr class="even">
<td><p>Header</p></td>
<td>Ksmedia .h (Ksk を含む)</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>関連項目


[**KSK プロパティ\_CAMERACONTROL\_S**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksproperty_cameracontrol_s)

[**KSPROPERTY\_CAMERACONTROL\_NODE\_S**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksproperty_cameracontrol_node_s)

 

 






