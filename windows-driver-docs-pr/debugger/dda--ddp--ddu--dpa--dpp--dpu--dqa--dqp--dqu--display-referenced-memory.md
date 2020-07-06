---
title: dda、ddp、ddu、dpa、dpp、dpu、dqa、dqp、dqu (参照メモリの表示)
description: Dda、ddp、ddu、dpa、ddu、ddu、ddu、ddu、および dqu コマンドは、指定された場所にポインターを表示し、そのポインターを逆参照して、関連付けられているメモリを表示します。
ms.assetid: af3db4e2-e3fc-4c4d-9432-13b87e699716
keywords:
- dda、ddp、ddu、dpa、ddu、ddu、ddu、ddu、dqu (参照されるメモリの表示) Windows デバッグ
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- dda, ddp, ddu, dpa, dpp, dpu, dqa, dqp, dqu (Display Referenced Memory)
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: fd063895872486fdd9b0837556f3845970382752
ms.sourcegitcommit: ca5045a739eefd6ed14b9dbd9249b335e090c4e9
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/06/2020
ms.locfileid: "85968025"
---
# <a name="dda-ddp-ddu-dpa-dpp-dpu-dqa-dqp-dqu-display-referenced-memory"></a>dda、ddp、ddu、dpa、dpp、dpu、dqa、dqp、dqu (参照メモリの表示)


**Dda**、 **ddp**、 **ddu**、 **dpa**、 **ddu**、 **ddu**、 **ddu**、 **ddu**、および**dqu**の各コマンドは、指定された場所にポインターを表示し、そのポインターを逆参照して、結果の場所にさまざまな形式でメモリを表示します。

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

## <a name="span-idddk_cmd_display_referenced_memory_dbgspanspan-idddk_cmd_display_referenced_memory_dbgspanparameters"></a><span id="ddk_cmd_display_referenced_memory_dbg"></span><span id="DDK_CMD_DISPLAY_REFERENCED_MEMORY_DBG"></span>パラメータ


<span id="_______Options______"></span><span id="_______options______"></span><span id="_______OPTIONS______"></span>*オプション*   
1つ以上の表示オプションを指定します。 次のオプションのいずれかを含めることができます。ただし、1つの **/p**オプションを指定することはできません \* 。

<span id="_cWidth"></span><span id="_cwidth"></span><span id="_CWIDTH"></span>**/c**_幅_  
表示に使用する列の数を指定します。 これを省略した場合、既定の列数は表示の種類によって異なります。 これらのコマンドによってポインターが表示される方法があるため、通常は、1つのデータ列のみの既定値を使用することをお勧めします。

<span id="_p"></span><span id="_P"></span>**/p**  
(カーネルモードのみ)ディスプレイの物理メモリアドレスを使用します。 *範囲*で指定された範囲は、仮想メモリではなく物理メモリから取得されます。

<span id="_p_c_"></span><span id="_P_C_"></span>**/p \[ c\]**  
(カーネルモードのみ)**/P**と同じですが、キャッシュされたメモリが読み取られる点が異なります。 **C**を囲む角かっこを含める必要があります。

<span id="_p_uc_"></span><span id="_P_UC_"></span>**/p \[ uc\]**  
(カーネルモードのみ)**/P**と同じですが、キャッシュされていないメモリが読み取られる点が異なります。 **Uc**を囲む角かっこを含める必要があります。

<span id="_p_wc_"></span><span id="_P_WC_"></span>**/p \[ wc\]**  
(カーネルモードのみ)書き込み結合メモリが読み込まれる点を除いて、 **/p**と同じです。 **Wc**を囲む角かっこを含める必要があります。

<span id="_______Range______"></span><span id="_______range______"></span><span id="_______RANGE______"></span>*範囲*   
表示するメモリ領域を指定します。 構文の詳細については、「[アドレスとアドレス範囲の構文](address-and-address-range-syntax.md)」を参照してください。 *Range*を省略した場合、コマンドは最後の display コマンドの終了位置からメモリを表示します。 *Range*が省略されていて、前の表示コマンドが使用されていない場合は、現在の命令ポインターから表示が開始されます。 単純なアドレスを指定した場合、既定の範囲の長さは128バイトになります。

### <a name="span-idenvironmentspanspan-idenvironmentspanspan-idenvironmentspanenvironment"></a><span id="Environment"></span><span id="environment"></span><span id="ENVIRONMENT"></span>Environment

**モード**: ユーザーモード、カーネルモード

**ターゲット**: ライブ、クラッシュダンプ

**プラットフォーム**: すべて

 

### <a name="span-idadditional_informationspanspan-idadditional_informationspanspan-idadditional_informationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>追加情報

メモリ操作の概要とその他のメモリ関連コマンドの説明については、「[メモリの読み取りと書き込み](reading-and-writing-memory.md)」を参照してください。

<a name="remarks"></a>注釈
-------

このコマンドの2番目と3番目の文字では、大文字と小文字が区別されます。

このコマンドの2番目の文字は、使用されるポインターのサイズを決定します。

|コマンド|ディスプレイ|
|--- |--- |
|dd|32-ビットポインターが使用されています|
|dq|64-ビットポインターが使用されています|
|dp|使用される標準ポインターのサイズ:32 ビットまたは64ビット。ターゲットのプロセッサアーキテクチャによって異なります。|

 

このコマンドの3番目の文字は、逆参照メモリの表示方法を決定します。

|コマンド|ディスプレイ|
|--- |--- |
|dp|ターゲットのプロセッサアーキテクチャのポインターサイズに応じて、ポインターによって参照されるメモリの内容を DWORD または QWORD 形式で表示します。 この値が既知のシンボルと一致する場合は、この記号も表示されます。|
|da|ポインターによって参照されるメモリの内容を ASCII 文字形式で表示します。|
|d * u|ポインターによって参照されるメモリの内容を Unicode 文字形式で表示します。|

 

行番号情報が有効になっている場合は、ソースファイル名と行番号が使用可能なときに表示されます。

 

 





