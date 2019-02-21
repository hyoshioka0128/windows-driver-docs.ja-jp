---
title: HS_CONNECTION_CONTEXT 構造体
description: HS_CONNECTION_CONTEXT 構造体には、プラグインによって post connect 認証するために必要な情報が含まれています。
ms.assetid: 22b219fc-691b-4813-a523-a76de037e64d
keywords:
- Windows Vista 以降のドライバーをネットワーク HS_CONNECTION_CONTEXT 構造体
- Windows Vista 以降のドライバーをネットワーク PHS_CONNECTION_CONTEXT 構造体ポインター
ms.date: 07/31/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4fe42ada75739323a10c0cbc78e0975ff7276a0b
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56530863"
---
# <a name="hsconnectioncontext-structure"></a>HS\_接続\_CONTEXT 構造体

[!include[Wi-Fi Hotspot Offloading deprecation](wi-fi-hotspot-offloading-deprecation.md)]


**HS\_接続\_コンテキスト**構造体には、プラグインによって post connect 認証するために必要な情報が含まれています。

<a name="syntax"></a>構文
------

```ManagedCPlusPlus
typedef struct _HS_CONNECTION_CONTEXT {
  HS_MAC_ADDRESS  MacAddress;
  HS_SIM_IDENTITY SIMIdentity;
  WCHAR           pszPhoneNumber[HS_MAX_PHONE_NUMBER_LENGTH+1];
} HS_CONNECTION_CONTEXT, *PHS_CONNECTION_CONTEXT;
```

<a name="members"></a>Members
-------

**Mac アドレス**  
[ **HS\_MAC\_アドレス**](hs-mac-address.md) MAC アドレスを含む構造体。

**SIMIdentity**  
[ **HS\_SIM\_IDENTITY** ](hs-sim-identity.md) AKA SIM/EAP の認証に必要な情報を含む構造体。

**pszPhoneNumber**  
電話番号へのポインター。

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

## <a name="see-also"></a>関連項目


[**HS\_MAC\_アドレス**](hs-mac-address.md)

[**HS\_SIM\_の ID**](hs-sim-identity.md)

 

 




