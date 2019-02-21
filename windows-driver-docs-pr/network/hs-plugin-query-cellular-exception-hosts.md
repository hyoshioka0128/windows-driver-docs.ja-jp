---
title: HS_PLUGIN_QUERY_CELLULAR_EXCEPTION_HOSTS 関数
description: HS_PLUGIN_QUERY_CELLULAR_EXCEPTION_HOSTS 関数は、プラグインは、認証プロセスの一環として移動体通信で接続する必要があるホストの一覧を照会します。
ms.assetid: 7f38f146-a637-4ec3-8610-ea4934c4a57a
keywords:
- Windows Vista 以降のドライバーをネットワーク typedef DWORD (WINAPI HS_PLUGIN_QUERY_CELLULAR_EXCEPTION_HOSTS) 関数
ms.date: 07/31/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3d0658d58919e081417e17c00603ac29a7d962dd
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56536243"
---
# <a name="hspluginquerycellularexceptionhosts-function"></a>HS\_プラグイン\_クエリ\_移動体通信\_例外\_ホスト関数

[!include[Wi-Fi Hotspot Offloading deprecation](wi-fi-hotspot-offloading-deprecation.md)]


**HS\_プラグイン\_クエリ\_移動体通信\_例外\_ホスト**関数の一部として、携帯電話上に接続する必要があります、プラグインのホストの一覧を照会します。その認証のプロセス。

<a name="syntax"></a>構文
------

```ManagedCPlusPlus
 typedef DWORD (WINAPI *HS_PLUGIN_QUERY_CELLULAR_EXCEPTION_HOSTS)(
  _Inout_ HS_PLUGIN_CELLULAR_EXCEPTION_HOSTS *pExceptionsList
);
```

<a name="parameters"></a>パラメーター
----------

*\*pExceptionsList* \[入力、出力\]  
[ **HS\_プラグイン\_移動体通信\_例外\_ホスト**](hs-plugin-cellular-exception-hosts.md)携帯電話のホスト名の一覧を含む構造体。

<a name="return-value"></a>戻り値
------------

この関数は、プラグインを使用して通信するためにホストによって呼び出され、値は返されません。

<a name="remarks"></a>注釈
-------

プラグインを設定する場合にのみ、この関数が呼び出されます、 **dwNumCellularExceptions**のフィールドの[ **HS\_プラグイン\_プロファイル**](hs-plugin-profile.md)値0 より大きい。

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


[**HS\_プラグイン\_移動体通信\_例外\_ホスト**](hs-plugin-cellular-exception-hosts.md)

[**HS\_プラグイン\_プロファイル**](hs-plugin-profile.md)

 

 




