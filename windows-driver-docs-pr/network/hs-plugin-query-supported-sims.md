---
title: HS_PLUGIN_QUERY_SUPPORTED_SIMS 関数
description: HS_PLUGIN_QUERY_SUPPORTED_SIMS 関数は、プラグインをサポートする Sim の一覧を返します。
ms.assetid: e1b41bb1-7f82-4298-b070-20cb557fa0fc
keywords:
- Windows Vista 以降のドライバーをネットワーク typedef DWORD (WINAPI HS_PLUGIN_QUERY_SUPPORTED_SIMS) 関数
ms.date: 07/31/2017
ms.localizationpriority: medium
ms.openlocfilehash: 20c7948c6769893e6147fc5b774d1e61f8282214
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56535734"
---
# <a name="hspluginquerysupportedsims-function"></a>HS\_プラグイン\_クエリ\_サポートされている\_SIM 関数

[!include[Wi-Fi Hotspot Offloading deprecation](wi-fi-hotspot-offloading-deprecation.md)]


**HS\_プラグイン\_クエリ\_サポートされている\_SIM**関数は、プラグインをサポートする Sim の一覧を返します。

<a name="syntax"></a>構文
------

```ManagedCPlusPlus
 typedef DWORD (WINAPI *HS_PLUGIN_QUERY_SUPPORTED_SIMS)(
  _In_opt_ HS_NETWORK_IDENTITY      *pNetworkIdentity,
  _Inout_  HS_PLUGIN_SUPPORTED_SIMS *pSupportedSIMs
);
```

<a name="parameters"></a>パラメーター
----------

*\*pNetworkIdentity* \[で、省略可能\]  
[ **HS\_ネットワーク\_IDENTITY** ](hs-network-identity.md)ネットワークを一意に識別する構造体。

*\*pSupportedSIMs* \[入力、出力\]  
1 つまたは複数の配列を指すポインター [ **HS\_プラグイン\_サポートされている\_SIM** ](hs-plugin-supported-sims.md)サポートされている Sim の一覧を格納する構造体。

<a name="return-value"></a>戻り値
------------

この関数は、プラグインを使用して通信するためにホストによって呼び出され、値は返されません。

<a name="remarks"></a>注釈
-------

場合、 *pNetworkIdentity*パラメーターが指定する必要があります指定されたネットワークに接続するために必要な SIM id のみで存在し、それ以外の場合、すべてのネットワークに接続するためには、Sim のリスト全体を指定する必要があります。

<a name="requirements"></a>要件
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>バージョン</p></td>
<td><p>Windows 10 Mobile</p></td>
</tr>
<tr class="even">
<td><p>Header</p></td>
<td>Hotspotoffloadplugin.h (Hotspotoffloadplugin.h を含む)</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>関連項目


[**HS\_ネットワーク\_IDENTITY**](hs-network-identity.md)

[**HS\_プラグイン\_サポートされている\_SIM**](hs-plugin-supported-sims.md)

 

 




