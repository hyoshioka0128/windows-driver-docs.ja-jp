---
title: HS_PLUGIN_DEINIT 関数
description: HS_PLUGIN_DEINIT 関数は、それがアンロードされるプラグインを通知するホストによって呼び出されます。
ms.assetid: 3bb0ad85-91db-476e-b347-0fa8ed4ae24e
keywords:
- Windows Vista 以降のドライバーをネットワーク typedef DWORD (WINAPI HS_PLUGIN_DEINIT) 関数
ms.date: 07/31/2017
ms.localizationpriority: medium
ms.openlocfilehash: e9fb4383d35237faeb57585798523f60983256e9
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56537393"
---
# <a name="hsplugindeinit-function"></a>HS\_プラグイン\_DEINIT 関数

[!include[Wi-Fi Hotspot Offloading deprecation](wi-fi-hotspot-offloading-deprecation.md)]


**HS\_プラグイン\_DEINIT**関数は、それがアンロードされるプラグインを通知するホストによって呼び出されます。

<a name="syntax"></a>構文
------

```ManagedCPlusPlus
 typedef DWORD (WINAPI *HS_PLUGIN_DEINIT)(
  _In_ eHS_UNLOAD_REASON UnloadReason
);
```

<a name="parameters"></a>パラメーター
----------

*UnloadReason* \[in\]  
[ **EHS\_アンロード\_理由**](ehs-unload-reason.md)アンロードの理由を示す列挙値。

<a name="return-value"></a>戻り値
------------

この関数は、プラグインを使用して通信するためにホストによって呼び出され、値は返されません。

<a name="remarks"></a>注釈
-------

受け取る通知することがアンロードされると、プラグインが、現在のアクティビティを完了、必要な場合に、状態を保存する必要があります。

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


[**eHS\_アンロード\_理由**](ehs-unload-reason.md)

 

 




