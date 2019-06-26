---
title: KSPROPERTY\_ストリーム\_MASTERCLOCK
description: KSPROPERTY\_ストリーム\_MASTERCLOCK プロパティが省略可能なプロパティ、暗証番号 (pin) を使用またはマスターのクロックの同期に使用する場合に実装する必要があります。
ms.assetid: b8fb4d7b-e2e3-498c-9f76-4075d3ae0cb2
keywords:
- KSPROPERTY_STREAM_MASTERCLOCK ストリーミング メディア デバイス
topic_type:
- apiref
api_name:
- KSPROPERTY_STREAM_MASTERCLOCK
api_location:
- ks.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: f208b5ac166110626a663f884f4a256f8df3a40c
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67376352"
---
# <a name="kspropertystreammasterclock"></a>KSPROPERTY\_ストリーム\_MASTERCLOCK


KSPROPERTY\_ストリーム\_MASTERCLOCK プロパティが省略可能なプロパティ、暗証番号 (pin) を使用またはマスターのクロックの同期に使用する場合に実装する必要があります。

## <span id="ddk_ksproperty_stream_masterclock_ks"></span><span id="DDK_KSPROPERTY_STREAM_MASTERCLOCK_KS"></span>


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
<td><p>〇</p></td>
<td><p>Pin</p></td>
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/ns-ks-ksidentifier" data-raw-source="[&lt;strong&gt;KSPROPERTY&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/ns-ks-ksidentifier)"><strong>KSPROPERTY</strong></a></p></td>
<td><p>ハンドル</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>注釈
-------

プロパティを返します、 **NULL**に対してクエリを実行するときに処理します。 サポートについては、呼び出しが正常に終了するかどうかによって決まります。

KSPROPERTY を使用する\_ストリーム\_MASTERCLOCK pin マスター クロックがサポートされているかどうかを照会するか、pin の現在のマスター時計を設定します。 通常これは、管理者として graph を通じてなど directshow です。 マスターのクロックのハンドルが取得されると別の pin にマスターの時計を設定するために使用するあるいはできますマスターのクロックのユーザー モードのプロキシとしてなど DirectShow グラフで。

Pin の時計を設定すると、暗証番号 (pin)、基になるファイル オブジェクトを参照してファイル オブジェクトに対してクエリを実行できる後で。 ハンドルのクエリを実行するクライアントによって自体ファイル ハンドルを閉じる必要があります。

フィルターは、他のストリームとを同期する必要なく、グラフの中程のマスターのクロックの生成やコンバーター フィルターなど、いずれかを参照する必要がありますに配置する場合に、プロパティをサポートする必要はありません。 プロパティが場合も使用できます読み取り専用フィルターは、マスターのクロックが生成されますが、外部のマスター クロックを同期しません。

参照してください[KS クロック](https://docs.microsoft.com/windows-hardware/drivers/stream/ks-clocks)と[AVStream クロック](https://docs.microsoft.com/windows-hardware/drivers/stream/avstream-clocks)します。

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


[**KSPROPERTY**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/ns-ks-ksidentifier)

 

 






