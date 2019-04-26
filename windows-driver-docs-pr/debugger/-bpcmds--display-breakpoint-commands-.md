---
title: .bpcmds (ブレークポイント コマンドの表示)
description: .Bpcmds コマンドには、現在のブレークポイントの各設定に使用されたコマンドが表示されます。
ms.assetid: 96c13c54-8d85-414c-9775-a0373459dc7a
keywords:
- .bpcmds (ブレークポイント コマンドが表示) の Windows デバッグ
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- .bpcmds (Display Breakpoint Commands)
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 8d77eebdf2b11279981f51560ab849f9ae985f4f
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63336989"
---
# <a name="bpcmds-display-breakpoint-commands"></a>.bpcmds (ブレークポイント コマンドの表示)


**.Bpcmds**コマンドには、現在のブレークポイントの各設定に使用されたコマンドが表示されます。

```dbgcmd
    .bpcmds
```

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

詳細とブレークポイント、他のコマンドのブレークポイントとブレークポイントを制御する方法を使用する方法の例については、次を参照してください。[を使用してブレークポイント](using-breakpoints.md)します。

<a name="remarks"></a>注釈
-------

明確ではありません、アドレス、シンボル参照の場合、またはシンボルに特定のブレークポイントを設定するかどうかを場合、使用して、 **.bpcmds**ブレークポイント コマンドは、その作成に使用されたコマンドを示しています。 ブレークポイントを作成するために使用されたコマンドは、その性質を決定します。

-   [ **Bp (ブレークポイントの設定)** ](bp--bu--bm--set-breakpoint-.md)コマンドは、アドレスの位置にブレークポイントを設定します。

-   [ **Bu (未解決のブレークポイントの設定)** ](bp--bu--bm--set-breakpoint-.md)コマンドでは、参照をシンボリックにブレークポイントを設定します。

-   [ **Bm (シンボルのブレークポイントの設定)** ](bp--bu--bm--set-breakpoint-.md)コマンドでは、指定したパターンに一致するシンボルにブレークポイントを設定します。 場合、 **/d**スイッチが含まれる、0 個以上のブレークポイントを作成します (bp) などのアドレスをそれ以外の場合 (bu) などのシンボル参照に 0 個以上のブレークポイントを作成します。

-   [ **Ba (アクセスの切断)** ](ba--break-on-access-.md)コマンドは、アドレスの位置にデータ ブレークポイントを設定します。

出力 **.bpcmds**各ブレークポイントの現在の性質が反映されます。 各行の **.bpcmds**表示を作成するために使用するコマンドを使用して開始 (**bp**、 **bu**、または**ba**) 後に、ブレークポイント ID とブレークポイントの位置。

ブレークポイントがによって作成された場合**ba**アクセスの種類とサイズも表示されます。

ブレークポイントがによって作成された場合**bm**せず、 **/d**スイッチ、表示、ブレークポイントの種類として**bu**評価のシンボル、で囲まれていると、その後 **@!""** (これは、リテラル文字いないな数値式またはレジスタを示します) トークンです。 ブレークポイントがによって作成された場合**bm**で、 **/d**スイッチ、表示、ブレークポイントの種類として**bp**します。

以下に例を示します。

```dbgcmd
0:000> bp notepad!winmain 

0:000> .bpcmds 
bp0 0x00000001`00003340 ;

0:000> bu myprog!winmain 
breakpoint 0 redefined

0:000> .bpcmds 
bu0 notepad!winmain;

0:000> bu myprog!LoadFile 

0:000> bp myprog!LoadFile+10 

0:000> bm myprog!openf* 
  3: 00421200 @!"myprog!openFile"
  4: 00427800 @!"myprog!openFilter"

0:000> bm /d myprog!closef* 
  5: 00421600 @!"myprog!closeFile"

0:000> ba r2 myprog!LoadFile+2E 

0:000> .bpcmds
bu0 notepad!winmain;
bu1 notepad!LoadFile;
bp2 0x0042cc10 ;
bu3 @!"myprog!openFile";
bu4 @!"myprog!openFilter";
bp5 0x00421600 ;
ba6 r2 0x0042cc2e ;
```

この例では、出力の **.bpcmds** (介在するスペースなし) とブレークポイント番号の後に関連するコマンド ("bu"、"bp"または"ba") で始まります。

ブレークポイント番号 0 の使用が設定されていたため、注意**bp**が再定義を使用して、 **bu**、"bu"としてその型が表示されます。

3、4、および 5、によって作成されたそのブレークポイントも注意してください、 **bm**この例で示されているコマンドのいずれかの種類"bp"として表示されますまたは型かどうかに応じて"bu"、、 **/d**スイッチが含まれている場合。**bm**が使用されました。

 

 





