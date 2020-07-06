---
title: dds、dps、dqs (単語とシンボルの表示)
description: Dds、dps、および dqs の各コマンドは、指定された範囲のメモリの内容を表示します。 このメモリは、シンボルテーブルの一連のアドレスとして扱われます。
ms.assetid: 5a3ed1c4-723a-4902-bfbf-d4a44d2cd0b5
keywords:
- dds、dps、dqs (単語とシンボルの表示) Windows デバッグ
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- dds, dps, dqs (Display Words and Symbols)
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: f1c192dde25bfeb2fa8485d3d87dc821dae6666b
ms.sourcegitcommit: ca5045a739eefd6ed14b9dbd9249b335e090c4e9
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/06/2020
ms.locfileid: "85968023"
---
# <a name="dds-dps-dqs-display-words-and-symbols"></a>dds、dps、dqs (単語とシンボルの表示)


**Dds**、 **dps**、および**dqs**の各コマンドは、指定された範囲のメモリの内容を表示します。 このメモリは、シンボルテーブルの一連のアドレスとして扱われます。 対応するシンボルも表示されます。

```dbgcmd
dds [Options] [Range] 
dqs [Options] [Range] 
dps [Options] [Range] 
```

## <a name="span-idddk_cmd_display_words_and_symbols_dbgspanspan-idddk_cmd_display_words_and_symbols_dbgspanparameters"></a><span id="ddk_cmd_display_words_and_symbols_dbg"></span><span id="DDK_CMD_DISPLAY_WORDS_AND_SYMBOLS_DBG"></span>パラメータ


<span id="_______Options______"></span><span id="_______options______"></span><span id="_______OPTIONS______"></span>*オプション*   
1つ以上の表示オプションを指定します。 次のオプションのいずれかを含めることができます。ただし、1つの **/p**オプションを指定することはできません \* 。

<span id="_c_Width"></span><span id="_c_width"></span><span id="_C_WIDTH"></span>**/c** *幅*  
表示に使用する列の数を指定します。 これを省略した場合、既定の列数は表示の種類によって異なります。 これらのコマンドによってシンボルが表示される方法があるため、通常は、1つのデータ列のみの既定値を使用することをお勧めします。

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

**Dds**の2番目の文字では、大文字と小文字が区別されます。 これらのコマンドの3番目の文字では、大文字と小文字が区別されます。

**Dds**コマンドでは、 [**dd**](d--da--db--dc--dd--dd--df--dp--dq--du--dw--dw--dyb--dyd--display-memor.md)コマンドのような2つの単語 (4 バイト) の値が表示されます。 **Dqs**コマンドを実行すると、 **dq**コマンドのように、クワッドワード (8 バイト) の値が表示されます。 **Dps**コマンドは、 **dp**コマンドのように、ポインターサイズの値 (ターゲットコンピューターのアーキテクチャによっては4バイトまたは8バイト) を表示します。

これらの各単語は、シンボルテーブルのアドレスとして扱われます。 各単語に対応するシンボル情報が表示されます。

行番号情報が有効になっている場合は、ソースファイル名と行番号が使用可能なときに表示されます。

 

 





