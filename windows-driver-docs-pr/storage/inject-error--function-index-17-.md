---
title: エラーの挿入 (関数インデックス 17)
description: この関数は、NVDIMM モジュールファームウェアにエラーを挿入します。 この関数の目的は、ソフトウェアの検証を有効にすることです。
ms.assetid: 4D77DC95-25BC-4D28-83B7-7A62383803E6
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 2df2d4c9572c55cce1ad7b1683c8e96da17d72dd
ms.sourcegitcommit: 2f37e8de9759164804a3b1c7f5c9e497a607539b
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/26/2020
ms.locfileid: "83851281"
---
# <a name="inject-error-function-index-17"></a>エラーの挿入 (関数インデックス 17)


この関数は、NVDIMM モジュールファームウェアにエラーを挿入します。 この関数の目的は、ソフトウェアの検証を有効にすることです。 このプラットフォームでは、ユーザーが BIOS 設定を構成した後など、特定のシナリオでのエラーの挿入のみを有効にすることができます。 ホストは、エラー挿入関数が有効になっているかどうかを調べるために、[クエリエラーの挿入ステータス (関数インデックス 16)](query-error-injection-status--function-index-16-.md)を呼び出すことができます。

> [!NOTE]
> スター () でマークされたすべてのレジスタ \* は、バイトアドレッシング可能なエネルギーバッキングインターフェイスの仕様で定義されているレジスタです。

 

## <a name="span-idinputspanspan-idinputspanspan-idinputspaninput"></a><span id="Input"></span><span id="input"></span><span id="INPUT"></span>代入


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
<th align="left">バイト長</th>
<th align="left">バイト オフセット</th>
<th align="left">説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><strong>挿入操作の失敗</strong></td>
<td align="left">2</td>
<td align="left">0</td>
<td align="left"><p>挿入する操作または非揮発性メモリエラーを指定します。</p>
<p><em>バイト0– <em>INJECT_OPS_FAILURES</em> (2, 0x60)</p>
<p></em>バイト1– <em>INJECT_BAD_BLOCKS</em>が 1 (バイト0のビット 7) の場合、これは<em>INJECT_BAD_BLOCK_CAP</em> (2、0x67) になります。 それ以外の場合は0になります。</p></td>
</tr>
<tr class="even">
<td align="left"><strong>エネルギーソースエラーの挿入</strong></td>
<td align="left">1</td>
<td align="left">2</td>
<td align="left"><p>どのエネルギーソースエラーが挿入されるかを指定します。</p>
<p><em>バイト0– <em>INJECT_ES_FAILURES</em> (2、0x64)</p></td>
</tr>
<tr class="odd">
<td align="left"><strong>ファームウェア更新エラーの挿入</strong></td>
<td align="left">1</td>
<td align="left">3</td>
<td align="left"><p>どのファームウェア操作エラーが挿入されるかを指定します。</p>
<p></em>バイト0– <em>INJECT_FW_FAILURES</em> (2、0x65)</p></td>
</tr>
</tbody>
</table>

 

## <a name="span-idoutputspanspan-idoutputspanspan-idoutputspanoutput"></a><span id="Output"></span><span id="output"></span><span id="OUTPUT"></span>Output


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
<th align="left">バイト長</th>
<th align="left">バイト オフセット</th>
<th align="left">説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><strong>状態</strong></td>
<td align="left">4</td>
<td align="left">0</td>
<td align="left"><p>この関数は、次の関数固有のエラーコードを返すことができます。</p>
<p>1: エラー挿入が無効になっています。</p>
<p>2: サポートされていないため、1つまたは複数のエラーを挿入できませんでした。</p>
<p>詳細については、 <a href="-dsm-interface-for-byte-addressable-energy-backed-function-class--function-interface-1-.md" data-raw-source="[_DSM Method Output](-dsm-interface-for-byte-addressable-energy-backed-function-class--function-interface-1-.md)">_DSM メソッドの出力</a>に関するページを参照してください。</p></td>
</tr>
</tbody>
</table>

 

> [!NOTE]
> 正常に挿入されたエラーは、関数固有のエラーコード2を返すと、挿入されたままになります。 この関数から関数固有のエラーコード2が返された場合は、[挿入されたエラーを取得します[(関数インデックス 18)](get-injected-errors--function-index-18-.md) ] を呼び出して、挿入できなかったエラーを取得します。

 

## <a name="span-idremarksspanspan-idremarksspanspan-idremarksspanremarks"></a><span id="Remarks"></span><span id="remarks"></span><span id="REMARKS"></span>注釈


一部のエラー挿入機能はオプションであり、デバイスでサポートされていない可能性があります。 オプションのエラー挿入の一覧については、適切なバイトアドレッシング可能なエネルギーサポートインターフェイス JEDEC 仕様を参照してください。

プラットフォームは、ホストがサポートされていないエラーを挿入しようとしたかどうかを検出する必要があります。 これを行うには、エラー挿入レジスタに書き込み、その後、同じレジスタ & 読み取って、目的のすべてのビットが設定されているかどうかを確認します。 たとえば、プラットフォームは次の処理を実行して操作エラーを挿入します。

1.  "**操作エラーの挿入**" フィールドのバイト0の値を* \_ OPS \_ failure の挿入*登録に書き込みます。

2.  * \_ OPS \_ エラーの挿入*登録を読み取ります。

3.  * \_ OPS \_ エラーの挿入*の新しい値が、[**操作エラーの挿入**] フィールドのバイト0と一致する場合は、success が返されます。 それ以外の場合は、関数固有のエラーコード2を返します。

## <a name="span-idrelated_topicsspanrelated-topics"></a><span id="related_topics"></span>関連トピック


[エラー挿入状態のクエリ (関数インデックス 16)](query-error-injection-status--function-index-16-.md)

[挿入されたエラーの取得 (関数インデックス 18)](get-injected-errors--function-index-18-.md)

[\_バイトアドレッシング可能なエネルギー対応関数クラスの DSM インターフェイス (関数インターフェイス 1)](-dsm-interface-for-byte-addressable-energy-backed-function-class--function-interface-1-.md)

 

 






