---
title: WdbgExts のシンボル
description: WdbgExts のシンボル
ms.assetid: 7e1a1799-b87c-42cb-94ce-fbdc9a5ec973
keywords:
- WdbgExts 拡張機能、シンボル
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: a8cabb8ee1edcee237821e5705837116bb695a0b
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72838794"
---
# <a name="wdbgexts-symbols"></a>WdbgExts のシンボル


このトピックでは、WdbgExts API を使用してシンボルを操作する方法の概要について説明します。 [デバッガーエンジン](introduction.md#debugger-engine)でのシンボルの使用の概要については、このドキュメントの「[デバッガーエンジンの概要](debugger-engine-overview.md)」セクションの「[シンボル](symbols.md)」を参照してください。

MASM またC++は式を評価するには、関数[**Getexpression または getexpression**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdbgexts/nc-wdbgexts-pwindbg_get_expression) [**ex**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdbgexts/nf-wdbgexts-getexpressionex)を使用します。

構造体のメンバーの値を読み取るには、 [**Getfielddata**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdbgexts/nf-wdbgexts-getfielddata)関数を使用します。または、メンバーにプリミティブ値が含まれている場合は、 [**GetFieldValue**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdbgexts/nf-wdbgexts-getfieldvalue)を使用できます。 ターゲットのメモリ内のシンボルのインスタンスのサイズを確認するには、 [**GetTypeSize**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdbgexts/nf-wdbgexts-gettypesize)関数を使用します。

構造体のメンバーのオフセットを検索するには、 [**GetFieldOffset**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-idebugsymbols-getfieldoffset)関数を使用します。

構造体の複数のメンバーを読み取るには、最初に[**InitTypeRead**](https://docs.microsoft.com/previous-versions/ff550953(v=vs.85))関数を使用して構造体を初期化します。 次に、 [**Readfield**](https://docs.microsoft.com/previous-versions/ff553539(v=vs.85))関数を使用して、サイズが8バイト以下のメンバーを一度に1つ読み取ることができます。 物理メモリ内の構造体アドレスの場合は、 **InitTypeRead**ではなく[**InitTypeReadPhysical**](https://docs.microsoft.com/previous-versions/ff550957(v=vs.85))関数を使用します。

リンクリストの反復処理に使用できる関数は2つあります。 リスト\_ENTRY32 または LIST\_ENTRY64 構造体を使用する二重リンクリストでは、関数[**ReadListEntry**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdbgexts/nf-wdbgexts-readlistentry)を使用して次のエントリと前のエントリを検索できます。 関数[**Listtype**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdbgexts/nf-wdbgexts-listtype)は、リンクリスト内のすべてのエントリを反復処理し、各エントリに対してコールバック関数を呼び出します。

ターゲットのメモリ内の指定されたアドレス付近のシンボルを検索するには、 [**Getsymbol**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdbgexts/nc-wdbgexts-pwindbg_get_symbol)関数を使用します。

デバッガーエンジンのキャッシュからすべてのシンボル情報を削除するには、 [**Reloadsymbols**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdbgexts/nf-wdbgexts-reloadsymbols)関数を使用します。 シンボルファイルの検索に使用されるシンボルパスを読み取りまたは変更するには、 [**GetSetSympath**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdbgexts/nf-wdbgexts-getsetsympath)関数を使用します。

デバッガーエンジンによって提供されるほとんどすべてのシンボル操作を実行するには、 [**Ioctl**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdbgexts/nc-wdbgexts-pwindbg_ioctl_routine)操作[**IG\_DUMP\_symbol\_INFO**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdbgexts/ns-wdbgexts-_sym_dump_param)を使用します。 ただし、非常に柔軟な関数であっても、高度な機能を備えているので、上記の単純な関数を使用することをお勧めします。

### <a name="span-idadditional_informationspanspan-idadditional_informationspanadditional-information"></a><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>追加情報

より強力なシンボル API については、このドキュメントの「 [using The Debugger ENGINE api](using-the-debugger-engine-api.md) 」セクションの「 [using symbols](using-symbols.md) 」を参照してください。

 

 





