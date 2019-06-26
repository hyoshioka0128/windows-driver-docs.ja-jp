---
title: WdbgExts のシンボル
description: WdbgExts のシンボル
ms.assetid: 7e1a1799-b87c-42cb-94ce-fbdc9a5ec973
keywords:
- シンボル、WdbgExts 拡張機能
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: 82021a03fd758a0429d1374f0bc4634fa9844dce
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67369411"
---
# <a name="wdbgexts-symbols"></a>WdbgExts のシンボル


このトピックではシンボルをする方法の概要、WdbgExts API を使用して操作します。 内のシンボルを使用しての概要については、[デバッガー エンジン](introduction.md#debugger-engine)を参照してください[シンボル](symbols.md)で、[デバッガー エンジンの概要](debugger-engine-overview.md)このドキュメントの「します。

MASM または C++ の式を評価する関数を使用して[ **GetExpression** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdbgexts/nc-wdbgexts-pwindbg_get_expression)または[ **GetExpressionEx**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdbgexts/nf-wdbgexts-getexpressionex)します。

構造体のメンバーの値を読み取り、使用、 [ **GetFieldData** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdbgexts/nf-wdbgexts-getfielddata)関数、またはの場合、メンバーには、プリミティブ型の値が含まれています[ **GetFieldValue** 。](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdbgexts/nf-wdbgexts-getfieldvalue)ことができます。 ターゲットのメモリ内のシンボルのインスタンスのサイズを調べるには、 [ **GetTypeSize** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdbgexts/nf-wdbgexts-gettypesize)関数。

構造体のメンバーのオフセットを見つけるには使用、 [ **GetFieldOffset** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgeng/nf-dbgeng-idebugsymbols-getfieldoffset)関数。

まず、構造体の複数のメンバーを読み取りを使用して、 [ **InitTypeRead** ](https://docs.microsoft.com/previous-versions/ff550953(v=vs.85))構造体を初期化する関数。 次に、使用、 [ **ReadField** ](https://docs.microsoft.com/previous-versions/ff553539(v=vs.85))を一度に 1 つの 8 バイト未満、サイズを持つメンバーを読み取る関数。 物理メモリ内構造体のアドレスを使用して、 [ **InitTypeReadPhysical** ](https://docs.microsoft.com/previous-versions/ff550957(v=vs.85))関数の代わりに**InitTypeRead**します。

リンク リストを反復処理するために使用できる 2 つの関数があります。 リストを使用する二重リンク リストの\_ENTRY32 またはリスト\_ENTRY64 構造体、関数は、 [ **ReadListEntry** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdbgexts/nf-wdbgexts-readlistentry)次または前のエントリを検索するために使用できます。 関数は、 [ **ListType** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdbgexts/nf-wdbgexts-listtype)リンク リストのすべてのエントリを反復処理され、各エントリのコールバック関数を呼び出します。

ターゲットのメモリ内で指定されたアドレスの近くのシンボルを見つけるには使用、 [ **GetSymbol** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdbgexts/nc-wdbgexts-pwindbg_get_symbol)関数。

デバッガー エンジンのキャッシュからすべてのシンボル情報を削除するには使用、 [ **ReloadSymbols** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdbgexts/nf-wdbgexts-reloadsymbols)関数。 読み取りまたはシンボル ファイルの検索に使用される、シンボル パスを変更するには使用、 [ **GetSetSympath** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdbgexts/nf-wdbgexts-getsetsympath)関数。

使用してデバッガー エンジンによって提供されるほとんどすべてのシンボルの操作を実行することができます、 [ **Ioctl** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdbgexts/nc-wdbgexts-pwindbg_ioctl_routine)操作[ **IG\_ダンプ\_シンボル\_情報**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdbgexts/ns-wdbgexts-_sym_dump_param)します。 ただし、非常に柔軟な関数を使用したときに、高度なことですし、該当する場合は、上記の簡単な関数を使用することをお勧めします。

### <a name="span-idadditionalinformationspanspan-idadditionalinformationspanadditional-information"></a><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>追加情報

強力なシンボル API では、次を参照してください。[を使用してシンボル](using-symbols.md)で、[デバッガー エンジン API を使用して](using-the-debugger-engine-api.md)このドキュメントの「します。

 

 





