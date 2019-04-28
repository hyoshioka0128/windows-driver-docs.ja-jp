---
title: KSPROPERTY\_ストリーム\_PRESENTATIONTIME
description: KSPROPERTY\_ストリーム\_PRESENTATIONTIME プロパティの使用を取得し、フィルターの暗証番号 (pin) の現在のプレゼンテーション時間を設定します。
ms.assetid: fb7bcd04-e600-4bab-b7e7-2b99e2bc0a6c
keywords:
- KSPROPERTY_STREAM_PRESENTATIONTIME ストリーミング メディア デバイス
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
ms.openlocfilehash: 0bf4e8ff2598abc3b75d14ca98631314f40603b1
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63379959"
---
# <a name="kspropertystreampresentationtime"></a>KSPROPERTY\_ストリーム\_PRESENTATIONTIME


KSPROPERTY\_ストリーム\_PRESENTATIONTIME プロパティの使用を取得し、フィルターの暗証番号 (pin) の現在のプレゼンテーション時間を設定します。

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
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff567145" data-raw-source="[&lt;strong&gt;KSTIME&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff567145)"><strong>KSTIME</strong></a></p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>注釈
-------

KSPROPERTY\_ストリーム\_PRESENTATIONTIME は pin が位置情報を保持またはタイムスタンプ形式は、位相的に異なる時間に異なるインターフェイスを使用して実装される、省略可能なプロパティに関連する pin。 そのため、時間することはシークのプレゼンテーション時間が発生すると、スタンプが変換されます。

としてフィルターの暗証番号 (pin) のプレゼンテーション時間が指定されて、 [ **KSTIME** ](https://msdn.microsoft.com/library/windows/hardware/ff567145)構造を解釈が使用されるインターフェイスに依存します。 標準のストリーミング インターフェイスの時刻が指定されて 100 ナノ秒単位で (指定いない限り、分子と分母) が現在処理中または処理が求めているストリームのフィルターのプレゼンテーションの位置を表します。 表示フィルターの場合は、この位置は現在レンダリングされているデータを表します。 この配置の情報は、マスターのクロックのプレゼンテーション時間と同期されます。 プレゼンテーション時間は通常は 0 から始まるし、ファイル データに時間オフセットを表す場合があります。 インターフェイスを強制するブロック配置を指定するのには、分子と分母を使用できます。

このプロパティは、シーク要求の伝播時に、位置指定値を変換するときにも使用されます。 1 つのピンでシーク位置指定値は、フィルターを位相的に関連するピンのプレゼンテーション時間内で変換されます。 クライアントは、シークするために、新しいストリームの位置では、このプロパティを設定します。 これは、通常が呼び出されます、プロキシで未処理の I/O をキャンセルし、デバイスの状態をリセットした後、シークが必要です。 リセットが実行されていない場合は、フィルターが自動的にキャンセルし、適切にリセットする必要があります。 プロパティには、接続で使用されるインターフェイスと同じ単位で、新しいストリームの位置を格納している KSTIME が渡されます。

クライアント (DirectShow プロキシなど) では、シーク要求が 1 つの接続に書き込む後から、プレゼンテーション時間に位相的に関連するその他の接続を照会します。 成功した読み取り要求を実行する他の接続は、その接続のもう一方の端に結果の位置を渡すプロキシをください。 この方法でシーク位置は、クライアントによって渡される最初の単体形式以外の単位の形式を知らなくても (たとえば、DirectShow グラフ) 全体で反映されます。 翻訳は、フィルター内でトポロジによる位置指定の情報が伝達される、フィルター内に発生します。 このまわりくどい方法は、通信方法は、グラフを使用するインターフェイスによって、さまざまなフィルター間に限定される可能性があるために使用されます。 シークの新しい位置を設定するときに、分子と分母のペアは、暗証番号 (pin) を満たすものである必要があります。

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


[**KSTIME**](https://msdn.microsoft.com/library/windows/hardware/ff567145)

[**KSPROPERTY**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/ns-ks-ksidentifier)

 

 






