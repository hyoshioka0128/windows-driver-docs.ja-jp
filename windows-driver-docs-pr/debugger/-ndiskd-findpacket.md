---
title: ndiskd findpacket
description: 警告この拡張機能は、レガシ NDIS 5.x ドライバー用です。 NDIS_PACKET 構造とそれに関連付けられているアーキテクチャは非推奨となりました。Ndiskd findpacket 拡張機能は、指定されたパケットを検索します。
ms.assetid: fc07b2d8-85ca-4be1-ae9d-40b7c7f81b08
keywords:
- ndiskd findpacket Windows デバッグ
ms.date: 06/15/2020
topic_type:
- apiref
api_name:
- ndiskd.findpacket
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 8aab4328493f0aec9aa88f656e7fd3a621c38454
ms.sourcegitcommit: 8596782b07c8a71adf38fc2c2da68b75ba0a1259
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/01/2020
ms.locfileid: "85593948"
---
# <a name="ndiskdfindpacket"></a>!ndiskd.findpacket

**警告**   この拡張機能は、従来の NDIS 5.x ドライバー用です。 [NDIS \_ パケット](https://docs.microsoft.com/previous-versions/windows/hardware/network/ff557086(v=vs.85))構造とそれに関連付けられているアーキテクチャは非推奨となりました。

**! Ndiskd findpacket**拡張機能は、指定されたパケットを検索します。

```console
!ndiskd.findpacket [-VirtualAddress] [-PoolAddress]  
```

## <a name="parameters"></a>パラメーター

<span id="_______VirtualAddress______"></span><span id="_______virtualaddress______"></span><span id="_______VIRTUALADDRESS______"></span>*Virtualaddress*   
目的のパケットに含まれる仮想アドレスを指定します。

<span id="_______PoolAddress______"></span><span id="_______pooladdress______"></span><span id="_______POOLADDRESS______"></span>*Pooladdress*   
プールアドレスを指定します。 このプール内の返されていないすべてのパケットが表示されます。

### <a name="dll"></a>[DLL]

Ndiskd.dll

## <a name="see-also"></a>関連項目

[NDIS \_ パケット](https://docs.microsoft.com/previous-versions/windows/hardware/network/ff557086(v=vs.85))
