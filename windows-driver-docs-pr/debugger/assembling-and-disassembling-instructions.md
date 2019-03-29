---
title: アセンブルと逆アセンブルの手順
description: アセンブルと逆アセンブルの手順
ms.assetid: 7681bea1-4d4e-4260-950d-69cb8feb3807
keywords:
- デバッガー エンジン API をアセンブルおよび逆アセンブル
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: e305e84f3643efb85643d81bd006b432d9ab09fd
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56577990"
---
# <a name="assembling-and-disassembling-instructions"></a>アセンブルと逆アセンブルの手順


デバッガー エンジンでは、表示すると、ターゲットでコードを変更するアセンブリ言語の使用をサポートしています。 デバッガーでのアセンブリ言語の使用の概要については、次を参照してください。[モードのアセンブリでのデバッグ](debugging-in-assembly-mode.md)します。

**注**  アーキテクチャはすべてのアセンブリ言語がサポートされていません。 いくつかのアーキテクチャのすべての命令がサポートされています。

 

1 つのアセンブリ言語命令をアセンブルし、ターゲットのメモリに結果として得られるプロセッサ命令を配置、使用[**アセンブル**](https://msdn.microsoft.com/library/windows/hardware/ff538121)します。

1 つの命令を逆アセンブルをターゲットからプロセッサ命令を取得し、アセンブリ命令を表す文字列を生成するには、使用[**逆アセンブル**](https://msdn.microsoft.com/library/windows/hardware/ff541948)します。

メソッド[ **GetDisassembleEffectiveOffset** ](https://msdn.microsoft.com/library/windows/hardware/ff546581)逆アセンブルする最後の命令の最初の有効なアドレスを返します。 たとえば、逆アセンブルする最後の命令が`move ax, [ebp+4]`、有効なアドレスの値である`ebp+4`します。 これに対応して、 **$ea**擬似レジスタ。

出力のコールバックに逆アセンブルした指示を送信するメソッドを使用して、 [ *OutputDisassembly* ](https://msdn.microsoft.com/library/windows/hardware/ff553211)と[ *OutputDisassemblyLines* ](https://msdn.microsoft.com/library/windows/hardware/ff553216).

デバッガー エンジンでは、アセンブリとの逆アセンブルを制御するいくつかのオプションがあります。 これらのオプションがによって返される[ **GetAssemblyOptions**](https://msdn.microsoft.com/library/windows/hardware/ff545605)します。 使用して設定できる[ **SetAssemblyOptions** ](https://msdn.microsoft.com/library/windows/hardware/ff556626)いくつかのオプションをオンにし[ **AddAssemblyOptions** ](https://msdn.microsoft.com/library/windows/hardware/ff537852)またはをオフになっています[**RemoveAssemblyOptions**](https://msdn.microsoft.com/library/windows/hardware/ff554483)します。

 

 





