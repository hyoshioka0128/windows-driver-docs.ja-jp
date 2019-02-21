---
title: HS_PLUGIN_CHECK_FOR_UPDATES 関数
description: HS_PLUGIN_CHECK_FOR_UPDATES 関数は、dwProfileUpdateTimeDays プラグインの HS_PLUGIN_PROFILE 構造体のメンバーで指定された頻度で構成の更新をチェックします。
ms.assetid: 8db3c237-d61b-4dca-b3a5-2fdaeb683b15
keywords:
- Windows Vista 以降のドライバーをネットワーク typedef DWORD (WINAPI HS_PLUGIN_CHECK_FOR_UPDATES) 関数
ms.date: 07/31/2017
ms.localizationpriority: medium
ms.openlocfilehash: dde9ec25b30f0b28c742229a2714d9b98733022c
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56530397"
---
# <a name="hsplugincheckforupdates-function"></a>HS\_プラグイン\_確認\_の\_更新関数

[!include[Wi-Fi Hotspot Offloading deprecation](wi-fi-hotspot-offloading-deprecation.md)]


**HS\_プラグイン\_確認\_の\_更新**関数で指定された頻度での構成の更新プログラムの確認、 **dwProfileUpdateTimeDays**のプラグインのメンバー [ **HS\_プラグイン\_プロファイル**](hs-plugin-profile.md)構造体。

<a name="syntax"></a>構文
------

```ManagedCPlusPlus
 typedef DWORD (WINAPI *HS_PLUGIN_CHECK_FOR_UPDATES)(
    
);
```

<a name="parameters"></a>パラメーター
----------

この関数には、パラメーターがありません。

**   

<a name="return-value"></a>戻り値
------------

この関数は、プラグインを使用して通信するためにホストによって呼び出され、値は返されません。

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


[**HS\_プラグイン\_プロファイル**](hs-plugin-profile.md)

 

 




