---
title: HS_SIM_DATA 構造体
description: HS_SIM_DATA 構造体には、SIM カードに格納された情報が含まれています。
ms.assetid: 9e29a85e-e764-4841-b218-c63bba0ca9fa
keywords:
- Windows Vista 以降のドライバーをネットワーク HS_SIM_DATA 構造体
- Windows Vista 以降のドライバーをネットワーク PHS_SIM_DATA 構造体ポインター
ms.date: 07/31/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5472ef1830e08cbea36a9fa879b22adde3614bbf
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63322137"
---
# <a name="hssimdata-structure"></a>HS\_SIM\_データ構造体

[!include[Wi-Fi Hotspot Offloading deprecation](wi-fi-hotspot-offloading-deprecation.md)]


**HS\_SIM\_データ**構造体には、SIM カードに格納された情報が含まれています。

<a name="syntax"></a>構文
------

```ManagedCPlusPlus
typedef struct _HS_SIM_DATA {
  WCHAR wszICCID[HS_CONST_MAX_ICCID_LENGTH+1];
  WCHAR wszIMEI[HS_CONST_MAX_IMEI_LENGTH+1];
  WCHAR wszMEID_ME[HS_CONST_MAX_MEID_ME_LENGTH+1];
  WCHAR wszSF_EUIMID[HS_CONST_MAX_SF_EUIMID_LENGTH+1];
} HS_SIM_DATA, *PHS_SIM_DATA;
```

<a name="members"></a>メンバー
-------

**wszICCID**  
Integrated 回線カード識別子 (ICCID) SIM カードに格納されています。

**wszIMEI**  
International Mobile Equipment Identity (IMEI) は、3 gpp のスマート フォンを識別するために使用されます。

**wszMEID\_ME**  
モバイル機器識別子 (MEID) 3GPP2 によって定義します。

**wszSF\_EUIMID**  
短いフォーム展開ユーザー Identity モジュールの識別子 (EUIMID)、R UIM または CSIM (CDMA SIM アプリケーション) カードの。

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

 

 




