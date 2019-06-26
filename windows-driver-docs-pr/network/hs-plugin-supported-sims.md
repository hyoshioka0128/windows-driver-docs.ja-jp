---
title: HS_PLUGIN_SUPPORTED_SIMS 構造体
description: HS_PLUGIN_SUPPORTED_SIMS 構造体には、SIM でサポートされる構成の一覧が含まれています。 ホット スポットのプラグインは、そのネットワークのいずれかの HTTP または EAP 認証を必要とする場合、この一覧を指定する必要があります。
ms.assetid: 7ec8fb95-b227-4feb-882e-457a9ad6ec3e
keywords:
- Windows Vista 以降のドライバーをネットワーク HS_PLUGIN_SUPPORTED_SIMS が構造体します。
- Windows Vista 以降のドライバーをネットワーク PHS_PLUGIN_SUPPORTED_SIMS 構造体ポインター
ms.date: 07/31/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6804143fe8be10d4e8306c742fe2832b0aa7f2f6
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67364057"
---
# <a name="hspluginsupportedsims-structure"></a>HS\_プラグイン\_サポートされている\_SIM 構造体

[!include[Wi-Fi Hotspot Offloading deprecation](wi-fi-hotspot-offloading-deprecation.md)]


**HS\_プラグイン\_サポートされている\_SIM**構造体には、SIM でサポートされる構成の一覧が含まれています。 ホット スポットのプラグインは、そのネットワークのいずれかの HTTP または EAP 認証を必要とする場合、この一覧を指定する必要があります。

<a name="syntax"></a>構文
------

```ManagedCPlusPlus
typedef struct _HS_PLUGIN_SUPPORTED_SIMS {
  DWORD           dwCount;
  HS_SIM_IDENTITY pSupportedSIMs[*];
  HS_SIM_IDENTITY pSupportedSIMs[1];
} HS_PLUGIN_SUPPORTED_SIMS, *PHS_PLUGIN_SUPPORTED_SIMS;
```

<a name="members"></a>メンバー
-------

**dwCount**  
リストのサイズ。

**pSupportedSIMs**  
MIDL を使用する場合に使用されます。 サイズは、一意である (dwCount) です。

HS の配列\_SIM\_IDENTITY 構造体のリストを構成するには、SIM 構成がサポートされています。

**pSupportedSIMs**  
MIDL が利用されていない場合に使用します。

HS の配列\_SIM\_IDENTITY 構造体のリストを構成するには、SIM 構成がサポートされています。

<a name="remarks"></a>注釈
-------

**DwEapMethods**のフィールド、 [ **HS\_SIM\_IDENTITY** ](hs-sim-identity.md)構造 SIM 構成ごとに、EAP メソッドを指定する必要がありますがサポートします。

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


[**HS\_SIM\_の ID**](hs-sim-identity.md)

[Microsoft インターフェイス定義言語](https://docs.microsoft.com/windows/desktop/Midl/midl-start-page)

 

 




