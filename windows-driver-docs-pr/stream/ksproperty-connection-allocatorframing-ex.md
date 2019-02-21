---
title: KSPROPERTY\_接続\_ALLOCATORFRAMING\_例
description: AVStream クライアントの使用、KSPROPERTY\_接続\_ALLOCATORFRAMING\_EX、pin のフレームの要件を決定するプロパティ。
ms.assetid: 7ff1462f-959b-413e-a888-bcf7d251edee
keywords:
- KSPROPERTY_CONNECTION_ALLOCATORFRAMING_EX ストリーミング メディア デバイス
topic_type:
- apiref
api_name:
- KSPROPERTY_CONNECTION_ALLOCATORFRAMING_EX
api_location:
- ks.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 373605c1fded851941d3049f1e487c2e690efd87
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56527278"
---
# <a name="kspropertyconnectionallocatorframingex"></a>KSPROPERTY\_接続\_ALLOCATORFRAMING\_例


AVStream クライアントの使用、KSPROPERTY\_接続\_ALLOCATORFRAMING\_EX、pin のフレームの要件を決定するプロパティ。

## <span id="ddk_ksproperty_connection_allocatorframing_ex_ks"></span><span id="DDK_KSPROPERTY_CONNECTION_ALLOCATORFRAMING_EX_KS"></span>


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
<td><p>Pin</p></td>
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/ns-ks-ksidentifier" data-raw-source="[&lt;strong&gt;KSPROPERTY&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/ns-ks-ksidentifier)"><strong>KSPROPERTY</strong></a></p></td>
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff560982" data-raw-source="[&lt;strong&gt;KSALLOCATOR_FRAMING_EX&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff560982)"><strong>KSALLOCATOR_FRAMING_EX</strong></a></p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>注釈
-------

このプロパティを返します、 [ **KSALLOCATOR\_フレーム\_EX**](https://msdn.microsoft.com/library/windows/hardware/ff560982)AVStream のピン留めのフレームの要件をについて説明します。

ストリーム クラスで実行されているミニドライバーを使用する必要があります[ **KSPROPERTY\_接続\_ALLOCATORFRAMING**](ksproperty-connection-allocatorframing.md)します。

参照してください[KS アロケーター](https://msdn.microsoft.com/library/windows/hardware/ff567257)します。 [AVStream アロケーター](https://msdn.microsoft.com/library/windows/hardware/ff554202)します。

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
<td>Ks.h (Ks.h を含む)</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>関連項目


[**KSALLOCATOR\_フレーム\_例**](https://msdn.microsoft.com/library/windows/hardware/ff560982)

 

 






