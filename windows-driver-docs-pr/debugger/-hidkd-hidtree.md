---
title: hidkd.hidtree
description: Hidkd.hidtree コマンドは、その子ノードと共に HID 機能ドライバーを持つすべてのデバイス ノードの一覧を表示します。
ms.assetid: 50FD5526-3B0E-4585-BFFD-72ED363D007A
keywords:
- デバッグ hidkd.hidtree Windows
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- hidkd.hidtree
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: c6d6304de090ad2ffc27721a49d599045e2a781b
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56531874"
---
# <a name="hidkdhidtree"></a>! hidkd.hidtree


**! Hidkd.hidtree**コマンドは、その子ノードと共に HID 機能ドライバーを持つすべてのデバイス ノードの一覧を表示します。 子ノードでは、親ノードの HID 関数ドライバーによって作成された、物理デバイス オブジェクト (PDO) が存在します。

```dbgcmd
!hidkd.hidtree
```

このスクリーン ショットの出力の例を示しています、 **! hidtree**コマンド。

![hidtree コマンドの出力](images/hidkd01.png)

O

この例では、HID 関数ドライバーがある 2 つのデバイス ノードです。 機能のデバイス オブジェクト (FDO) は、これら 2 つのノードで HID ドライバーを表します。 FDO の最初のノードが 2 つの子ノードと 2 番目の FDO ノードが 1 つの子ノード。 デバッガーの出力では、子ノードは、PDO 見出しがあります。

**注**  このデバイス ノードのセットでは単一のルート ノードを持つツリーが形成されていません。 HID 機能ドライバーを持つデバイス ノードは互いから分離することはできます。

 

HID の問題をデバッグするとき、 **! hidtree**のコマンドは、他の HID デバッガー コマンドに渡すことができるいくつかのアドレスを表示するために、お勧めは、します。 出力を使用して[デバッガー マークアップ言語 (DML)](debugger-markup-language-commands.md)リンクを提供します。 リンクは、個々 のデバイス ノードに関連する詳細な情報を提供するコマンドを実行します。 たとえばのいずれかをクリックして FDO に関する情報を取得できます、 [ **! hidfdo** ](-hidkd-hidfdo.md)リンク。 リンクをクリックする代わりに、コマンドを入力することができます。 たとえば、上記の出力の最初のノードに関する詳細な情報を表示することがコマンドを入力する **! devnode 0xffffe00003b18d30**します。

**注**  DML の機能は、WinDbg がではなく Visual Studio または KD で使用できます。

 

## <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>DLL


Hidkd.dll

## <a name="span-idseealsospansee-also"></a><span id="see_also"></span>参照してください。


[HID の拡張機能](hid-extensions.md)

 

 






