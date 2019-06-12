---
title: dda、ddp、ddu、dpa、dpp、dpu、dqa、dqp、dqu (参照メモリの表示)
description: Dda、ddp、ddu、dpa、dpp、dpu、dqa、dqp、および dqu コマンド指定した位置にポインターを表示、そのポインターを逆参照および関連付けられているメモリを表示します。
ms.assetid: af3db4e2-e3fc-4c4d-9432-13b87e699716
keywords:
- dda、ddp、ddu、dpa、dpp、dpu、dqa、dqp、dqu (参照されているメモリを表示する) Windows のデバッグ
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- dda, ddp, ddu, dpa, dpp, dpu, dqa, dqp, dqu (Display Referenced Memory)
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 0141024d6efe46fce102f7880ea94f5026e8be4a
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63374916"
---
# <a name="dda-ddp-ddu-dpa-dpp-dpu-dqa-dqp-dqu-display-referenced-memory"></a>dda、ddp、ddu、dpa、dpp、dpu、dqa、dqp、dqu (参照メモリの表示)


**Dda**、 **ddp**、 **ddu**、 **dpa**、 **dpp**、 **dpu**、 **dqa**、 **dqp**、および**dqu**コマンドは、指定した位置にポインターを表示し、そのポインターを逆参照し、メモリをその結果を表示さまざまな形式での場所です。

```dbgcmd
ddp [Options] [Range] 
dqp [Options] [Range] 
dpp [Options] [Range] 
dda [Options] [Range] 
dqa [Options] [Range] 
dpa [Options] [Range] 
ddu [Options] [Range] 
dqu [Options] [Range] 
dpu [Options] [Range]
```

## <a name="span-idddkcmddisplayreferencedmemorydbgspanspan-idddkcmddisplayreferencedmemorydbgspanparameters"></a><span id="ddk_cmd_display_referenced_memory_dbg"></span><span id="DDK_CMD_DISPLAY_REFERENCED_MEMORY_DBG"></span>パラメーター


<span id="_______Options______"></span><span id="_______options______"></span><span id="_______OPTIONS______"></span> *オプション*   
1 つまたは複数の表示オプションを指定します。 次のオプションを含めることができ個を超える 1 つを除く **/p** \*オプションを示すことができます。

<span id="_cWidth"></span><span id="_cwidth"></span><span id="_CWIDTH"></span>* */c***Width*  
表示に使用する列の数を指定します。 これを省略すると、既定の列数は、表示の種類によって異なります。 ポインターは、これらのコマンドで表示されるため、1 つのデータ列の既定値を使用することをお勧めします。

<span id="_p"></span><span id="_P"></span> **/p**  
(カーネル モードのみ)表示の物理メモリ アドレスを使用します。 指定された範囲*範囲*は仮想メモリではなく、物理メモリから取得されます。

<span id="_p_c_"></span><span id="_P_C_"></span> **/p\[c\]**  
(カーネル モードのみ)同じ **/p**, キャッシュ メモリが読み取られる点が異なります。 かっこ、 **c**含める必要があります。

<span id="_p_uc_"></span><span id="_P_UC_"></span> **/p\[uc\]**  
(カーネル モードのみ)同じ **/p**, キャッシュされていないメモリが読み取られる点が異なります。 かっこ、 **uc**含める必要があります。

<span id="_p_wc_"></span><span id="_P_WC_"></span> **/p\[wc\]**  
(カーネル モードのみ)同じ **/p**, 書き込み結合のメモリが読み取られる点が異なります。 かっこ、 **wc**含める必要があります。

<span id="_______Range______"></span><span id="_______range______"></span><span id="_______RANGE______"></span> *範囲*   
表示するメモリ領域を指定します。 構文の詳細については、次を参照してください。[アドレスとアドレス範囲の構文](address-and-address-range-syntax.md)します。 省略した場合*範囲*、最後の表示コマンドの終了位置から始まるメモリが表示されます。 場合*範囲*省略してない前の表示は、コマンドが使用されている、現在の命令ポインターで、表示が開始されます。 単純なアドレスを指定すると、既定値の範囲の長さは 128 バイトになります。

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

このコマンドの 2 番目と 3 番目の文字は大文字小文字を区別します。

このコマンドの 2 番目の文字は、ポインターを決定します。 使用するサイズ。

|コマンド|ディスプレイ|
|--- |--- |
|dd|32 ビット ポインターの使用|
|dq|64 ビット ポインターの使用|
|dp*|使用される標準的なポインター サイズ:32 ビットまたは 64 ビット ターゲットのプロセッサ アーキテクチャに応じた|

 

このコマンドの 3 番目の文字は、逆参照されるメモリを表示する方法を決定します。

|コマンド|ディスプレイ|
|--- |--- |
|dp|ターゲットのプロセッサ アーキテクチャのポインターのサイズに応じて、QWORD の DWORD またはこれの形式でポインターによって参照されるメモリの内容を表示します。 この値には、任意の既知の記号が一致するもこのシンボルが表示されます。|
|da|ASCII 文字の形式でポインターによって参照されるメモリの内容を表示します。|
|d * u|Unicode 文字形式のポインターが参照されているメモリの内容を表示します。|

 

行番号情報が有効にされている場合は、ソース ファイル名や行番号が表示されます使用可能な場合。

 

 





