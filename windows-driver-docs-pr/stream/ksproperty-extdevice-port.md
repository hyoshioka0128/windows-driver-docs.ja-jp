---
title: KSPROPERTY\_EXTDEVICE\_ポート
description: KSPROPERTY\_EXTDEVICE\_ポートのプロパティを外部デバイスのポートの種類を取得します。
ms.assetid: 7513c37f-0c93-4078-ba85-cbc98304880f
keywords:
- KSPROPERTY_EXTDEVICE_PORT ストリーミング メディア デバイス
topic_type:
- apiref
api_name:
- KSPROPERTY_EXTDEVICE_PORT
api_location:
- ksmedia.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 161dc349f23b6c96178ed44009c86be08cf6857a
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63373384"
---
# <a name="kspropertyextdeviceport"></a>KSPROPERTY\_EXTDEVICE\_ポート


KSPROPERTY\_EXTDEVICE\_ポートのプロパティを外部デバイスのポートの種類を取得します。

## <span id="ddk_ksproperty_extdevice_port_ks"></span><span id="DDK_KSPROPERTY_EXTDEVICE_PORT_KS"></span>


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
<td><p>デバイス</p></td>
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff565156" data-raw-source="[&lt;strong&gt;KSPROPERTY_EXTDEVICE_S&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff565156)"><strong>KSPROPERTY_EXTDEVICE_S</strong></a></p></td>
<td><p>ULONG</p></td>
</tr>
</tbody>
</table>

 

プロパティの値 (データの操作) は、外部のデバイスの接続ポートを指定する ULONG です。 たとえば 1394 または USB です。

<a name="remarks"></a>注釈
-------

**DevPort** 、KSPROPERTY のメンバー\_EXTDEVICE\_の構造を外部デバイスのポートの種類を指定します。 **DevPort**メンバーは、開発と同じに設定する可能性があります\_ポート\_1394、DEV\_ポート\_USB など。これらのトークンが定義されている、 *xprtdefs.h* Microsoft DirectX SDK 内のファイル。

<a name="requirements"></a>要件
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>Header</p></td>
<td>Ksmedia.h (Ksmedia.h を含む)</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>関連項目


[**KSPROPERTY**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/ns-ks-ksidentifier)

[**KSPROPERTY\_EXTDEVICE\_S**](https://msdn.microsoft.com/library/windows/hardware/ff565156)

 

 






