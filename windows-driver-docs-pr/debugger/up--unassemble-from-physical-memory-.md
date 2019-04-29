---
title: up (物理メモリからの逆アセンブル)
description: コマンドでは、物理メモリの中に、アセンブリの翻訳の指定したプログラム コードが表示されます。
ms.assetid: 4db66566-b7b8-4f1e-9492-b4b78016b45a
keywords:
- (物理メモリから Unassemble) Windows のデバッグ
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- up (Unassemble from Physical Memory)
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 8bceebc2d2b5969f9d5631bbab5e5740882220b8
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63383747"
---
# <a name="up-unassemble-from-physical-memory"></a>up (物理メモリからの逆アセンブル)


**を**コマンドは、物理メモリに、アセンブリの翻訳の指定したプログラム コードを表示します。

```dbgcmd
up Range 
up Address 
up 
```

## <a name="span-idddkcmdunassembledbgspanspan-idddkcmdunassembledbgspanparameters"></a><span id="ddk_cmd_unassemble_dbg"></span><span id="DDK_CMD_UNASSEMBLE_DBG"></span>パラメーター


<span id="_______Range______"></span><span id="_______range______"></span><span id="_______RANGE______"></span> *範囲*   
逆アセンブルする指示が含まれている物理メモリでは、メモリ範囲を指定します。 構文の詳細については、次を参照してください。[アドレスとアドレス範囲の構文](address-and-address-range-syntax.md)します。

<span id="_______Address______"></span><span id="_______address______"></span><span id="_______ADDRESS______"></span> *アドレス*   
逆アセンブルする物理メモリでは、メモリ範囲の先頭を指定します。 (X86 ベースのプロセッサの場合) に 8 つの命令または (Itanium ベースのプロセッサの場合) の 9 つの手順については、アセンブリではありません。 構文の詳細については、次を参照してください。[アドレスとアドレス範囲の構文](address-and-address-range-syntax.md)します。

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

<a name="remarks"></a>注釈
-------

パラメーターを指定しない場合、**を**コマンドを逆アセンブルが現在のアドレスに開始し、8 つの命令 (上の x86 ベースのプロセッサの場合) または (Itanium ベースのプロセッサの場合) 上の 9 つの手順を拡張します。

このコマンドを混同しないでください、 [ **u (Unassemble)**](u--unassemble-.md)します。 **を**コマンドは、物理メモリだけを逆アセンブル中に、 **u**コマンドは、仮想メモリだけを逆アセンブルします。

 

 





