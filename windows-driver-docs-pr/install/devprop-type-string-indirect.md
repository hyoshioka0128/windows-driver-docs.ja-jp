---
title: DEVPROP_TYPE_STRING_INDIRECT
description: DEVPROP_TYPE_STRING_INDIRECT 識別子は、間接的な文字列の参照を含む NULL で終わる Unicode 文字列の基本データ型識別子を表します。
ms.assetid: c3a4f627-02d7-47ba-aa62-5d6b0e8dd9cd
keywords:
- DEVPROP_TYPE_STRING_INDIRECT デバイスとドライバーのインストール
topic_type:
- apiref
api_name:
- DEVPROP_TYPE_STRING_INDIRECT
api_location:
- Devpropdef.h
api_type:
- HeaderDef
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 7ab34cc95fffd5793b7cb93e5ea1584a9827dccf
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63391704"
---
# <a name="devprop_type_string_indirect"></a>DEVPROP_TYPE_STRING_INDIRECT


DEVPROP_TYPE_STRING_INDIRECT 識別子は、間接的な文字列の参照を含む NULL で終わる Unicode 文字列の基本データ型識別子を表します。

<a name="remarks"></a>注釈
-------

間接的な文字列、参照では、実際の文字列を含む文字列リソースについて説明します。 間接的な文字列参照は、次の形式のいずれかで表示できます。

<a href="" id="--path--filename--resourceid"></a> **@** \[<em>path</em> **\\** \]<em>FileName</em>* *,-***ResourceID*  
Windows で指定されているモジュールから文字列を抽出し、*パス*と*FileName*エントリ、および文字列のリソース識別子は、によって提供される、 *ResourceID*エントリ (必要なマイナス記号を除く)。 文字列リソースは、呼び出し元の推奨される UI 言語のいずれかに最適なモジュール リソース セクションから読み込まれます。 *パス*エントリは省略可能です。 指定した場合、*パス*エントリ、モジュールは、システム定義の検索パス内にあるディレクトリに配置する必要があります。

<a href="" id="-infname--strkey-"></a> **@** <em>InfName</em> **,%** <em>strkey</em> **%**  
Windows では、文字列を抽出、INF から**文字列**、%systemroot% 内 INF ファイルのセクション\\*inf*ディレクトリの名前を持つがによって提供される、 *InfName*エントリ。 *Strkey*トークン識別子が内の行のキーと一致する必要があります、**文字列**呼び出し元のいずれかに最適なセクションの UI 言語を優先します。 言語に固有の場合**文字列**セクションが存在して、Windows が既定値を使用して**文字列**セクション。

データ型のプロパティの修飾子のいずれかで DEVPROP_TYPE_STRING_INDIRECT を組み合わせることはできません。

### <a name="setting-a-property-of-this-type"></a>この型のプロパティを設定

基本データ型は DEVPROP_TYPE_STRING_INDIRECT プロパティを設定する呼び出し、対応する **SetupDiSet * * * Xxx*プロパティ関数と set 関数は、次のようにパラメーターを入力します。

-   設定、 *PropertyType* DEVPROP_TYPE_STRING_INDIRECT パラメーター。

-   設定、 *PropertyBuffer*間接的な文字列の参照を提供する NULL で終わる文字列を格納しているバッファーへのポインターへのパラメーター。

-   設定、 *PropertyBufferSize*パラメーター文字列のバイト単位のサイズにします。

-   プロパティを設定する適切な関数の残りのパラメーターを設定します。

### <a name="retrieving-the-value-of-this-property-type"></a>この種類のプロパティの値を取得します。

アプリケーションを呼び出すと、**SetupDiGet * * * Xxx*この基本のデータのプロパティの値を取得するプロパティ関数の入力、プロパティを参照する実際の文字列を検索する Windows 試行します。 呼び出し元に実際の文字列を返し、として取得されたプロパティの基本データ型を識別する場合は、Windows では、実際の文字列を取得できます、 [ **DEVPROP_TYPE_STRING**](devprop-type-string.md)します。 それ以外の場合、Windows では、間接的な文字列参照を取得し、DEVPROP_TYPE_STRING_INDIRECT として取得されたプロパティの基本データ型を識別します。

### <a name="localizing-static-text"></a>静的テキストをローカライズします。

Windows Vista で始まる DEVPROP_TYPE_STRING_INDIRECT に静的なテキスト プロパティの型を設定して、PE イメージの文字列またはリソース テーブルからのリソースを使用して、カスタムの標準的な文字列型の PnP の静的なテキスト プロパティをローカライズできます。 静的テキストに書式設定できる置換文字列をローカライズされていないデータを追加することもできます。

PE イメージの STRINGTABLE のリソース (通常は LoadString によって実行されます) にある文字列には、次の形式を使用する必要があります。

"@"System32\\mydll.dll、-21\[;フォールバック"文字列\]"

"@System32\\mydll.dll、-21\[;文字列 %1、%2、フォールバックしています. %n に\[; (Arg1, Arg2,..., ArgN)\]\]"

PE イメージのメッセージ テーブル リソースの (通常はドライバーでよく使用の詳細は、RtlFindMessage によって実行されます) にある文字列には、次の形式を使用する必要があります。

"@System32\\ドライバー\\mydriver.sys、\#21\[;フォールバック文字列\]"

"@System32\\ドライバー\\mydriver.sys、\#21\[;文字列 %1、%2、フォールバックしています. %n に\[; (Arg1, Arg2,..., ArgN)\]\]"

「代替文字列」は、返すことができる場合は、リソースが見つからないか読み込まれることはできませんのでは省略できますが、便利です。 フォールバックの文字列は、ユーザーの偽装はいないとようできないローカライズされたテキストをユーザーに表示します非対話型システムのプロセスにも返されます。

この手法では、呼び出し元のロケールに最も一致する文字列またはメッセージ テーブル リソースからプルされた静的なテキストをローカライズすることができます。

Windows は、後続の引数を書式設定文字列 (またはフォールバックの文字列) にはときに取得した同様のようにより、それぞれのリソース テーブルから RtlFormatMessage 同様です。

システム レベルのコンポーネントのシステムの既定のロケールでは、通常、"設定"操作を実行するコンポーネントからリソースを読み込むことで、プロパティを設定すると、カスタムの標準的な文字列型の静的なテキストの PnP がローカライズします。

注:PE イメージには、リソース テーブル型 (STRINGTABLE リソース、またはメッセージ テーブル リソース) を使用できます。

<a name="requirements"></a>要件
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p>バージョン</p></td>
<td align="left"><p>Windows Vista と Windows の以降のバージョン。</p></td>
</tr>
<tr class="even">
<td align="left"><p>Header</p></td>
<td align="left">Devpropdef.h (Devpropdef.h を含む)</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>関連項目


[**DEVPROP_TYPE_STRING**](devprop-type-string.md)

 

 






