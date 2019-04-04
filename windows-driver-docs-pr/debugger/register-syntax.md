---
title: 構文を登録します。
description: 構文を登録します。
ms.assetid: 64a566b1-c10b-4329-947c-af69904a21f8
keywords:
- 式、レジスタ
- レジスタ、コマンドの構文
- (プレフィックスを登録する)
- (登録プレフィックス) のコマンドの構文規則
- レジスタのコマンドの構文規則
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: 79b4dfeea0548d23d0ca17bb31850bbf35a22478
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56531822"
---
# <a name="register-syntax"></a>構文を登録します。


## <span id="ddk_register_syntax_dbg"></span><span id="DDK_REGISTER_SYNTAX_DBG"></span>


デバッガーには、レジスタ、および浮動小数点レジスタを制御できます。

追加する必要があります式でレジスタを使用すると、アット マーク ( **@** )、登録する前にします。 デバッガーを指示このアット マークと、次のテキストは、レジスタの名前であります。

MASM 式の構文を使用している場合は、省略、特定の非常に一般的な記号を登録します。 X86 ベースのシステムでは、省略することができます、アット マークの**eax**、 **ebx**、 **ecx**、 **edx**、 **esi**、 **edi**、 **ebp**、 **eip**、および**efl**を登録します。 ただし、あまり一般的なレジスタなしを指定する場合、アット マークは、デバッガーは、まず、テキストを 16 進数として解釈します。 テキストに 16 進数以外の文字が含まれている場合、デバッガーは、テキストを次に、シンボルとして解釈されます。 最後に、デバッガーがシンボルの一致を見つけられない場合、デバッガーはレジスタとして、テキストを解釈します。

C++ の式の構文を使用している場合、アット マークは必須では常にします。

[ **R (レジスタ)** ](r--registers-.md)コマンドは、この規則の例外。 デバッガーは常に、レジスタとして、最初の引数を解釈します。 (にサインインのために必要なまたは許可されていない)。2 番目の引数がある場合、 **r**コマンドで、既定の式の構文に従って解釈されます。 既定式の構文が C++ の場合は、コピーする次のコマンドを使用する必要があります、 **ebx**を登録、 **eax**を登録します。

```dbgcmd
0:000> r eax = @ebx
```

レジスタと各プロセッサに固有の手順の詳細については、[プロセッサ アーキテクチャ](processor-architecture.md)を参照してください。

### <a name="span-idflagsonanx86basedprocessorspanspan-idflagsonanx86basedprocessorspanflags-on-an-x86-based-processor"></a><span id="flags_on_an_x86_based_processor"></span><span id="FLAGS_ON_AN_X86_BASED_PROCESSOR"></span>X86 ベースのプロセッサのフラグ

x86 ベースのプロセッサが使用してもいくつかの 1 ビット レジスタと呼ばれる*フラグ*します。 これらのフラグとを表示または変更に使用できる構文の詳細については、[x86 フラグ](x86-architecture.md#x86-flags)を参照してください。

### <a name="span-idregistersandthreadsspanspan-idregistersandthreadsspanregisters-and-threads"></a><span id="registers_and_threads"></span><span id="REGISTERS_AND_THREADS"></span>レジスタとスレッド

各スレッドは、独自のレジスタの値を持っています。 これらの値は、別のスレッドを実行するときにメモリ内と、スレッドを実行するときに、CPU レジスタに格納されます。

ユーザー モードでは、レジスタへの参照は、現在のスレッドに関連付けられている登録として解釈されます。 現在のスレッドの詳細については、[を制御するプロセスとスレッド](controlling-processes-and-threads.md)を参照してください。

カーネル モードでは、レジスタへの参照が現在のレジスタのコンテキストに関連付けられている登録として解釈されます。 特定のスレッド、コンテキストのレコードを一致するように登録するコンテキストを設定したり、フレームをトラップします。 指定したコンテキストを登録すると、その値を変更することはできません、最も重要なレジスタのみを表示できます。

 

 





