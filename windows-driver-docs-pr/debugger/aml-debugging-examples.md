---
title: AML デバッグの例
description: AML デバッグの例
ms.assetid: 3a9f760f-f511-412f-aca0-3c415b3e5dc2
keywords:
- AMLI デバッガー、例のデバッグ
ms.date: 11/07/2018
ms.localizationpriority: medium
ms.openlocfilehash: e090547a65b599eb1f778d7a012f17a0b8ffd853
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56579808"
---
# <a name="aml-debugging-examples"></a>AML デバッグの例


## <span id="ddk_aml_debugging_examples_dbg"></span><span id="DDK_AML_DEBUGGING_EXAMPLES_DBG"></span>


AML を開始する方法を示す例をここではデバッグします。

### <a name="span-idinvestigatingafrozencomputerspanspan-idinvestigatingafrozencomputerspaninvestigating-a-frozen-computer"></a><span id="investigating_a_frozen_computer"></span><span id="INVESTIGATING_A_FROZEN_COMPUTER"></span>固定されたコンピューターの調査

使用して、ターゲット コンピューターが固定されており、ACPI の問題が可能性があると思われる場合の開始、 [ **! amli lc** ](-amli-lc.md)すべてのアクティブなコンテキストを表示する拡張機能。

```dbgcmd
kd> !amli lc
*Ctxt=ffffffff8128d000, ThID=ffffffff81277880, Flgs=----R----, pbOp=ffffffff8124206c, Obj=\_SB.PCI0.ISA0.FDC0._CRS
```

コンテキストが表示されない場合、エラーがない可能性があります ACPI に関連します。

コンテキストを示す場合は、1 つのアスタリスクでマークを探します。 これは、*現在のコンテキスト*(存在する時点で、インタープリターで実行されているもの)。

この例では、ターゲット コンピューターは 32 ビット プロセッサで Windows を実行します。 そのためのすべてのアドレスは、64 ビット、上位 32 ビットで贈答 FFFFFFFF の生成にキャストされます。 省略形**pbOp**命令ポインター (「ポインターを二項演算のコード」) を示します。 **Obj** ACPI テーブルに表示されるフィールドは、完全なパスと、メソッドの名前。 フラグの説明は、次を参照してください。 [ **! amli lc**](-amli-lc.md)します。

使用することができます、 [ **! amli u** ](-amli-u.md)逆アセンブルするコマンド、 \_CRS メソッドとして、次のとおりです。

```dbgcmd
kd> !amli u \_SB.PCI0.ISA0.FDC0._CRS

ffffffff80e4a535 : CreateDWordFieldCRES, 0x76, RAMT)
ffffffff80e4a540 : CreateDWordField(CRES, 0x82, PCIT)
ffffffff80e4a54b : Add(MLEN(), 0x100000, RAMT)
ffffffff80e4a559 : Subtract(0xffe00000, RAMT, PCIT)
ffffffff80e4a567 : Return(CRES)
```

### <a name="span-idbreakingintotheamlidebuggerspanspan-idbreakingintotheamlidebuggerspanbreaking-into-the-amli-debugger"></a><span id="breaking_into_the_amli_debugger"></span><span id="BREAKING_INTO_THE_AMLI_DEBUGGER"></span>AMLI デバッガーの中断

[ **! Amli デバッガー** ](-amli-debugger.md)コマンドは、任意の AML コードが実行される次回 AMLI デバッガーを中断する AML インタープリターを実行します。

AMLI デバッガー プロンプトが表示されます、AMLI デバッガー コマンドを使用することができます。 使用することも **! amli**でそれらをプレフィックスとしてせず拡張コマンド"! amli"。

```dbgcmd
kd> !amli debugger
kd> g

AMLI(? for help)-> find _crs
\_SB.LNKA._CRS
\_SB.LNKB._CRS
\_SB.LNKC._CRS
\_SB.LNKD._CRS
\_SB.PCI0._CRS
\_SB.PCI0.LPC.NCP._CRS
\_SB.PCI0.LPC.PIC._CRS
\_SB.PCI0.LPC.TIME._CRS
\_SB.PCI0.LPC.IDMA._CRS
\_SB.PCI0.LPC.RTC._CRS
\_SB.PCI0.LPC.SPKR._CRS
\_SB.PCI0.LPC.FHUB._CRS
\_SB.PCI0.SBD1._CRS
\_SB.PCI0.SBD2._CRS
\_SB.MBRD._CRS

AMLI(? for help)-> u \_SB.PCI0._CRS

ffffffff80e4a535 : CreateDWordFieldCRES, 0x76, RAMT)
ffffffff80e4a540 : CreateDWordField(CRES, 0x82, PCIT)
ffffffff80e4a54b : Add(MLEN(), 0x100000, RAMT)
ffffffff80e4a559 : Subtract(0xffe00000, RAMT, PCIT)
ffffffff80e4a567 : Return(CRES)
```

### <a name="span-idusingbreakpointsspanspan-idusingbreakpointsspanusing-breakpoints"></a><span id="using_breakpoints"></span><span id="USING_BREAKPOINTS"></span>ブレークポイントの使用

次の例では、メソッドの前に AMLI デバッガーに割り込むは\_BST を実行します。

検出された場合でも、 \_BST オブジェクト、メソッドが実際あることを確認する必要があります。 使用することができます、 [ **! amli dns** ](-amli-dns.md)これを行う拡張機能。

```dbgcmd
kd> !amli dns /s \_sb.pci0.isa.bat1._bst

ACPI Name Space: \_SB.PCI0.ISA.BAT1._BST (c29c2044)
Method(_BST:Flags=0x0,CodeBuff=c29c20a5,Len=103)
```

使用して、 [ **! amli bp** ](-amli-bp.md)ブレークポイントを配置するコマンド。

```dbgcmd
kd> !amli bp \_sb.pci0.isa.bat1._bst
```

メソッド内でブレークポイントを配置することもできます。 使用できます、 [ **! amli u** ](-amli-u.md)逆アセンブルするコマンド\_BST し、その手順のいずれかにブレークポイントを配置します。

```dbgcmd
kd> !amli u _sb.pci0.isa.bat1._bst

ffffffffc29c20a5: Acquire(\_SB_.PCI0.ISA_.EC0_.MUT1, 0xffff)
ffffffffc29c20c0: Store("CMBatt - _BST.BAT1", Debug)
ffffffffc29c20d7: \_SB_.PCI0.ISA_.EC0_.CPOL()
ffffffffc29c20ee: Release(\_SB_.PCI0.ISA_.EC0_.MUT1)
ffffffffc29c2107: Return(PBST)

kd> !amli bp c29c20ee
```

### <a name="span-idrespondingtoatriggeredbreakpointspanspan-idrespondingtoatriggeredbreakpointspanresponding-to-a-triggered-breakpoint"></a><span id="responding_to_a_triggered_breakpoint"></span><span id="RESPONDING_TO_A_TRIGGERED_BREAKPOINT"></span>トリガーされたブレークポイントへの応答

次の例では、メソッドで\_WAK が実行されていると、ブレークポイントに到達しました。

```dbgcmd
Running \_WAK method
Hit Breakpoint 0.
```

使用して、 [ **! amli ln** ](-amli-ln.md)拡張機能を現在のプログラム カウンターに最も近いメソッドを参照してください。 次の例には、32 ビット形式でアドレスを表示しています。

```dbgcmd
kd> !amli ln
c29accf5: \_WAK
```

[ **! Amli lc** ](-amli-lc.md)拡張機能は、すべてのアクティブなコンテキストを表示します。

```dbgcmd
kd> !amli lc
 Ctxt=c18b6000, ThID=00000000, Flgs=A-QC-W----, pbOp=c29bf8fe, Obj=\_SB.PCI0.ISA.EC0._Q09
*Ctxt=c18b4000, ThID=c15a6618, Flgs=----R-----, pbOp=c29accf5, Obj=\_WAK
```

アクティブなコンテキストをメソッドに関連付けられたことを示しますこの\_Q09 と\_WAK します。 現在のコンテキストが\_WAK します。

使用して、 [ **! amli r** ](-amli-r.md)コマンドの詳細については、現在のコンテキストを表示します。 スレッドとスタックの有用な情報とに渡される引数を表示するこの\_WAK とローカル データ オブジェクト。

```dbgcmd
kd> !amli r
Context=c18b4000*, Queue=00000000, ResList=00000000
ThreadID=c15a6618, Flags=00000010
StackTop=c18b5eec, UsedStackSize=276 bytes, FreeStackSize=7636 bytes
LocalHeap=c18b40c0, CurrentHeap=c18b40c0, UsedHeapSize=88 bytes
Object=\_WAK, Scope=\_WAK, ObjectOwner=c18b4108, SyncLevel=0
AsyncCallBack=ff06b5d0, CallBackData=0, CallBackContext=c99efddc

MethodObject=\_WAK
c18b40e4: Arg0=Integer(:Value=0x00000001[1])
c18b5f3c: Local0=Unknown()
c18b5f54: Local1=Unknown()
c18b5f6c: Local2=Unknown()
c18b5f84: Local3=Unknown()
c18b5f9c: Local4=Unknown()
c18b5fb4: Local5=Unknown()
c18b5fcc: Local6=Unknown()
c18b5fe4: Local7=Unknown()
c18b4040: RetObj=Unknown()
```

### <a name="span-idtracingsteppingandrunningamlcodespanspan-idtracingsteppingandrunningamlcodespantracing-stepping-and-running-aml-code"></a><span id="tracing__stepping__and_running_aml_code"></span><span id="TRACING__STEPPING__AND_RUNNING_AML_CODE"></span>トレース、ステップ実行、および AML コードを実行します。

コードをトレースする場合を使用して完全なトレース情報は有効にできます、 [ **! amli セット**](-amli-set.md)拡張機能として次のとおりです。

```dbgcmd
kd> !amli set spewon verboseon traceon
```

これでコードの実行が 1 行ずつの視聴、AML コード ステップできます。 **P**関数の呼び出し経由での手順をコマンドします。 **T**コマンドは関数呼び出しにステップ インします。

```dbgcmd
AMLI(? for help)-> p

c29bfcb7: Store(\_SB_.PCI0.ISA_.ACAD.CHAC(SEL0=0x10e1)
c29c17b1: {
c29c17b1: | Store(LGreater(And(Arg0=0x10e1,0xf0,)=0xe0,0x80)=0xffffffff,Local0)=0xffffffff

AMLI(? for help)-> p

c29c17bb: | If(LNot(LEqual(Local0=0xffffffff,ACP_=0xffffffff)=0xffffffff)=0x0)
c29c17ce: | {
c29c17ce: | | Return(Zero)
c29c17d0: | }
c29c17d0: },Local1)=0x0

AMLI(? for help)-> t

c29bfcd4: Store(\_SB_.PCI0.ISA_.BAT1.CHBP(SEL0=0x10e1)
c29c293d: {
c29c293d: | Store("CMBatt - CHBP.BAT1",Debug)String(:Str="CMBatt - CHBP.BAT1")="CMBatt - CHBP.BAT1"
```

選択した場合は、AMLI デバッガー内のメソッドを実行することも可能性があります。 たとえば、そのコントロールのメソッドを実行して LNKA デバイスの状態を評価する可能性があります\_STA:

```dbgcmd
AMLI(? for help)-> run \_sb.lnka._sta
PCI OpRegion Access on region c29b2268 device c29b2120

\_SB.LNKA._STA completed successfully with object data:
Integer(:Value=0x0000000b[11])
```

## <a name="see-also"></a>関連項目

 [AMLI デバッガー](the-amli-debugger.md)

 





