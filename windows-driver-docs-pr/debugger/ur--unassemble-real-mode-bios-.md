---
title: (リアル モードを逆アセンブル BIOS)
description: コマンドは、アセンブリの翻訳の指定した 16 ビットのリアル モードのコードを表示します。
ms.assetid: 7ea3421a-3841-47ea-ab40-99d10516bb14
keywords:
- (リアル モードを逆アセンブル BIOS) Windows のデバッグ
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- ur (Unassemble Real Mode BIOS)
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 5922e23340d416f45f37fa88917f8e20afe7322e
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56530197"
---
# <a name="ur-unassemble-real-mode-bios"></a>(リアル モードを逆アセンブル BIOS)


**、** コマンドは、アセンブリの翻訳の指定した 16 ビットのリアル モードのコードを表示します。

```dbgcmd
ur Range 
ur Address
ur 
```

## <a name="span-idddkcmdunassemblerealmodebiosdbgspanspan-idddkcmdunassemblerealmodebiosdbgspanparameters"></a><span id="ddk_cmd_unassemble_real_mode_bios_dbg"></span><span id="DDK_CMD_UNASSEMBLE_REAL_MODE_BIOS_DBG"></span>パラメーター


<span id="_______Range______"></span><span id="_______range______"></span><span id="_______RANGE______"></span> *範囲*   
逆アセンブルする指示を含む、メモリ範囲を指定します。 構文の詳細については、[アドレスとアドレス範囲の構文](address-and-address-range-syntax.md)を参照してください。

<span id="_______Address______"></span><span id="_______address______"></span><span id="_______ADDRESS______"></span> *アドレス*   
逆アセンブルするメモリの範囲の先頭を指定します。 (X86 ベースのプロセッサの場合) に 8 つの命令または (Itanium ベースのプロセッサの場合) の 9 つの手順については、アセンブリではありません。 構文の詳細については、[アドレスとアドレス範囲の構文](address-and-address-range-syntax.md)を参照してください。

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

BIOS のコードをデバッグする方法の詳細については、[BIOS コードのデバッグ](debugging-bios-code.md)を参照してください。

<a name="remarks"></a>注釈
-------

指定しない場合*範囲*または*アドレス*、逆アセンブルが現在のアドレスで開始され、(x86 ベースのプロセッサの場合) に 8 つの命令 (Itanium ベースのプロセッサの場合) 上の 9 つの手順を拡張します。

X86 ベースのプロセッサでは、上の 16 ビットのリアル モード コードを調べている場合両方、 **、** コマンドと[ **u (Unassemble)** ](u--unassemble-.md)コマンドには、正しい結果が得られます。

ただし、リアル モードのコードは、デバッガーがない場所に存在する場合 (たとえば、x86 以外コンピューターまたは x86 ベースの BIOS コード プラグイン カードからのエミュレートされる)、予期する必要があります使用 **、** これを正しく逆アセンブルするにはコードです。

使用する場合 **、** 32 ビットまたは 64 ビットのコードで、コマンドが 16 ビット コードの場合と同様に、コードを逆アセンブルを試みます。 このような状況では、意味のない結果を生成します。

 

 





