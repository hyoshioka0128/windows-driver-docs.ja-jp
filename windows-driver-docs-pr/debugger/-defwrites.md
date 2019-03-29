---
title: defwrites
description: Defwrites 拡張機能には、キャッシュ マネージャーによって使用されるカーネルの変数の値が表示されます。
ms.assetid: da576e05-3d9f-4599-bf8e-b1fa05093d77
keywords:
- キャッシュ マネージャー
- Windows デバッグ defwrites
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- defwrites
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 2e54cc4f1f01e091870c9979cc77fcaaa2bec9e9
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56571033"
---
# <a name="defwrites"></a>!defwrites


**! Defwrites**拡張機能には、キャッシュ マネージャーによって使用されるカーネルの変数の値が表示されます。

```dbgcmd
!defwrites
```

## <span id="ddk__defwrites_dbg"></span><span id="DDK__DEFWRITES_DBG"></span>


### <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>DLL

Kdexts.dll
 

### <a name="span-idadditionalinformationspanspan-idadditionalinformationspanspan-idadditionalinformationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>追加情報

書き込みの制限については、次を参照してください。 *Microsoft Windows internals 』* Mark Russinovich と David Solomon します。 

その他のキャッシュ管理拡張機能については、使用、 [ **! cchelp** ](-cchelp.md)拡張機能。

<a name="remarks"></a>コメント
-------

遅延書き込み (「ダーティ ページ」) の数が大きすぎると、ページの書き込みが調整されます。 この拡張機能、システムがこのポイントに達したかどうかを確認することができます。

以下に例を示します。

```dbgcmd
kd> !defwrites 
*** Cache Write Throttle Analysis ***

        CcTotalDirtyPages:                   0 (       0 Kb)
        CcDirtyPageThreshold:             1538 (    6152 Kb)
        MmAvailablePages:                 2598 (   10392 Kb)
        MmThrottleTop:                     250 (    1000 Kb)
        MmThrottleBottom:                   30 (     120 Kb)
        MmModifiedPageListHead.Total:      699 (    2796 Kb)

Write throttles not engaged
```

この場合は、ダーティ ページではありません。 場合**CcTotalDirtyPages** 1538 に達すると (の値**CcDirtyPageThreshold**)、書き込みはダーティ ページの数が減少するまで遅延されます。

 

 





