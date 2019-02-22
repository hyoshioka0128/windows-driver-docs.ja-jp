---
title: HS_MAC_ADDRESS 構造体
description: HS_MAC_ADDRESS 構造体には、ホスト メディア アクセス コントロール (MAC) アドレスにはが含まれています。
ms.assetid: 2d632ed4-4522-48ae-b23d-927517185d73
keywords:
- Windows Vista 以降のドライバーをネットワーク HS_MAC_ADDRESS が構造体します。
- Windows Vista 以降のドライバーをネットワーク PHS_MAC_ADDRESS 構造体ポインター
ms.date: 07/31/2017
ms.localizationpriority: medium
ms.openlocfilehash: c3da45d1c5f9088da55ec0b771ecfecc433b25ea
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56536242"
---
# <a name="hsmacaddress-structure"></a>HS\_MAC\_アドレスの構造

[!include[Wi-Fi Hotspot Offloading deprecation](wi-fi-hotspot-offloading-deprecation.md)]


**HS\_MAC\_アドレス**構造には、ホスト メディア アクセス コントロール (MAC) アドレスにはが含まれています。

<a name="syntax"></a>構文
------

```ManagedCPlusPlus
typedef struct _HS_MAC_ADDRESS {
  UCHAR ucHSMacAddress[6];
} HS_MAC_ADDRESS, *PHS_MAC_ADDRESS;
```

<a name="members"></a>Members
-------

**ucHSMacAddress**  
MAC アドレス。

<a name="requirements"></a>要件
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>Header</p></td>
<td>Hotspotoffloadplugin.h (Hotspotoffloadplugin.h を含む)</td>
</tr>
</tbody>
</table>

 

 




