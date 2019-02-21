---
title: '%ld (シンボルの読み込み)'
description: '%Ld 個のコマンドは、指定したモジュールのシンボルを読み込み、すべてのモジュール情報を更新します。'
ms.assetid: 1dae519f-8dd1-4f30-98f4-fe904454c84c
keywords:
- '%ld (シンボルの読み込み) の Windows デバッグ'
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- ld (Load Symbols)
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 606e10615b5c49e421f448d95991d0ad77956578
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56535725"
---
# <a name="ld-load-symbols"></a>%ld (シンボルの読み込み)


**%Ld**コマンドを指定したモジュールのシンボルを読み込み、モジュールのすべての情報を更新します。

```dbgcmd
ld ModuleName [/f FileName]
```

## <a name="span-idddkcmdloadsymbolsdbgspanspan-idddkcmdloadsymbolsdbgspanparameters"></a><span id="ddk_cmd_load_symbols_dbg"></span><span id="DDK_CMD_LOAD_SYMBOLS_DBG"></span>パラメーター


<span id="_______ModuleName______"></span><span id="_______modulename______"></span><span id="_______MODULENAME______"></span> *ModuleName*   
シンボルが読み込まれるモジュールの名前を指定します。 *ModuleName*さまざまなワイルドカード文字と指定子を含めることができます。

<span id="________f_______FileName______"></span><span id="________f_______filename______"></span><span id="________F_______FILENAME______"></span> **/f** *FileName*   
一致の選択された名前を変更します。 既定では、モジュール名が一致するしますが、 **/f**されるモジュール名の代わりに、ファイル名が一致します。 *ファイル名*さまざまなワイルドカード文字と指定子を含めることができます。 ワイルドカード文字と指定子の構文の詳細については、次を参照してください。[文字列のワイルドカード構文](string-wildcard-syntax.md)します。

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

 

<a name="remarks"></a>注釈
-------

デバッガーの既定の動作が使用するには*シンボルの遅延読み込み*(とも呼ばれます[シンボルの読み込みの遅延](deferred-symbol-loading.md))。 これは必要になるまでには、シンボルが実際に読み込まれるしないことを意味します。

**%Ld**コマンド、その一方で、強制的に読み込まれる指定したモジュールのすべてのシンボルです。

### <a name="span-idadditionalinformationspanspan-idadditionalinformationspanspan-idadditionalinformationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>追加情報

遅延 (遅延) シンボルの読み込みの詳細については、次を参照してください。[シンボルの遅延読み込み](deferred-symbol-loading.md)します。 その他のシンボルのオプションの詳細については、次を参照してください。[シンボル オプションを設定](symbol-options.md)します。

 

 





