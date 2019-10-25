---
title: KSK プロパティ\_ストリーム\_のプレゼンテーション時間
description: KSK プロパティ\_STREAM\_presentation TIME プロパティは、フィルターの pin の現在のプレゼンテーション時間を取得して設定するために使用されます。
ms.assetid: fb7bcd04-e600-4bab-b7e7-2b99e2bc0a6c
keywords:
- KSPROPERTY_STREAM_PRESENTATIONTIME ストリーミングメディアデバイス
topic_type:
- apiref
api_name:
- KSPROPERTY_STREAM_PRESENTATIONTIME
api_location:
- ks.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 520c08105c6be153d4432cb116b7bfd5c3bdd1f7
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72837945"
---
# <a name="ksproperty_stream_presentationtime"></a>KSK プロパティ\_ストリーム\_のプレゼンテーション時間


KSK プロパティ\_STREAM\_presentation TIME プロパティは、フィルターの pin の現在のプレゼンテーション時間を取得して設定するために使用されます。

## <span id="ddk_ksproperty_stream_presentationtime_ks"></span><span id="DDK_KSPROPERTY_STREAM_PRESENTATIONTIME_KS"></span>


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
<td><p>Pin</p></td>
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-ksidentifier" data-raw-source="[&lt;strong&gt;KSPROPERTY&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-ksidentifier)"><strong>KSPROPERTY</strong></a></p></td>
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-kstime" data-raw-source="[&lt;strong&gt;KSTIME&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-kstime)"><strong>KSTIME</strong></a></p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>注釈
-------

KSK プロパティ\_ストリーム\_プレゼンテーション時間は、pin が位置情報を保持する場合、または位相的関連の pin でタイムスタンプ形式が異なる別のインターフェイスを使用する場合に実装する必要がある省略可能なプロパティです。 そのため、シークプレゼンテーション時間に応じてタイムスタンプを変換する必要があります。

フィルターピンのプレゼンテーション時間は、使用されるインターフェイスによって解釈が異なる[**KSTIME**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-kstime)構造体として指定されます。 標準ストリーミングインターフェイスでは、時間は100ナノ秒単位で指定されます (分子と分母がそれ以外の値を指定している場合を除きます)。フィルターが現在処理している、または処理するためにシークしているストリームのプレゼンテーション位置を表します。 これがレンダリングフィルターである場合、この位置は現在表示されているデータを表します。 この配置情報は、マスタークロックのプレゼンテーション時間と同期されます。 通常、プレゼンテーション時間は0から始まり、ファイルデータへの時間オフセットを表すことができます。 分子と分母を使用すると、インターフェイスで適用されるブロックの配置を指定できます。

このプロパティは、シーク要求の伝達時に位置指定値を変換する場合にも使用されます。 1つのピンのシーク位置の値は、位相的関連のピンのプレゼンテーション時間にフィルターで変換されます。 クライアントは、シークするために、このプロパティに新しいストリームの位置を設定します。 これは通常、未処理の i/o をキャンセルし、デバイスの状態をリセットした後にシークが必要になったときにプロキシによって呼び出されます。 リセットが実行されていない場合は、フィルターが自動的にキャンセルされ、適切にリセットされることがあります。 プロパティには、接続で使用されるインターフェイスと一貫性のある単位での新しいストリームの位置を含む KSTIME が渡されます。

クライアント (たとえば、DirectShow プロキシ) が1つの接続にシーク要求を書き込むと、他の位相的関連接続に対してプレゼンテーション時間に対してクエリを実行します。 読み取り要求が正常に実行される他の接続では、プロキシがその接続のもう一方の端に結果の位置を渡します。 この方法では、クライアントによって渡された初期単位形式以外の単位形式を知らなくても、シーク位置が (たとえば、DirectShow グラフ全体で) 伝達されます。 フィルター内では、位置情報がフィルター内のトポロジを通じて伝達されるため、フィルター内で変換が行われます。 このまわりくどいメソッドは、使用するインターフェイスに応じて、グラフ内のさまざまなフィルター間で通信メソッドが制限される可能性があるため、使用されます。 新しいシーク位置を設定するときは、pin の分子と分母のペアを受け入れる必要があります。

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
<td>Ks (Ks を含む)</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>関連項目


[**KSTIME**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-kstime)

[**KSPROPERTY**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-ksidentifier)

 

 






