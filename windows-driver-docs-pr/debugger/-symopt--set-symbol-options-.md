---
title: .symopt (シンボル オプションを設定)
description: .Symopt コマンドを設定またはシンボルのオプションが表示されます。
ms.assetid: 0793baa3-14f7-48df-8773-736b6a5470e6
keywords:
- .symopt (シンボル オプションを設定する) Windows のデバッグ
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- .symopt (Set Symbol Options)
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 4654c414d39a4c213818d269c08653c03efb85a0
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56559008"
---
# <a name="symopt-set-symbol-options"></a>.symopt (シンボル オプションを設定)


**.Symopt**コマンドを設定またはシンボルのオプションが表示されます。

```dbgcmd
.symopt+ Flags 
.symopt- Flags 
.symopt 
```

## <a name="span-idddkmetasetsymboloptionsdbgspanspan-idddkmetasetsymboloptionsdbgspanparameters"></a><span id="ddk_meta_set_symbol_options_dbg"></span><span id="DDK_META_SET_SYMBOL_OPTIONS_DBG"></span>パラメーター


<span id="______________"></span> **+**   
シンボル オプションを指定してにより*フラグ*を設定します。 場合 **.symopt**併用*フラグ*がないプラスまたはマイナス記号、プラス記号が使われます。

<span id="_______-______"></span> **-**   
シンボル オプションを指定してにより*フラグ*クリアします。

<span id="_______Flags______"></span><span id="_______flags______"></span><span id="_______FLAGS______"></span> *フラグ*   
変更するシンボルのオプションを指定します。 *フラグ*シンボル オプションをこれらのビット フラグの合計をする必要があります。

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
<td align="left"><p>all</p></td>
</tr>
</tbody>
</table>

 

### <a name="span-idadditionalinformationspanspan-idadditionalinformationspanspan-idadditionalinformationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>追加情報

リストと各シンボル オプションや、ビット フラグを設定してこれらのオプションをオフにすると、他の方法の説明では、[シンボル オプションを設定](symbol-options.md)を参照してください。

<a name="remarks"></a>注釈
-------

任意の引数を指定せず **.symopt**現在のシンボルのオプションが表示されます。

 

 





