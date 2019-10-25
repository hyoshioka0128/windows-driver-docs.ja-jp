---
title: アセンブルと逆アセンブルの手順
description: アセンブルと逆アセンブルの手順
ms.assetid: 7681bea1-4d4e-4260-950d-69cb8feb3807
keywords:
- デバッガーエンジン API, アセンブルと逆アセンブル
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: 24e64983fdcbb1e1a2b7840a3f78920cdf5c9033
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72837639"
---
# <a name="assembling-and-disassembling-instructions"></a>アセンブルと逆アセンブルの手順


デバッガーエンジンでは、ターゲットでコードを表示および変更するためのアセンブリ言語の使用がサポートされています。 デバッガーでのアセンブリ言語の使用の概要については、「[アセンブリモードでのデバッグ](debugging-in-assembly-mode.md)」を参照してください。

**注**   アセンブリ言語は、すべてのアーキテクチャでサポートされているわけではありません。 一部のアーキテクチャでは、一部の命令がサポートされていません。

 

単一のアセンブリ言語命令をアセンブルし、結果のプロセッサ命令をターゲットのメモリに配置するには、[**アセンブル**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-idebugcontrol3-assemble)を使用します。

ターゲットからプロセッサ命令を取得し、アセンブリ命令を表す文字列を生成することによって1つの命令を逆アセンブルするには、[**逆アセンブル**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-idebugcontrol3-disassemble)を使用します。

[**GetDisassembleEffectiveOffset**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-idebugcontrol3-getdisassembleeffectiveoffset)メソッドは、逆アセンブルする最後の命令の最初の有効なアドレスを返します。 たとえば、逆アセンブルする最後の命令が `move ax, [ebp+4]`場合、有効なアドレスは `ebp+4`の値になります。 これは **$ea**擬似レジスタに相当します。

逆アセンブルされた命令を出力コールバックに送信するには、 [*Outputdisassembly アセンブル*](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-idebugcontrol3-outputdisassembly)と[*Outputdisassemblylines*](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-idebugcontrol3-outputdisassemblylines)メソッドを使用します。

デバッガーエンジンには、アセンブリと逆アセンブリを制御するオプションがいくつかあります。 これらのオプションは、 [**GetAssemblyOptions**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-idebugcontrol3-getassemblyoptions)によって返されます。 これらは[**Setassemblyoptions**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-idebugcontrol3-setassemblyoptions)を使用して設定できます。また、一部のオプションは、 [**addassemblyoptions**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-idebugcontrol3-addassemblyoptions)で有効にすることも、 [**removeassemblyoptions**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-idebugcontrol3-removeassemblyoptions)で無効にすることもできます。

 

 





