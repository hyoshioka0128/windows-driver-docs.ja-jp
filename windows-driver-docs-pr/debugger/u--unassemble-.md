---
title: u、ub、uu (Unassemble)
description: U のコマンドは、メモリ内の指定したプログラム コード、アセンブリの翻訳を表示します。 このコマンドと混同しないで、~ (スレッドの固定の解除) u コマンド。
ms.assetid: 933a308c-61d1-4ca4-89c1-5749ba1b41c1
keywords:
- u、ub、uu (Unassemble) Windows のデバッグ
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- u, ub, uu (Unassemble)
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: a4e70cbe647cfb76cddcff3baa9e6669d1684904
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56579987"
---
# <a name="u-ub-uu-unassemble"></a>u、ub、uu (Unassemble)


**U\\*** コマンドでは、メモリ内、アセンブリの翻訳の指定したプログラム コードを表示します。

このコマンドと混同しないで、 [ **~ (スレッドの固定の解除) u** ](-u--unfreeze-thread-.md)コマンド。

```dbgcmd
u[u|b] Range 
u[u|b] Address
u[u|b] 
```

## <a name="span-idddkcmdunassembledbgspanspan-idddkcmdunassembledbgspanparameters"></a><span id="ddk_cmd_unassemble_dbg"></span><span id="DDK_CMD_UNASSEMBLE_DBG"></span>パラメーター


<span id="_______Range______"></span><span id="_______range______"></span><span id="_______RANGE______"></span> *範囲*   
逆アセンブルする指示を含む、メモリ範囲を指定します。 構文の詳細については、次を参照してください。[アドレスとアドレス範囲の構文](address-and-address-range-syntax.md)します。 使用する場合、 **b**フラグが指定する必要があります*範囲*を使用して、"*アドレス* **L * * * 長さ*"の構文、しない"、*住所 1 住所 2*"構文があります。

<span id="_______Address______"></span><span id="_______address______"></span><span id="_______ADDRESS______"></span> *アドレス*   
逆アセンブルするメモリの範囲の先頭を指定します。 (X86 ベースのプロセッサの場合) に 8 つの命令または (Itanium ベースのプロセッサの場合) の 9 つの手順については、アセンブリではありません。 構文の詳細については、次を参照してください。[アドレスとアドレス範囲の構文](address-and-address-range-syntax.md)します。

<span id="_______b______"></span><span id="_______B______"></span> **b**   
旧バージョンとカウントすることによって逆アセンブルするメモリの範囲を決定します。 場合**ub** *アドレス*が使用すると、逆アセンブルした範囲になりますで終わる 8 または 9 バイト範囲*アドレス*します。 構文を使用して、範囲が指定されている場合**ub** *アドレス* **L * * * 長さ*、逆アセンブルされた範囲終了に指定された長さの範囲になります*アドレス*します。

<span id="_______u______"></span><span id="_______U______"></span> **u**   
メモリの読み取りエラーがある場合でも、逆アセンブルは引き続きことを指定します。

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

パラメーターを指定しない場合、 **u**コマンドを逆アセンブルが現在のアドレスで開始され、(x86 ベースまたは x64 ベース プロセッサ) で 8 つの命令 (Itanium ベースのプロセッサの場合) 上の 9 つの手順を拡張します。 使用すると**ub**逆アセンブルにはパラメーターなしでは、現在のアドレスより前に、の 8 または 9 の指示が含まれています。

このコマンドを混同しないでください、 [ **(物理メモリから Unassemble) を**](up--unassemble-from-physical-memory-.md)します。 **U**コマンドは、仮想メモリだけを逆アセンブル中に、**を**コマンドは、物理メモリだけを逆アセンブルします。

 

 





