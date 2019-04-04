---
title: .fiximports (修正対象モジュールのインポート)
description: .Fiximports コマンドでは、検証し、対象のモジュールのすべての静的インポート リンクを修正します。
ms.assetid: 584a5060-5ab5-4126-bfec-e2fe647d50ff
keywords:
- ターゲット モジュールのインポート (.fiximports) コマンドを修正します。
- .fiximports (修正対象モジュールのインポート) の Windows デバッグ
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- .fiximports (Fix Target Module Imports)
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 92a5ef997dc3ae8bc85d4bb762a93994e6b38ad1
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56531531"
---
# <a name="fiximports-fix-target-module-imports"></a>.fiximports (修正対象モジュールのインポート)


**.Fiximports**コマンドを検証し、対象のモジュールのすべての静的インポート リンクを修正します。

```dbgcmd
.fiximports Module
```

## <a name="span-idddkmetafixtargetmoduleimportsdbgspanspan-idddkmetafixtargetmoduleimportsdbgspanparameters"></a><span id="ddk_meta_fix_target_module_imports_dbg"></span><span id="DDK_META_FIX_TARGET_MODULE_IMPORTS_DBG"></span>パラメーター


<span id="_______Module______"></span><span id="_______module______"></span><span id="_______MODULE______"></span> *モジュール*   
ターゲット モジュールがインポートがデバッガーの修正を指定します。 *モジュール*さまざまなワイルドカード文字と指定子を含めることができます。 構文の詳細については、[文字列のワイルドカード構文](string-wildcard-syntax.md)を参照してください。 内のスペースを含める場合*モジュール*パラメーターを引用符で囲む必要があります。

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
<td align="left"><p>クラッシュ ダンプのみ (ミニダンプのみ)</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>プラットフォーム</strong></p></td>
<td align="left"><p>すべての</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>注釈
-------

使用することができます、 **.fiximports**独自の実行可能イメージがないミニダンプが場合にのみ、ターゲット コマンドします。

デバッガーは、メモリとして使用するためのイメージをマップとデバッガーではエクスポーターのイメージのインポートは自動的に接続しません。 そのため、インポートを参照する手順についてはライブ デバッグ セッションと同じ方法で逆アセンブルします。 使用することができます **.fiximports**を適切なインポートのリンク、デバッガーの実行を要求します。

 

 





