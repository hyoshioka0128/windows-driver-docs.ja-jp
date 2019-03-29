---
title: HS_HOST_UPDATE_CONFIGURATION_COMPLETION 関数
description: HS_HOST_UPDATE_CONFIGURATION_COMPLETION 関数は、更新プログラムを確認する要求の成否を示します。
ms.assetid: 7e9eda04-db8e-4181-90e3-8716a99429a8
keywords:
- Windows Vista 以降のドライバーをネットワーク typedef DWORD (WINAPI HS_HOST_UPDATE_CONFIGURATION_COMPLETION) 関数
ms.date: 07/31/2017
ms.localizationpriority: medium
ms.openlocfilehash: 67135e7348bfe8a3ee2c58b932c98c54f5fad319
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56569931"
---
# <a name="hshostupdateconfigurationcompletion-function"></a>HS\_ホスト\_UPDATE\_構成\_完了関数

[!include[Wi-Fi Hotspot Offloading deprecation](wi-fi-hotspot-offloading-deprecation.md)]


**HS\_ホスト\_UPDATE\_構成\_完了**関数は、更新プログラムを確認する要求の成否を示します。

<a name="syntax"></a>構文
------

```ManagedCPlusPlus
 typedef DWORD (WINAPI *HS_HOST_UPDATE_CONFIGURATION_COMPLETION)(
  _In_ HANDLE            hPluginContext,
  _In_ eHS_UPDATE_RESULT UpdateResult
);
```

<a name="parameters"></a>パラメーター
----------

*hPluginContext* \[in\]  
この関数を呼び出すプラグインのコンテキスト ハンドル。

*UpdateResult* \[で\]  
[ **EHS\_UPDATE\_結果**](ehs-update-result.md)更新プログラムを確認要求の結果を示す列挙値。

<a name="return-value"></a>戻り値
------------

この関数は、ホストと通信するようにプラグインによって呼び出され、値は返されません。

<a name="remarks"></a>コメント
-------

このプラグインは、以前の呼び出しの結果のホストに通知するには、この関数を呼び出す必要があります[ **HS\_プラグイン\_確認\_の\_更新**](hs-plugin-check-for-updates.md)。

<a name="requirements"></a>必要条件
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


[**eHS\_UPDATE\_結果**](ehs-update-result.md)

[**HS\_プラグイン\_確認\_の\_更新プログラム**](hs-plugin-check-for-updates.md)

 

 




