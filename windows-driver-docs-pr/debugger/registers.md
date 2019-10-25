---
title: レジスタ
description: レジスタ
ms.assetid: fa334c9f-46c6-4288-95ce-43128fff7f03
keywords:
- メモリアクセス、レジスタ
- register
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3de47f38e5f6a56b69876c2191e07bc1513d61b6
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72834287"
---
# <a name="registers"></a>レジスタ


## <span id="ddk_registers_dbx"></span><span id="DDK_REGISTERS_DBX"></span>


[デバッガーエンジン](introduction.md#debugger-engine)を使用して、ターゲットのレジスタを確認および変更できます。

ターゲットで使用できるレジスタは、プロセッサのアーキテクチャによって異なります。 X86 および Itanium プロセッサのレジスタの詳細については、「[プロセッサアーキテクチャ](processor-architecture.md)」を参照してください。 プロセッサで使用できるレジスタの詳細については、そのプロセッサのドキュメントを参照してください。

### <a name="span-idthe_register_setspanspan-idthe_register_setspanthe-register-set"></a><span id="the_register_set"></span><span id="THE_REGISTER_SET"></span>レジスタセット

[**Getnumber register**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-idebugregisters2-getnumberregisters)メソッドを使用して、ターゲット上のレジスタの数を調べることができます。

各レジスタは、そのインデックスによって参照されます。 最初のレジスタのインデックスは0で、最後のレジスタのインデックスはレジスタの数から1を引いた数になります。 名前がわかっているレジスタのインデックスを検索するには、 [**GetIndexByName**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-idebugregisters2-getindexbyname)を使用します。

[**Getdescription**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-idebugregisters2-getdescription)メソッドは、レジスタに関する情報を返します。 これには、レジスタの名前、保持できる値の型、およびサブレジスタであるかどうかが含まれます。

*Subregister*は、別のレジスタ内に含まれるレジスタです。 サブレジスタが変更されると、それを含むレジスタも変更されます。 たとえば、x86 プロセッサでは、 **ax**サブレジスタは32ビットの**eax**レジスタの下位16ビットと同じです。

次のメソッドを使用して、値が見つかった3つの特殊なレジスタがあります。 これらのレジスタの値の解釈は、プラットフォームに依存します。

-   現在の命令の場所には、 [**GetInstructionOffset**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-idebugregisters2-getinstructionoffset)と[**GetInstructionOffset2**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-idebugregisters2-getinstructionoffset2)が含まれている場合があります。

-   現在のプロセッサスタックスロットの場所は、 [**Getstackoffset**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-idebugregisters2-getstackoffset)と[**GetStackOffset2**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-idebugregisters2-getstackoffset2)を使用して見つけることができます。

-   現在の関数のスタックフレームの位置は、 [**getframe offset**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-idebugregisters2-getframeoffset)と[**GetFrameOffset2**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-idebugregisters2-getframeoffset2)を使用して見つけることができます。

### <a name="span-idmanipulating_registersspanspan-idmanipulating_registersspanmanipulating-registers"></a><span id="manipulating_registers"></span><span id="MANIPULATING_REGISTERS"></span>操作 (レジスタを)

レジスタの値は、 [**GetValue**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-idebugregisters2-getvalue)メソッドを使用して読み取ることができます。 [**GetValues**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-idebugregisters2-getvalues)と[**GetValues2**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-idebugregisters2-getvalues2)を使用すると、複数のレジスタを読み取ることができます。

値は、 [**SetValue**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-idebugregisters2-setvalue)メソッドを使用してレジスタに書き込むことができます。 [**Setvalues**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-idebugregisters2-setvalues)と[**SetValues2**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-idebugregisters2-setvalues2)を使用して、複数のレジスタを書き込むことができます。

レジスタに値を書き込むときに、指定した値の型がレジスタの型と異なる場合は、その値がレジスタの型に変換されます。 この変換は、メソッド[**CoerceValue**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-idebugcontrol3-coercevalue)によって実行されるものと同じです。 レジスタの型が指定された値を保持できない場合、この変換によってデータが失われる可能性があります。

### <a name="span-idpseudo_registersspanspan-idpseudo_registersspan-pseudo-registers"></a><span id="pseudo_registers"></span><span id="PSEUDO_REGISTERS"></span>擬似レジスタ

*擬似レジスタ*は、特定の値を保持するデバッガーエンジンによって管理される変数です。たとえば、 **$teb**は、現在のスレッドのスレッド環境ブロック (teb) のアドレスを値とする擬似レジスタの名前です。 詳細と擬似レジスタの一覧については、「[擬似レジスタの構文](pseudo-register-syntax.md)」を参照してください。

各擬似レジスタにはインデックスがあります。 インデックスは、0から ( [**GetNumberPseudoRegisters**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-idebugregisters2-getnumberpseudoregisters)によって返される) 擬似レジスタの数から1を引いた数までの数値です。 名前によって疑似レジスタのインデックスを検索するには、 [**GetPseudoIndexByName**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-idebugregisters2-getpseudoindexbyname)を使用します。 擬似レジスタの値は[**Get擬似値**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-idebugregisters2-getpseudovalues)を使用して読み取ることができ、値は[**set擬似値**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-idebugregisters2-setpseudovalues)を使用して擬似レジスタに書き込むことができます。 擬似レジスタの種類などの詳細については、「 [**Get擬似説明**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-idebugregisters2-getpseudodescription)」を使用してください。

すべてのデバッグセッションまたは特定のセッションですべての擬似レジスタが使用できるとは限りませ**ん  。**

 

### <a name="span-iddisplaying_registersspanspan-iddisplaying_registersspandisplaying-registers"></a><span id="displaying_registers"></span><span id="DISPLAYING_REGISTERS"></span>表示 (レジスタを)

メソッド[**Outputregisters**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-idebugregisters2-outputregisters)と[**OutputRegisters2**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-idebugregisters2-outputregisters2)は、ターゲットのレジスタを書式設定し、出力としてクライアントに送信します。

### <a name="span-ideventsspanspan-ideventsspanevents"></a><span id="events"></span><span id="EVENTS"></span>記録

ターゲットのレジスタの値が変更されるたびに、エンジンは[**IDebugEventCallbacks:: ChangeDebuggeeState**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-idebugeventcallbacks-changedebuggeestate)コールバックメソッドを呼び出します。パラメーター*フラグ*を設定して\_CD\_レジスタにデバッグします。

 

 





