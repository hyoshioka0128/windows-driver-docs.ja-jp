---
title: d、da、db、dc、dd、dD、df、dp、dq、du、dw (表示メモリ)
description: D のコマンドは、特定の範囲内のメモリの内容を表示します。
ms.assetid: deb58b77-6648-466d-be00-e2e0a92895b5
keywords:
- d、da、db、dc、dd、dD、df、dp、dq、du、dw (表示メモリ) の Windows デバッグ
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- d, da, db, dc, dd, dD, df, dp, dq, du, dw (Display Memory)
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: fa50f4a4698824200407038302c1b916ae12fd15
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56558731"
---
# <a name="d-da-db-dc-dd-dd-df-dp-dq-du-dw-display-memory"></a>d、da、db、dc、dd、dD、df、dp、dq、du、dw (表示メモリ)


**D\\*** のコマンドは、特定の範囲内でメモリの内容を表示します。

```dbgcmd
d{a|b|c|d|D|f|p|q|u|w|W} [Options] [Range] 
dy{b|d} [Options] [Range] 
d [Options] [Range] 
```

## <a name="span-idddkcmddisplaymemorydbgspanspan-idddkcmddisplaymemorydbgspanparameters"></a><span id="ddk_cmd_display_memory_dbg"></span><span id="DDK_CMD_DISPLAY_MEMORY_DBG"></span>パラメーター


<span id="_______Options______"></span><span id="_______options______"></span><span id="_______OPTIONS______"></span> *オプション*   
1 つまたは複数の表示オプションを指定します。 次のオプションを含めることができ個を超える 1 つを除く **/p** \*オプションを示すことができます。

<span id="_cWidth"></span><span id="_cwidth"></span><span id="_CWIDTH"></span>**/c***Width*  
表示に使用する列の数を指定します。 これを省略すると、既定の列数は、表示の種類によって異なります。

<span id="_p"></span><span id="_P"></span>**/p**  
(カーネル モードのみ)表示の物理メモリ アドレスを使用します。 指定された範囲*範囲*は仮想メモリではなく、物理メモリから取得されます。

<span id="_p_c_"></span><span id="_P_C_"></span>**/p\[c\]**  
(カーネル モードのみ)同じ **/p**, キャッシュ メモリが読み取られる点が異なります。 かっこ、 **c**含める必要があります。

<span id="_p_uc_"></span><span id="_P_UC_"></span>**/p\[uc\]**  
(カーネル モードのみ)同じ **/p**, キャッシュされていないメモリが読み取られる点が異なります。 かっこ、 **uc**含める必要があります。

<span id="_p_wc_"></span><span id="_P_WC_"></span>**/p\[wc\]**  
(カーネル モードのみ)同じ **/p**, 書き込み結合のメモリが読み取られる点が異なります。 かっこ、 **wc**含める必要があります。

<span id="_______Range______"></span><span id="_______range______"></span><span id="_______RANGE______"></span> *範囲*   
表示するメモリ領域を指定します。 構文の詳細については、次を参照してください。[アドレスとアドレス範囲の構文](address-and-address-range-syntax.md)します。 省略した場合*範囲*、最後の表示コマンドの終了位置から始まるメモリが表示されます。 場合*範囲*省略してない前の表示は、コマンドが使用されている、現在の命令ポインターで、表示が開始されます。

### <a name="span-idenvironmentspanspan-idenvironmentspanspan-idenvironmentspanenvironment"></a><span id="Environment"></span><span id="environment"></span><span id="ENVIRONMENT"></span>環境

|||
|--- |--- |
|モード|ユーザー モードでは、カーネル モード|
|ターゲット|ライブ、クラッシュ ダンプ|
|プラットフォーム|all|
 

### <a name="span-idadditionalinformationspanspan-idadditionalinformationspanspan-idadditionalinformationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>追加情報

その他のメモリに関連するコマンドの説明とメモリの操作の概要については、次を参照してください。[読み取りと書き込みメモリ](reading-and-writing-memory.md)します。

<a name="remarks"></a>注釈
-------

表示される各の行の後にそのメモリの内容と次の場所の行で最初のバイトのアドレスが含まれます。

省略した場合*範囲*、最後の表示コマンドの終了位置から始まるメモリが表示されます。 これにより、継続的にメモリをスキャンすることができます。

このコマンドは、次の形式で存在します。 2 番目の文字、 **dd**、 **dD**、 **dw**、および**dW**コマンドは大文字/小文字、の3番目の文字として**dyb**と**dyd**コマンド。

|コマンド|ディスプレイ|
|--- |--- |
|d|これには、最新の d コマンドと同じ形式でデータが表示されます。 D の前のコマンドが実行されていない場合は d では db と同じ効果です。 D が d で開始しますが、最新のコマンドを繰り返すことを確認します。 これだけが含まれます dda には、ddp には、ddu には、dpa には、dpp には、dpu には、dqa には、dqp には、dqu には、dds には、dps には、dqs には、ds には、dS には、配布グループには、dl には、dt、および dv もこのページで、コマンドが表示します。 D の後に指定されたパラメーターが適切でないエラーが発生する可能性があります。|
|da|ASCII 文字。 各行には、48 文字までが表示されます。 表示には、最初の null バイトまで、または表示されている範囲内のすべての文字までが続きます。 キャリッジ リターンとライン フィードなどのすべての印刷できない文字がピリオド (.) として表示されます。|
|db|バイト値は、ASCII 文字。 最大 16 の 16 進のバイト値に続く各表示行の行で、最初のバイトのアドレスを示しています。 バイト値のすぐ後で、対応する ASCII 値。 8 番目、9 番目の 16 進値は、ハイフン (-) で区切られます。 キャリッジ リターンとライン フィードなどのすべての印刷できない文字がピリオド (.) として表示されます。 既定の数には、128 バイトです。|
|dc|ダブル ワード値 (4 バイト) は、ASCII 文字。 各表示行のアドレスを示しますの最初の単語の行で、最大 8 個の 16 進数の word 値と、ASCII と同じです。 既定の数は、32 の Dword (128 バイト) です。| 
|dd|ダブル ワード値 (4 バイト)。既定の数は、32 の Dword (128 バイト) です。|
|DD|倍精度浮動小数点数 (8 バイト)。 既定の数は、15 の数値 (120 バイト) です。|
|df|単精度浮動小数点数 (4 バイト)。 既定の数は、16 個 (64 バイト) です。|
|dp|ポインターのサイズの値。 このコマンドは、dd またはかどうか、ターゲット コンピューターのプロセッサ アーキテクチャがに応じて 32 ビットまたは 64 ビット、それぞれの dq と同じです。 既定の数は、32 の Dword または 16 のクアッド単語 (128 バイト) には。|
|dq|クワドワード値 (8 バイト)。 既定の数は、16 台のクアッド単語 (128 バイト) です。|
|du|Unicode 文字。 各行には、48 文字までが表示されます。 表示には、最初の null バイトまで、または表示されている範囲内のすべての文字までが続きます。 キャリッジ リターンとライン フィードなどのすべての印刷できない文字がピリオド (.) として表示されます。|
|dw|Word の値 (2 バイト)。 各表示行は、行では最大 8 個の 16 進数の word 値の最初の単語のアドレスを示します。 既定の数は、64 の単語 (128 バイト) です。|
|DW|ワード値 (2 バイト) は、ASCII 文字。 各表示行は、行では最大 8 個の 16 進数の word 値の最初の単語のアドレスを示します。 既定の数は、64 の単語 (128 バイト) です。|
|dyb|バイナリ値とバイト値。 既定の数は 32 バイトです。|
|dyd|バイナリ値とダブル ワード値 (4 バイト)。 既定の数は、8 Dword (32 バイト) です。|

 

疑問符 (?)、その内容が示すように、無効なアドレスを表示しようとした場合 (**?**)。

 

 





