---
title: HS_SIM_IDENTITY 構造体
description: HS_SIM_IDENTITY 構造体には、EAP SIM または EAP-AKA の認証に必要な SIM 識別情報が含まれています。
ms.assetid: b45fac33-79de-4006-9dcb-95725be11ec1
keywords:
- Windows Vista 以降のドライバーをネットワーク HS_SIM_IDENTITY 構造体
- Windows Vista 以降のドライバーをネットワーク PHS_SIM_IDENTITY 構造体ポインター
ms.date: 07/31/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5f1e8b3931fd6dd90e84f413d0e531ad02d9035c
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63322142"
---
# <a name="hssimidentity-structure"></a>HS\_SIM\_IDENTITY 構造体

[!include[Wi-Fi Hotspot Offloading deprecation](wi-fi-hotspot-offloading-deprecation.md)]


**HS\_SIM\_IDENTITY**構造体には、EAP SIM または EAP-AKA の認証に必要な SIM 識別情報が含まれています。

<a name="syntax"></a>構文
------

```ManagedCPlusPlus
typedef struct _HS_SIM_IDENTITY {
  eHS_SIM_TYPE SimType;
  DWORD        dwMNC;
  DWORD        dwMCC;
  DWORD        dwNID;
  DWORD        dwSID;
  DWORD        dwEapMethods;
} HS_SIM_IDENTITY, *PHS_SIM_IDENTITY;
```

<a name="members"></a>メンバー
-------

**SimType**  
SIM の型かどうか、GSM または CDMA、または none。 ネットワークが、GSM の場合、 **dwMNC**と**dwMCC**は 2 つのフィールドが定義される CDMA の**dwSID**と**dwNID** 2 つのフィールド定義する必要があります。

**dwMNC**  
SIM が GSM 型である場合に使用します。

GSM ネットワークのモバイル ネットワーク コード (mnc も)。

**dwMCC**  
SIM が GSM 型である場合に使用します。

GSM ネットワークのモバイルの国コード (MCC) です。

**dwNID**  
SIM が CDMA 型である場合に使用します。

ネットワークの識別番号 (NID) CDMA ネットワーク。

**dwSID**  
SIM が CDMA 型である場合に使用します。

システム Id (SID) の CDMA ネットワーク。

**dwEapMethods**  
EAP 認証方法。

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


[拡張認証プロトコル](https://msdn.microsoft.com/library/windows/desktop/aa363502)

 

 




