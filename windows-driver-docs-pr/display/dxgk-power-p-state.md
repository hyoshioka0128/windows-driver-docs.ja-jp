---
title: DXGK\_POWER\_P\_状態構造体
description: システムの使用に予約されています。 ドライバーでは使用しないでください。
ms.assetid: F4612284-36C8-49C4-914D-43C32489EABD
keywords:
- DXGK_POWER_P_STATE 構造体のディスプレイ デバイス
- PDXGK_POWER_P_STATE 構造体ポインター ディスプレイ デバイス
topic_type:
- apiref
api_name:
- DXGK_POWER_P_STATE
api_location:
- D3dkmddi.h
api_type:
- HeaderDef
ms.date: 01/05/2018
ms.localizationpriority: medium
ms.openlocfilehash: 216d30e15ceb8690160bc0655371d24bcaef7b65
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56532568"
---
# <a name="dxgkpowerpstate-structure"></a>DXGK\_POWER\_P\_状態構造体


システムの使用に予約されています。 ドライバーでは使用しないでください。

<a name="syntax"></a>構文
------

```ManagedCPlusPlus
typedef struct _DXGK_POWER_P_STATE {
  ULONG     NominalPower;
  ULONG     OperatingFrequency;
  ULONGLONG TransitionLatencies[DXGK_MAX_P_STATES];
  ULONGLONG ResidencyRequirement;
} DXGK_POWER_P_STATE, *PDXGK_POWER_P_STATE;
```

<a name="members"></a>Members
-------

**NominalPower**

**OperatingFrequency**

**TransitionLatencies**

**ResidencyRequirement**

<a name="requirements"></a>要件
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p>サポートされている最小のクライアント</p></td>
<td align="left"><p>Windows 8.1</p></td>
</tr>
<tr class="even">
<td align="left"><p>サポートされている最小のサーバー</p></td>
<td align="left"><p>Windows Server 2012 R2</p></td>
</tr>
<tr class="odd">
<td align="left"><p>Header</p></td>
<td align="left">D3dkmddi.h (include D3dkmddi.h)</td>
</tr>
</tbody>
</table>

 

 





