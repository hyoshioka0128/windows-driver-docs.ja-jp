---
title: dds、dp、dqs (表示語およびシンボル)
description: Dds、dp、および dqs のコマンドは、特定の範囲内でメモリの内容を表示します。 このメモリは、一連のシンボル テーブル内のアドレスと見なされます。
ms.assetid: 5a3ed1c4-723a-4902-bfbf-d4a44d2cd0b5
keywords:
- dds、dp、dqs (表示語およびシンボル) Windows のデバッグ
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- dds, dps, dqs (Display Words and Symbols)
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 3e6754c4089f04672bfae8b65825e4a8923ab5b6
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56529393"
---
# <a name="dds-dps-dqs-display-words-and-symbols"></a>dds、dp、dqs (表示語およびシンボル)


**Dds**、 **dps**、および**dqs**コマンドは、特定の範囲内でメモリの内容を表示します。 このメモリは、一連のシンボル テーブル内のアドレスと見なされます。 対応するシンボルがも表示されます。

```dbgcmd
dds [Options] [Range] 
dqs [Options] [Range] 
dps [Options] [Range] 
```

## <a name="span-idddkcmddisplaywordsandsymbolsdbgspanspan-idddkcmddisplaywordsandsymbolsdbgspanparameters"></a><span id="ddk_cmd_display_words_and_symbols_dbg"></span><span id="DDK_CMD_DISPLAY_WORDS_AND_SYMBOLS_DBG"></span>パラメーター


<span id="_______Options______"></span><span id="_______options______"></span><span id="_______OPTIONS______"></span> *オプション*   
1 つまたは複数の表示オプションを指定します。 次のオプションを含めることができ個を超える 1 つを除く **/p** \*オプションを示すことができます。

<span id="_c_Width"></span><span id="_c_width"></span><span id="_C_WIDTH"></span>**/c** *幅*  
表示に使用する列の数を指定します。 これを省略すると、既定の列数は、表示の種類によって異なります。 シンボルは、これらのコマンドで表示されるため、1 つのデータ列の既定値を使用することをお勧めします。

<span id="_p"></span><span id="_P"></span>**/p**  
(カーネル モードのみ)表示の物理メモリ アドレスを使用します。 指定された範囲*範囲*は仮想メモリではなく、物理メモリから取得されます。

<span id="_p_c_"></span><span id="_P_C_"></span>**/p\[c\]**  
(カーネル モードのみ)同じ **/p**, キャッシュ メモリが読み取られる点が異なります。 かっこ、 **c**含める必要があります。

<span id="_p_uc_"></span><span id="_P_UC_"></span>**/p\[uc\]**  
(カーネル モードのみ)同じ **/p**, キャッシュされていないメモリが読み取られる点が異なります。 かっこ、 **uc**含める必要があります。

<span id="_p_wc_"></span><span id="_P_WC_"></span>**/p\[wc\]**  
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

2 番目の文字の**dds**小文字が区別されます。 これらすべてのコマンドの 3 番目の文字が大文字小文字を区別します。

**Dds**コマンドのようにダブル ワード (4 バイト) の値が表示されます、 [ **dd** ](d--da--db--dc--dd--dd--df--dp--dq--du--dw--dw--dyb--dyd--display-memor.md)コマンド。 **Dqs**などクワドワード (8 バイト) の値を表示、 **dq**コマンド。 **Dps**コマンドのようなポインター サイズの値 (4 バイトまたは 8 バイトは、ターゲット コンピューターのアーキテクチャに応じて) が表示されます、 **dp**コマンド。

これらの単語のそれぞれは、シンボル テーブル内のアドレスとして扱われます。 各単語に対応するシンボル情報が表示されます。

行番号情報が有効にされている場合は、ソース ファイル名や行番号が表示されます使用可能な場合。

 

 





