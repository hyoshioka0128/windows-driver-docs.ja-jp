---
title: レジスタ
description: レジスタ
ms.assetid: fa334c9f-46c6-4288-95ce-43128fff7f03
keywords:
- メモリのアクセスを登録します
- レジスタ
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: 103c1fc3e2bb486d469d930ba645f9239b8cbf6b
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67366433"
---
# <a name="registers"></a>レジスタ


## <span id="ddk_registers_dbx"></span><span id="DDK_REGISTERS_DBX"></span>


[デバッガー エンジン](introduction.md#debugger-engine)を調べて、ターゲットのレジスタを変更するために使用できます。

ターゲットで使用可能なレジスタは、そのプロセッサ アーキテクチャに依存します。 X86、Itanium プロセッサのレジスタの説明は、次を参照してください。[プロセッサ アーキテクチャ](processor-architecture.md)します。 プロセッサの使用可能なレジスタの詳細については、そのプロセッサのマニュアルを参照してください。

### <a name="span-idtheregistersetspanspan-idtheregistersetspanthe-register-set"></a><span id="the_register_set"></span><span id="THE_REGISTER_SET"></span>登録セット

[ **GetNumberRegisters** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgeng/nf-dbgeng-idebugregisters2-getnumberregisters)メソッドは、ターゲット上のレジスタ番号を検索するために使用できます。

各レジスタは、そのインデックスを使用して参照されます。 最初のレジスタのインデックスは 0、および最後のレジスタのインデックスはレジスタから 1 を引いた数です。 既知の名前を持つ、レジスタのインデックスを検索する使用[ **GetIndexByName**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgeng/nf-dbgeng-idebugregisters2-getindexbyname)します。

メソッド[ **GetDescription** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgeng/nf-dbgeng-idebugregisters2-getdescription)レジスタに関する情報を返します。 登録の名前保持できる値の型にはが含まれます、subregister がかどうか。

A *subregister*が別のレジスタ内に含まれる登録します。 Subregister 変更、それを含んでいるレジスタも変更されたとき。 たとえば、x86 でプロセッサ、 **ax** subregister は 32 ビットの下位 16 ビットの場合と同じ**eax**を登録します。

これは、次の 3 つの特別なレジスタを次のメソッドを使用して値を持ついる可能性があります。 これらのレジスタの値の解釈は、プラットフォームに依存します。

-   現在の命令の場所にあります[ **GetInstructionOffset** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgeng/nf-dbgeng-idebugregisters2-getinstructionoffset)と[ **GetInstructionOffset2**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgeng/nf-dbgeng-idebugregisters2-getinstructionoffset2)します。

-   現在のプロセッサ スタック スロットの場所にあります[ **GetStackOffset** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgeng/nf-dbgeng-idebugregisters2-getstackoffset)と[ **GetStackOffset2**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgeng/nf-dbgeng-idebugregisters2-getstackoffset2)します。

-   現在の関数のスタック フレームの場所にあります[ **GetFrameOffset** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgeng/nf-dbgeng-idebugregisters2-getframeoffset)と[ **GetFrameOffset2**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgeng/nf-dbgeng-idebugregisters2-getframeoffset2)します。

### <a name="span-idmanipulatingregistersspanspan-idmanipulatingregistersspanmanipulating-registers"></a><span id="manipulating_registers"></span><span id="MANIPULATING_REGISTERS"></span>レジスタを操作します。

メソッドを使用して、レジスタの値が読み取れる[ **GetValue**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgeng/nf-dbgeng-idebugregisters2-getvalue)します。 使用して複数のレジスタが読み取れる[ **GetValues** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgeng/nf-dbgeng-idebugregisters2-getvalues)と[ **GetValues2**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgeng/nf-dbgeng-idebugregisters2-getvalues2)します。

メソッドを使用して、レジスタに値を書き込むことが[ **SetValue**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgeng/nf-dbgeng-idebugregisters2-setvalue)します。 使用して複数のレジスタが書き込む[ **SetValues** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgeng/nf-dbgeng-idebugregisters2-setvalues)と[ **SetValues2**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgeng/nf-dbgeng-idebugregisters2-setvalues2)します。

レジスタの型を別の型を指定した値がある場合は、レジスタに値を書き込むときに、値は、register の型に変換されます。 この変換は、メソッドによって実行されると同じ[ **CoerceValue**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgeng/nf-dbgeng-idebugcontrol3-coercevalue)します。 レジスタの型は、指定された値を保持することがない場合、この変換はデータが失われるあります。

### <a name="span-idpseudoregistersspanspan-idpseudoregistersspan-pseudo-registers"></a><span id="pseudo_registers"></span><span id="PSEUDO_REGISTERS"></span> 擬似レジスタ

*擬似レジスタ*デバッガー エンジンによって管理される、たとえば、特定の値を保持する変数 **$teb**擬似レジスタの値が現在のスレッドのスレッドの環境のアドレスの名前を指定しますブロック終了します。 詳細についてと擬似レジスタの一覧は、次を参照してください。[擬似レジスタ構文](pseudo-register-syntax.md)します。

各擬似レジスタには、インデックスがあります。 インデックスが 0 ~ 擬似レジスタの数の数値 (によって返される[ **GetNumberPseudoRegisters**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgeng/nf-dbgeng-idebugregisters2-getnumberpseudoregisters)) から 1 を引いたします。 その名前で擬似レジスタのインデックスを確認する[ **GetPseudoIndexByName**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgeng/nf-dbgeng-idebugregisters2-getpseudoindexbyname)します。 使用して擬似レジスタの値を読み取ることができます[ **GetPseudoValues**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgeng/nf-dbgeng-idebugregisters2-getpseudovalues)を使用して擬似レジスタに値を記述できますと[ **SetPseudoValues** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgeng/nf-dbgeng-idebugregisters2-setpseudovalues). については、その型を含む、擬似レジスタを使用して、 [ **GetPseudoDescription**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgeng/nf-dbgeng-idebugregisters2-getpseudodescription)します。

**注**  または特定のセッションで常にすべてのデバッグ セッションですべての擬似レジスタが使用可能な。

 

### <a name="span-iddisplayingregistersspanspan-iddisplayingregistersspandisplaying-registers"></a><span id="displaying_registers"></span><span id="DISPLAYING_REGISTERS"></span>レジスタを表示します。

メソッド[ **OutputRegisters** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgeng/nf-dbgeng-idebugregisters2-outputregisters)と[ **OutputRegisters2** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgeng/nf-dbgeng-idebugregisters2-outputregisters2)ターゲットを形式は、登録し、出力として、クライアントに送信します。

### <a name="span-ideventsspanspan-ideventsspanevents"></a><span id="events"></span><span id="EVENTS"></span>イベント

エンジンを呼び出すが、ターゲットのレジスタの値が変更されるたびに、 [ **IDebugEventCallbacks::ChangeDebuggeeState** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgeng/nf-dbgeng-idebugeventcallbacks-changedebuggeestate)コールバック メソッド、パラメーターを持つ*フラグ*デバッグ に設定\_CDS\_を登録します。

 

 





