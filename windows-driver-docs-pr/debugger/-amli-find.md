---
title: amli 検索
description: Amli ACPI 名前空間オブジェクトの検索拡張機能を検索します。
ms.assetid: bacb1be2-f079-49da-a8d2-1e9821b20ed3
keywords:
- Windows デバッグ amli 検索
ms.date: 09/17/2018
topic_type:
- apiref
api_name:
- amli find
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 446c2f36f94500054a4022649dffebc2cd697e07
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63334764"
---
# <a name="amli-find"></a>!amli find


**! Amli 検索**拡張機能は、ACPI 名前空間のオブジェクトを検索します。

構文

```dbgcmd
    !amli find Name
```

## <a name="span-idddkamlifinddbgspanspan-idddkamlifinddbgspanparameters"></a><span id="ddk__amli_find_dbg"></span><span id="DDK__AMLI_FIND_DBG"></span>パラメーター


<span id="_______Name______"></span><span id="_______name______"></span><span id="_______NAME______"></span> *名*   
(パス) を使用せず、名前空間オブジェクトの名前を指定します。

### <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>DLL

Kdexts.dll

### <a name="span-idadditionalinformationspanspan-idadditionalinformationspanspan-idadditionalinformationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>追加情報

関連するコマンドとその用途については、次を参照してください。 [AMLI デバッガー](the-amli-debugger.md)します。

<a name="remarks"></a>コメント
-------

**! Amli 検索**コマンド オブジェクトの名前を受け取るし、完全なパスと名前を返します。 *名前*パラメーターは、完全なパスと名前の最後のセグメントである必要があります。

例をいくつか紹介します。 次のコマンドは、オブジェクトのすべての宣言を検索\_SRS:

```console
kd> !amli find _srs
\_SB.LNKA._SRS
\_SB.LNKB._SRS
\_SB.LNKC._SRS
\_SB.LNKD._SRS
```

これは、単にテキストの検索ではありません。 コマンドは、 **! amli 検索 srs**これらの各宣言の最後のセグメントがあるため、すべてのヒット数は表示されません"\_SRS"、"SRS"ではありません。 コマンドは、 **! amli 検索 LNK**同様に、ヒットは返しません。 コマンドは、 **! amli 検索 LNKB**前の表示に示すようにこのノードの 4 つの子ではありません"LNKB"で終了して 1 つのノードに表示されます。

```console
kd> !amli find lnkb
\_SB.LNKB.
```

ノードの子を表示する必要がある場合、 [ **! amli dns** ](-amli-dns.md)コマンドと、 **/s**パラメーター。

プロンプト AMLI デバッガーから発行された、別の例を次に示します。 これは、オブジェクトのすべての宣言を示しています\_BST 名前空間。

```console
AMLI(? for help)-> find _bst
\_SB.PCI0.ISA.BAT1._BST
\_SB.PCI0.ISA.BAT2._BST
```

 

 





