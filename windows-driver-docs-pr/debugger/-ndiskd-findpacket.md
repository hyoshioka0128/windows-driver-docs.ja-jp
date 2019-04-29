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
ms.openlocfilehash: 9debfc45c946987dc72a585edaae2f7e445e217b
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63335997"
---
# <a name="ndiskdfindpacket"></a>!ndiskd.findpacket


**警告**  は従来の NDIS 5.x ドライバーのこの拡張子です。 [NDIS\_パケット](https://msdn.microsoft.com/library/windows/hardware/ff557086)構造とその関連付けられているアーキテクチャが使用されなくなりました。

 

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

[NDIS\_パケット](https://msdn.microsoft.com/library/windows/hardware/ff557086)

 

 






