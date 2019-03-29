---
title: uf (関数の逆アセンブル)
description: Uf コマンドでは、メモリの中に指定された関数のアセンブリの翻訳が表示されます。
ms.assetid: 344e3afd-6b8d-48f2-9e07-dd7e1937f71b
keywords:
- uf (関数の逆アセンブル) Windows のデバッグ
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- uf (Unassemble Function)
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 5e4dd50771339718b2a6c77a6c062100db3e8dca
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56572706"
---
# <a name="uf-unassemble-function"></a>uf (関数の逆アセンブル)


**Uf**コマンドは、メモリ内で指定された関数のアセンブリの変換を表示します。

```dbgcmd
uf [Options] Address
```

## <a name="span-idddkcmdunassemblefunctiondbgspanspan-idddkcmdunassemblefunctiondbgspanparameters"></a><span id="ddk_cmd_unassemble_function_dbg"></span><span id="DDK_CMD_UNASSEMBLE_FUNCTION_DBG"></span>パラメーター


<span id="_______Options______"></span><span id="_______options______"></span><span id="_______OPTIONS______"></span> *オプション*   
1 つまたは複数の次のオプション:

<span id="_c"></span><span id="_C"></span>**/c**  
完全な混合モードではなく、ルーチンの呼び出し命令のみが表示されます。 呼び出し命令は、逆アセンブルしたコードから呼び出し元と呼び出し先の関係の決定に役立ちます。

<span id="_D"></span><span id="_d"></span>**/D**  
呼び出し先のナビゲーション リンクの呼び出し先名を作成します。

<span id="_m"></span><span id="_M"></span>**/m**  
複数の終了を許可するようにブロックしている要件を緩和します。

<span id="_o"></span><span id="_O"></span>**/o**  
関数のオフセットでアドレスの代わりに、表示を並べ替えます。 このオプションは、完全な関数のメモリ レイアウト ビューを表示します。

<span id="_O"></span><span id="_o"></span>**/O**  
情報とブレークポイントの作成に呼び出しにアクセスするは、呼び出しのリンクされた行を作成します。

<span id="_i"></span><span id="_I"></span>**/i**  
ルーチンでは、命令の数を表示します。

<span id="_______Address______"></span><span id="_______address______"></span><span id="_______ADDRESS______"></span> *アドレス*   
逆アセンブルする関数のアドレスを指定します。 構文の詳細については、次を参照してください。[アドレスとアドレス範囲の構文](address-and-address-range-syntax.md)します。

### <a name="span-idenvironmentspanspan-idenvironmentspanspan-idenvironmentspanenvironment"></a><span id="Environment"></span><span id="environment"></span><span id="ENVIRONMENT"></span>環境

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>モード</strong></p></td>
<td align="left"><p>ユーザー モードでは、カーネル モード</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>ターゲット</strong></p></td>
<td align="left"><p>ライブ、クラッシュ ダンプ</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>プラットフォーム</strong></p></td>
<td align="left"><p>すべての</p></td>
</tr>
</tbody>
</table>

 

### <a name="span-idadditionalinformationspanspan-idadditionalinformationspanspan-idadditionalinformationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>追加情報

アセンブリの詳細については、デバッグ、および関連するコマンドを参照してください[モードのアセンブリでのデバッグ](debugging-in-assembly-mode.md)します。

<a name="remarks"></a>コメント
-------

関数の順序に従って、関数全体が表示されます。

 

 





