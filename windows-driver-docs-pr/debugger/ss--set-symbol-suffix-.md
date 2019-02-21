---
title: ss (セット記号サフィックス)
description: Ss コマンドを設定またはシンボルの数値式の照合に使用される現在のサフィックスの値を表示します。
ms.assetid: acf4cf2e-5b09-4d46-aa42-e539ee968685
keywords:
- ss (セット記号サフィックス) の Windows デバッグ
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- ss (Set Symbol Suffix)
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: c230128657006ddbaa3d1504fe8c88515e6d6e3f
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56536741"
---
# <a name="ss-set-symbol-suffix"></a>ss (セット記号サフィックス)


**Ss**コマンドを設定またはシンボルの数値式の照合に使用される現在のサフィックスの値が表示されます。

```dbgcmd
ss [a|w|n] 
```

## <a name="span-idddkcmdsetsymbolsuffixdbgspanspan-idddkcmdsetsymbolsuffixdbgspanparameters"></a><span id="ddk_cmd_set_symbol_suffix_dbg"></span><span id="DDK_CMD_SET_SYMBOL_SUFFIX_DBG"></span>パラメーター


<span id="_______a______"></span><span id="_______A______"></span> **A**   
記号のサフィックスは"A"である必要がありますを指定します。 一致する多くの ASCII シンボル。

<span id="_______w______"></span><span id="_______W______"></span> **w**   
記号のサフィックスがあることを指定します。"W"、多くの Unicode 記号に一致します。

<span id="_______n______"></span><span id="_______N______"></span> **n**   
デバッガーがシンボル サフィックスを使用しないことを指定します。 (このパラメーターは、既定の動作です)。

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

一致するシンボルの詳細については、次を参照してください。[シンボルの構文と照合シンボル](symbol-syntax-and-symbol-matching.md)します。

<a name="remarks"></a>注釈
-------

指定した場合、 **ss**サフィックスの値の現在の状態が表示されると共に、パラメーターのないコマンドします。

 

 





