---
title: ndiskd.findpacket
description: この拡張機能の警告が、従来の NDIS 5.x ドライバーです。 NDIS_PACKET 構造とその関連付けられているアーキテクチャが推奨されていません。 Ndiskd.findpacket 拡張機能は、指定されたパケットを検索します。
ms.assetid: fc07b2d8-85ca-4be1-ae9d-40b7c7f81b08
keywords:
- デバッグ ndiskd.findpacket Windows
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- ndiskd.findpacket
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 025c09e65c83148d9cec6c6b1a9101d1abdbac32
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67363160"
---
# <a name="ndiskdfindpacket"></a>!ndiskd.findpacket


**警告**  は従来の NDIS 5.x ドライバーのこの拡張子です。 [NDIS\_パケット](https://docs.microsoft.com/previous-versions/windows/hardware/network/ff557086(v=vs.85))構造とその関連付けられているアーキテクチャが使用されなくなりました。

 

**! Ndiskd.findpacket**拡張機能は、指定されたパケットを検索します。

```console
!ndiskd.findpacket [-VirtualAddress] [-PoolAddress]  
```

## <a name="span-idddkndiskdfindpacketdbgspanspan-idddkndiskdfindpacketdbgspanparameters"></a><span id="ddk__ndiskd_findpacket_dbg"></span><span id="DDK__NDISKD_FINDPACKET_DBG"></span>パラメーター


<span id="_______VirtualAddress______"></span><span id="_______virtualaddress______"></span><span id="_______VIRTUALADDRESS______"></span> *virtualAddress*   
目的のパケットに格納されている仮想アドレスを指定します。

<span id="_______PoolAddress______"></span><span id="_______pooladdress______"></span><span id="_______POOLADDRESS______"></span> *PoolAddress*   
プールのアドレスを指定します。 このプール内のすべての unreturned パケットが表示されます。

### <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>DLL

Ndiskd.dll

## <a name="span-idseealsospansee-also"></a><span id="see_also"></span>参照してください。

[NDIS\_パケット](https://docs.microsoft.com/previous-versions/windows/hardware/network/ff557086(v=vs.85))

 

 






