---
title: アセンブルと逆アセンブルの手順
description: アセンブルと逆アセンブルの手順
ms.assetid: 7681bea1-4d4e-4260-950d-69cb8feb3807
keywords:
- デバッガー エンジン API をアセンブルおよび逆アセンブル
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: 41e1a129bf10e9496a91e83266d14ff6cae4f828
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67362408"
---
# <a name="assembling-and-disassembling-instructions"></a>アセンブルと逆アセンブルの手順


デバッガー エンジンでは、表示すると、ターゲットでコードを変更するアセンブリ言語の使用をサポートしています。 デバッガーでのアセンブリ言語の使用の概要については、次を参照してください。[モードのアセンブリでのデバッグ](debugging-in-assembly-mode.md)します。

**注**  アーキテクチャはすべてのアセンブリ言語がサポートされていません。 いくつかのアーキテクチャのすべての命令がサポートされています。

 

1 つのアセンブリ言語命令をアセンブルし、ターゲットのメモリに結果として得られるプロセッサ命令を配置、使用[**アセンブル**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgeng/nf-dbgeng-idebugcontrol3-assemble)します。

1 つの命令を逆アセンブルをターゲットからプロセッサ命令を取得し、アセンブリ命令を表す文字列を生成するには、使用[**逆アセンブル**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgeng/nf-dbgeng-idebugcontrol3-disassemble)します。

メソッド[ **GetDisassembleEffectiveOffset** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgeng/nf-dbgeng-idebugcontrol3-getdisassembleeffectiveoffset)逆アセンブルする最後の命令の最初の有効なアドレスを返します。 たとえば、逆アセンブルする最後の命令が`move ax, [ebp+4]`、有効なアドレスの値である`ebp+4`します。 これに対応して、 **$ea**擬似レジスタ。

出力のコールバックに逆アセンブルした指示を送信するメソッドを使用して、 [ *OutputDisassembly* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgeng/nf-dbgeng-idebugcontrol3-outputdisassembly)と[ *OutputDisassemblyLines* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgeng/nf-dbgeng-idebugcontrol3-outputdisassemblylines).

デバッガー エンジンでは、アセンブリとの逆アセンブルを制御するいくつかのオプションがあります。 これらのオプションがによって返される[ **GetAssemblyOptions**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgeng/nf-dbgeng-idebugcontrol3-getassemblyoptions)します。 使用して設定できる[ **SetAssemblyOptions** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgeng/nf-dbgeng-idebugcontrol3-setassemblyoptions)いくつかのオプションをオンにし[ **AddAssemblyOptions** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgeng/nf-dbgeng-idebugcontrol3-addassemblyoptions)またはをオフになっています[**RemoveAssemblyOptions**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgeng/nf-dbgeng-idebugcontrol3-removeassemblyoptions)します。

 

 





