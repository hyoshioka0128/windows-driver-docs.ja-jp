---
title: WdbgExts のシンボル
description: WdbgExts のシンボル
ms.assetid: 7e1a1799-b87c-42cb-94ce-fbdc9a5ec973
keywords:
- シンボル、WdbgExts 拡張機能
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: e84d2f0573ab54d8a46e22484acc7ce742fd513d
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63325836"
---
# <a name="wdbgexts-symbols"></a>WdbgExts のシンボル


このトピックではシンボルをする方法の概要、WdbgExts API を使用して操作します。 内のシンボルを使用しての概要については、[デバッガー エンジン](introduction.md#debugger-engine)を参照してください[シンボル](symbols.md)で、[デバッガー エンジンの概要](debugger-engine-overview.md)このドキュメントの「します。

MASM または C++ の式を評価する関数を使用して[ **GetExpression** ](https://msdn.microsoft.com/library/windows/hardware/ff546683)または[ **GetExpressionEx**](https://msdn.microsoft.com/library/windows/hardware/ff546691)します。

構造体のメンバーの値を読み取り、使用、 [ **GetFieldData** ](https://msdn.microsoft.com/library/windows/hardware/ff546743)関数、またはの場合、メンバーには、プリミティブ型の値が含まれています[ **GetFieldValue** 。](https://msdn.microsoft.com/library/windows/hardware/ff546781)ことができます。 ターゲットのメモリ内のシンボルのインスタンスのサイズを調べるには、 [ **GetTypeSize** ](https://msdn.microsoft.com/library/windows/hardware/ff549446)関数。

構造体のメンバーのオフセットを見つけるには使用、 [ **GetFieldOffset** ](https://msdn.microsoft.com/library/windows/hardware/ff546758)関数。

まず、構造体の複数のメンバーを読み取りを使用して、 [ **InitTypeRead** ](https://msdn.microsoft.com/library/windows/hardware/ff550953)構造体を初期化する関数。 次に、使用、 [ **ReadField** ](https://msdn.microsoft.com/library/windows/hardware/ff553539)を一度に 1 つの 8 バイト未満、サイズを持つメンバーを読み取る関数。 物理メモリ内構造体のアドレスを使用して、 [ **InitTypeReadPhysical** ](https://msdn.microsoft.com/library/windows/hardware/ff550957)関数の代わりに**InitTypeRead**します。

リンク リストを反復処理するために使用できる 2 つの関数があります。 リストを使用する二重リンク リストの\_ENTRY32 またはリスト\_ENTRY64 構造体、関数は、 [ **ReadListEntry** ](https://msdn.microsoft.com/library/windows/hardware/ff553585)次または前のエントリを検索するために使用できます。 関数は、 [ **ListType** ](https://msdn.microsoft.com/library/windows/hardware/ff551988)リンク リストのすべてのエントリを反復処理され、各エントリのコールバック関数を呼び出します。

ターゲットのメモリ内で指定されたアドレスの近くのシンボルを見つけるには使用、 [ **GetSymbol** ](https://msdn.microsoft.com/library/windows/hardware/ff548447)関数。

デバッガー エンジンのキャッシュからすべてのシンボル情報を削除するには使用、 [ **ReloadSymbols** ](https://msdn.microsoft.com/library/windows/hardware/ff554381)関数。 読み取りまたはシンボル ファイルの検索に使用される、シンボル パスを変更するには使用、 [ **GetSetSympath** ](https://msdn.microsoft.com/library/windows/hardware/ff548291)関数。

使用してデバッガー エンジンによって提供されるほとんどすべてのシンボルの操作を実行することができます、 [ **Ioctl** ](https://msdn.microsoft.com/library/windows/hardware/ff551084)操作[ **IG\_ダンプ\_シンボル\_情報**](https://msdn.microsoft.com/library/windows/hardware/ff550906)します。 ただし、非常に柔軟な関数を使用したときに、高度なことですし、該当する場合は、上記の簡単な関数を使用することをお勧めします。

### <a name="span-idadditionalinformationspanspan-idadditionalinformationspanadditional-information"></a><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>追加情報

強力なシンボル API では、次を参照してください。[を使用してシンボル](using-symbols.md)で、[デバッガー エンジン API を使用して](using-the-debugger-engine-api.md)このドキュメントの「します。

 

 





