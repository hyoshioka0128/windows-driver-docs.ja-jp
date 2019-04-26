---
title: .asm (逆アセンブリ オプションの変更)
description: .Asm コマンドでは、逆アセンブリ コードの表示方法を制御します。
ms.assetid: c963c4f2-3bfc-4551-9b7b-74473a63eb11
keywords:
- 逆アセンブル オプション (.asm) コマンドを変更します。
- アセンブリのデバッグは、[逆アセンブル] オプションを変更する (.asm) コマンド
- .asm (逆アセンブリのオプションを変更) Windows のデバッグ
ms.date: 09/17/2018
topic_type:
- apiref
api_name:
- .asm (Change Disassembly Options)
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 35a76cb9f8294411d07ee652e693060901165313
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63337001"
---
# <a name="asm-change-disassembly-options"></a>.asm (逆アセンブリ オプションの変更)


**.Asm**コマンドは、逆アセンブリ コードの表示方法を制御します。

```dbgcmd
    .asm 
    .asm[-] Options
```

## <a name="span-idddkmetachangedisassemblyoptionsdbgspanspan-idddkmetachangedisassemblyoptionsdbgspanparameters"></a><span id="ddk_meta_change_disassembly_options_dbg"></span><span id="DDK_META_CHANGE_DISASSEMBLY_OPTIONS_DBG"></span>パラメーター


<span id="_______-______"></span> **-**   
により指定されたオプションは無効にします。 マイナス記号を使用しない場合は、指定したオプションを有効になります。

<span id="_______Options______"></span><span id="_______options______"></span><span id="_______OPTIONS______"></span> *オプション*   
次のオプションの任意の数を指定できます。

<span id="ignore_output_width"></span><span id="IGNORE_OUTPUT_WIDTH"></span>**ignore\_output\_width**  
デバッガーが逆アセンブルの表示で線の幅をチェックするを防ぎます。

<span id="no_code_bytes"></span><span id="NO_CODE_BYTES"></span>**いいえ\_コード\_バイト**  
(x86 および x64 ターゲットのみ)実際のバイトを表示をしません。

<span id="source_line"></span><span id="SOURCE_LINE"></span>**ソース\_行**  
プレフィックスの各行の逆アセンブリのソース コードの行番号を使用します。

<span id="verbose"></span><span id="VERBOSE"></span>**詳細**  
(Itanium のターゲットのみ)標準の逆アセンブリの情報と共に表示されるバンドルの種類の情報をによりします。

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

アセンブリの説明については、デバッグ、および関連するコマンドを参照してください[モードのアセンブリでのデバッグ](debugging-in-assembly-mode.md)します。

<a name="remarks"></a>注釈
-------

使用して **.asm**自体で、オプションの現在の状態が表示されます。

このコマンドでは、デバッガー コマンド ウィンドウで、逆アセンブリ命令の表示に影響します。 WinDbg で逆アセンブル ウィンドウの内容も変更されます。

 

 





