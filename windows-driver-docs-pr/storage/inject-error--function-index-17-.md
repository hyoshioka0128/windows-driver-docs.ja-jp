---
title: エラーの挿入 (関数インデックス 17)
description: この関数は、NVDIMM-N のモジュールのファームウェアでエラーを挿入します。 この関数では、ソフトウェアの検証を有効にします。
ms.assetid: 4D77DC95-25BC-4D28-83B7-7A62383803E6
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 25d749b13a6a4b3e34629532c942e0d391af03f8
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63327000"
---
# <a name="inject-error-function-index-17"></a>エラーの挿入 (関数インデックス 17)


この関数は、NVDIMM-N のモジュールのファームウェアでエラーを挿入します。 この関数では、ソフトウェアの検証を有効にします。 プラットフォームのみなど、特定のシナリオでのエラーの挿入を有効にすることもできます、ユーザーが BIOS 設定を構成した後。 ホストを呼び出すことが[クエリ エラーの挿入の状態 (関数インデックス 16)](query-error-injection-status--function-index-16-.md)学習するかどうか、エラーの挿入関数は、有効です。

&gt; \[!注\]    &gt;、星が付いたマークされているすべてのレジスタ (\*) バイト アドレス指定可能なエネルギー バックアップ インターフェイス仕様で定義されているレジスタします。

 

## <a name="span-idinputspanspan-idinputspanspan-idinputspaninput"></a><span id="Input"></span><span id="input"></span><span id="INPUT"></span>入力


### <a name="span-idargs3spanspan-idargs3spanspan-idargs3spanargs3"></a><span id="Args3"></span><span id="args3"></span><span id="ARGS3"></span>Args3

<table>
<colgroup>
<col width="25%" />
<col width="25%" />
<col width="25%" />
<col width="25%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">フィールド</th>
<th align="left">バイトの長さ</th>
<th align="left">バイト オフセット</th>
<th align="left">説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><strong>挿入操作の失敗</strong></td>
<td align="left">2</td>
<td align="left">0</td>
<td align="left"><p>どの操作または非揮発性メモリ エラーが挿入されるかを指定します。</p>
<p><em>バイト 0 – <em>INJECT_OPS_FAILURES</em> (2, 0x60 です)</p>
<p></em>1 – バイト場合<em>INJECT_BAD_BLOCKS</em>は 1 (7 バイトのビット 0)、これは<em>INJECT_BAD_BLOCK_CAP</em> (2, 0x67)。 それ以外の場合、0 である必要があります。</p></td>
</tr>
<tr class="even">
<td align="left"><strong>エネルギーのソースのエラーを挿入します</strong></td>
<td align="left">1</td>
<td align="left">2</td>
<td align="left"><p>どのエネルギー ソース (ES) エラーが挿入されるかを指定します。</p>
<p><em>バイト 0 – <em>INJECT_ES_FAILURES</em> (2, 0x64)</p></td>
</tr>
<tr class="odd">
<td align="left"><strong>ファームウェアの更新エラーを挿入します</strong></td>
<td align="left">1</td>
<td align="left">3</td>
<td align="left"><p>挿入されるファームウェア操作エラーを指定します。</p>
<p></em>バイト 0 – <em>INJECT_FW_FAILURES</em> (2, 0x65)</p></td>
</tr>
</tbody>
</table>

 

## <a name="span-idoutputspanspan-idoutputspanspan-idoutputspanoutput"></a><span id="Output"></span><span id="output"></span><span id="OUTPUT"></span>出力


<table>
<colgroup>
<col width="25%" />
<col width="25%" />
<col width="25%" />
<col width="25%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">フィールド</th>
<th align="left">バイトの長さ</th>
<th align="left">バイト オフセット</th>
<th align="left">説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><strong>ステータス</strong></td>
<td align="left">4</td>
<td align="left">0</td>
<td align="left"><p>この関数は、次の関数に固有のエラー コードを返すことができます。</p>
<p>1:エラーの挿入は無効です。</p>
<p>2:サポートされていないために、1 つまたは複数のエラーは挿入されませんでした。</p>
<p>移動して<a href="-dsm-interface-for-byte-addressable-energy-backed-function-class--function-interface-1-.md" data-raw-source="[_DSM Method Output](-dsm-interface-for-byte-addressable-energy-backed-function-class--function-interface-1-.md)">_DSM メソッドの出力</a>詳細についてはします。</p></td>
</tr>
</tbody>
</table>

 

&gt; \[!注\]    &gt;関数に固有のエラー コード 2 を返すときに、エラーが正常に挿入されたが挿入されたままです。 この関数が関数に固有のエラー コード 2 を返す場合は、呼び出す[挿入エラーの取得 (関数インデックス 18)](get-injected-errors--function-index-18-.md)を取得するエラーは挿入されませんでした。

 

## <a name="span-idremarksspanspan-idremarksspanspan-idremarksspanremarks"></a><span id="Remarks"></span><span id="remarks"></span><span id="REMARKS"></span>注釈


一部のエラーの挿入機能は、省略可能なデバイスでサポートされていない可能性があります。 省略可能なエラー インジェクションの一覧については、適切なバイト アドレス指定可能なエネルギー バックアップ インターフェイス JEDEC 仕様を参照してください。

プラットフォームでは、ホストがサポートされていないエラーを挿入しようとしたかどうかを検出する必要があります。 書き込み、エラーの挿入に登録し、同じ登録を読み取る & 目的のすべてのビットを設定するかどうかを確認します。 たとえば、プラットフォームは運用上のエラーを挿入するには、次を行います。

1.  バイト 0 の値を書き込み、**挿入操作の失敗**フィールドを*挿入\_OPS\_エラー*を登録します。

2.  読み取り、*挿入\_OPS\_エラー*を登録します。

3.  場合の新しい値*挿入\_OPS\_エラー*のバイト 0 と一致する、**挿入操作の失敗**フィールドに、成功を返します。 それ以外の場合、関数に固有のエラー コード 2 を返します。

## <a name="span-idrelatedtopicsspanrelated-topics"></a><span id="related_topics"></span>関連トピック


[クエリ エラーの挿入の状態 (関数インデックス 16)](query-error-injection-status--function-index-16-.md)

[挿入されたエラー (関数インデックス 18) の取得](get-injected-errors--function-index-18-.md)

[\_バイトのアドレス指定可能なエネルギーの DSM インターフェイス関数クラス (関数インターフェイス 1) のバックアップ](-dsm-interface-for-byte-addressable-energy-backed-function-class--function-interface-1-.md)

 

 






