---
title: ds、dS (表示文字列)
description: Ds および dS コマンドは、文字列、ANSI_STRING、または UNICODE_STRING 構造を表示します。
ms.assetid: cb05e89c-6c83-476b-a577-a6aeefd8cdd6
keywords:
- ds、dS (表示文字列) の Windows デバッグ
ms.date: 05/03/2018
topic_type:
- apiref
api_name:
- ds, dS (Display String)
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: a03159b71e8194b825ffb1df2f40c32ba20d8eaf
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56553762"
---
# <a name="ds-ds-display-string"></a>ds、dS (表示文字列)


**Ds**と**dS**コマンド表示文字列を ANSI\_文字列、または UNICODE\_文字列*構造*します。 

これらのコマンドは、null 区切り文字の文字列には表示されませんが、構造体を文字列ではなく。

Unicode 文字列の文字のアドレスがある場合は、代わりに du コマンドを使用し。 Da コマンドを使用すると、ASCII 文字を表示できます。 詳細については、[d、da、db、dc、dd、dD、df、dp、dq、du、dw (表示メモリ)](https://docs.microsoft.com/windows-hardware/drivers/debugger/d--da--db--dc--dd--dd--df--dp--dq--du--dw--dw--dyb--dyd--display-memor)を参照してください。

```dbgcmd
d{s|S} [/c Width] [Address]
```

## <a name="span-idddkcmddisplaystringdbgspanspan-idddkcmddisplaystringdbgspanparameters"></a><span id="ddk_cmd_display_string_dbg"></span><span id="DDK_CMD_DISPLAY_STRING_DBG"></span>パラメーター


<span id="_______s______"></span><span id="_______S______"></span> **s**   
指定する文字列または ANSI\_文字列構造体が表示されます。 (この**s**小文字が区別されます)。

<span id="_______S______"></span><span id="_______s______"></span> **S**   
指定します、UNICODE\_文字列構造体が表示されます。 (この**S**小文字が区別されます)。

<span id="________c_______Width______"></span><span id="________c_______width______"></span><span id="________C_______WIDTH______"></span> **/c** *幅*   
行ごとに表示する文字数を指定します。 この数値には、null 文字が含まれますは表示されません。

<span id="_______Address______"></span><span id="_______address______"></span><span id="_______ADDRESS______"></span> *アドレス*   
メモリ アドレス where UNICODE_STRING 構造が格納されます。 

構文の詳細については、[アドレスとアドレス範囲の構文](address-and-address-range-syntax.md)を参照してください。 省略した場合、表示のコマンドで使用される最後のアドレスが使用されます。

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

その他のメモリに関連するコマンドの説明とメモリの操作の概要については、[読み取りと書き込みメモリ](reading-and-writing-memory.md)を参照してください。

<a name="remarks"></a>注釈
-------

[ローカル] ウィンドウまたは WinDbg のウォッチ ウィンドウで Unicode 文字列を表示する場合は、使用する必要があります、 [**リストア\_(Unicode 表示を有効にする) unicode** ](-enable-unicode--enable-unicode-display-.md)最初コマンドします。

 

 





