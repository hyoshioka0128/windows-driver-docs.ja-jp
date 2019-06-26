---
title: ndiskd.pktpools
description: この拡張機能の警告が、従来の NDIS 5.x ドライバーです。 Ndiskd.pktpools 拡張機能では、すべてのパケットを割り当てられたプールの一覧が表示されます。
ms.assetid: 0aceb22c-17ab-4199-a313-ecbc4c8f0b6e
keywords:
- デバッグ ndiskd.pktpools Windows
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- ndiskd.pktpools
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 3953c94e9d9c586c723f50eae444a803c5c8dbb9
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67362458"
---
# <a name="ndiskdpktpools"></a>!ndiskd.pktpools


**警告**  は従来の NDIS 5.x ドライバーのこの拡張子です。 [NDIS\_パケット](https://docs.microsoft.com/previous-versions/windows/hardware/network/ff557086(v=vs.85))構造とその関連付けられているアーキテクチャが使用されなくなりました。

 

**! Ndiskd.pktpools**拡張機能は、すべてのパケットを割り当てられたプールの一覧を表示します。

```console
!ndiskd.pktpools 
```

## <span id="ddk__ndiskd_pktpools_dbg"></span><span id="DDK__NDISKD_PKTPOOLS_DBG"></span>


### <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>DLL

Ndiskd.dll

<a name="examples"></a>例
--------

実行、 **! ndiskd.pktpools**拡張機能をシステム上のすべてのパケットを割り当てられたプールの一覧を参照してください。 パケット プール ハンドルいないこと、つまり、パケットのプールに関する詳細情報を探索することはできませんに注意してください。 NDIS がパケット プールが以前のシステムである可能性がありますが、従来のドライバーに対してだけこれらのプールが割り当てられているために、NDIS 6.0 以降を使用しないためにです。 この例では、デバッグ対象のマシンのパケットのプールが使用されないようにインストールされているレガシ NDIS 5.x ドライバーではありません。 この例では、例示を目的としてのみです。

```console
3: kd> !ndiskd.pktpools
Pool      Allocator  BlocksAllocated  BlockSize  PktsPerBlock  PacketLength
ffffdf80131d58c0  fffff80f1fbe3e8f   0x1          0x1000     0xa           0x190   ndis!DriverEntry+6af
ffffdf80131d5940  fffff80f1fbe3e71   0x1          0x1000     0xa           0x180   ndis!DriverEntry+691
```

## <a name="span-idseealsospansee-also"></a><span id="see_also"></span>参照してください。


[Windows 2000 および Windows XP のネットワーク設計ガイド](https://docs.microsoft.com/previous-versions/windows/hardware/network/ff565849(v=vs.85))

[Windows 2000 および Windows XP のネットワークの参照](https://docs.microsoft.com/previous-versions/windows/hardware/network/ff565850(v=vs.85))

[NDIS\_パケット](https://docs.microsoft.com/previous-versions/windows/hardware/network/ff557086(v=vs.85))

 

 






