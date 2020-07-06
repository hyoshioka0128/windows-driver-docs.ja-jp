---
title: d、da、db、dc、dd、dD、df、dp、dq、du、dw (Display Memory)
description: D * コマンドは、指定された範囲のメモリの内容を表示します。
ms.assetid: deb58b77-6648-466d-be00-e2e0a92895b5
keywords:
- d、da、db、dc、dd、dD、df、dp、dq、du、dw (Display Memory) Windows デバッグ
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- d, da, db, dc, dd, dD, df, dp, dq, du, dw (Display Memory)
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: f895a8aef458a9d1cfb4c7d8943665c73e3a3e4a
ms.sourcegitcommit: ca5045a739eefd6ed14b9dbd9249b335e090c4e9
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/06/2020
ms.locfileid: "85968029"
---
# <a name="d-da-db-dc-dd-dd-df-dp-dq-du-dw-display-memory"></a>d、da、db、dc、dd、dD、df、dp、dq、du、dw (Display Memory)


**D \* **コマンドは、指定された範囲のメモリの内容を表示します。

```dbgcmd
d{a|b|c|d|D|f|p|q|u|w|W} [Options] [Range] 
dy{b|d} [Options] [Range] 
d [Options] [Range] 
```

## <a name="span-idddk_cmd_display_memory_dbgspanspan-idddk_cmd_display_memory_dbgspanparameters"></a><span id="ddk_cmd_display_memory_dbg"></span><span id="DDK_CMD_DISPLAY_MEMORY_DBG"></span>パラメータ


<span id="_______Options______"></span><span id="_______options______"></span><span id="_______OPTIONS______"></span>*オプション*   
1つ以上の表示オプションを指定します。 次のオプションのいずれかを含めることができます。ただし、1つの **/p**オプションを指定することはできません \* 。

<span id="_cWidth"></span><span id="_cwidth"></span><span id="_CWIDTH"></span>**/c**_幅_  
表示に使用する列の数を指定します。 これを省略した場合、既定の列数は表示の種類によって異なります。

<span id="_p"></span><span id="_P"></span>**/p**  
(カーネルモードのみ)ディスプレイの物理メモリアドレスを使用します。 *範囲*で指定された範囲は、仮想メモリではなく物理メモリから取得されます。

<span id="_p_c_"></span><span id="_P_C_"></span>**/p \[ c\]**  
(カーネルモードのみ)**/P**と同じですが、キャッシュされたメモリが読み取られる点が異なります。 **C**を囲む角かっこを含める必要があります。

<span id="_p_uc_"></span><span id="_P_UC_"></span>**/p \[ uc\]**  
(カーネルモードのみ)**/P**と同じですが、キャッシュされていないメモリが読み取られる点が異なります。 **Uc**を囲む角かっこを含める必要があります。

<span id="_p_wc_"></span><span id="_P_WC_"></span>**/p \[ wc\]**  
(カーネルモードのみ)書き込み結合メモリが読み込まれる点を除いて、 **/p**と同じです。 **Wc**を囲む角かっこを含める必要があります。

<span id="_______Range______"></span><span id="_______range______"></span><span id="_______RANGE______"></span>*範囲*   
表示するメモリ領域を指定します。 構文の詳細については、「[アドレスとアドレス範囲の構文](address-and-address-range-syntax.md)」を参照してください。 *Range*を省略した場合、コマンドは最後の display コマンドの終了位置からメモリを表示します。 *Range*が省略されていて、前の表示コマンドが使用されていない場合は、現在の命令ポインターから表示が開始されます。

### <a name="span-idenvironmentspanspan-idenvironmentspanspan-idenvironmentspanenvironment"></a><span id="Environment"></span><span id="environment"></span><span id="ENVIRONMENT"></span>Environment

**モード**: ユーザーモード、カーネルモード

**ターゲット**: ライブ、クラッシュダンプ

**プラットフォーム**: すべて

 

### <a name="span-idadditional_informationspanspan-idadditional_informationspanspan-idadditional_informationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>追加情報

メモリ操作の概要とその他のメモリ関連コマンドの説明については、「[メモリの読み取りと書き込み](reading-and-writing-memory.md)」を参照してください。

<a name="remarks"></a>注釈
-------

表示される各行には、行の最初のバイトのアドレスと、それに続く位置のメモリの内容が含まれます。

*Range*を省略した場合、コマンドは最後の display コマンドの終了位置からメモリを表示します。 これにより、メモリを継続的にスキャンできます。

このコマンドは、次の形式で存在します。 **Dd**、 **dd**、 **dw**、 **dw**の各コマンドの2番目の文字は、 **dyb**および**dyb**コマンドの3番目の文字と同様に、大文字と小文字が区別されます。

|コマンド|ディスプレイ|
|--- |--- |
|d|これにより、最新の d コマンドと同じ形式でデータが表示されます。 前の d コマンドが発行されていない場合、d は db と同じ効果を持ちます。 D で始まる最新のコマンドが d で繰り返されていることに注意してください。 これには、dda、ddp、ddu、dpa、ddu、ddu、ddu、ddu、dqu、dds、dps、dqs、ds、dS、dg、dl、dt、dv のほか、このページの表示コマンドも含まれます。 D の後に指定されたパラメーターが適切でない場合は、エラーが発生する可能性があります。|
|da|ASCII 文字。 各行には最大48文字が表示されます。 表示は、最初の null バイトまで、または範囲内のすべての文字が表示されるまで続行されます。 復帰や改行など、印刷できない文字はすべてピリオド (.) で表示されます。|
|db|バイト値と ASCII 文字。 各表示線には、行の最初のバイトのアドレスの後に16進数の最大16バイト値が表示されます。 バイト値の直後に、対応する ASCII 値が続きます。 8番目と9番目の16進値は、ハイフン (-) で区切られます。 復帰や改行など、印刷できない文字はすべてピリオド (.) で表示されます。 既定の数は128バイトです。|
|dc|ダブルワード値 (4 バイト) と ASCII 文字。 各表示線には、行の最初の単語のアドレスと、最大8個の16進単語の値、およびそれに対応する ASCII の値が表示されます。 既定の数は 32 Dword (128 バイト) です。| 
|dd|ダブルワード値 (4 バイト)。既定の数は 32 Dword (128 バイト) です。|
|dD|倍精度浮動小数点数 (8 バイト)。 既定のカウントは15桁 (120 バイト) です。|
|df|単精度浮動小数点数 (4 バイト)。 既定の数は16桁 (64 バイト) です。|
|dp|ポインターサイズの値。 このコマンドは、対象のコンピューターのプロセッサアーキテクチャが32ビットまたは64ビットのどちらであるかによって、dd または dq に相当します。 既定の数は 32 Dword または16個のクワッドワード (128 バイト) です。|
|dq|クワッドワード値 (8 バイト)。 既定のカウントは、16個のクワッドワード (128 バイト) です。|
|du|Unicode 文字。 各行には最大48文字が表示されます。 表示は、最初の null バイトまで、または範囲内のすべての文字が表示されるまで続行されます。 復帰や改行など、印刷できない文字はすべてピリオド (.) で表示されます。|
|dw|単語の値 (2 バイト)。 各表示線には、行の最初の単語のアドレスと、最大8個の16進単語の値が表示されます。 既定のカウントは64語 (128 バイト) です。|
|dW|Word の値 (2 バイト) と ASCII 文字。 各表示線には、行の最初の単語のアドレスと、最大8個の16進単語の値が表示されます。 既定のカウントは64語 (128 バイト) です。|
|dyb|バイナリ値とバイト値。 既定の数は32バイトです。|
|dyd|バイナリ値とダブルワード値 (4 バイト)。 既定の数は 8 Dword (32 バイト) です。|

 

無効なアドレスを表示しようとすると、その内容は疑問符 (**?**) として表示されます。

 

 





