---
title: HS_PLUGIN_SEND_KEEP_ALIVE 関数
description: HS_PLUGIN_SEND_KEEP_ALIVE 関数は、ネットワーク接続のキープ アライブ メッセージを送信するホストによって呼び出されます。 これは、dwKeepAliveTimeMins プラグインの HS_PLUGIN_PROFILE 構造体のメンバーで指定された頻度で呼び出されます。
ms.assetid: 1db91146-03bb-4513-9c1b-f0dbd5c941f5
keywords:
- Windows Vista 以降のドライバーをネットワーク typedef DWORD (WINAPI HS_PLUGIN_SEND_KEEP_ALIVE) 関数
ms.date: 07/31/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1bda0334afb1974b183400a7694c5b5bd21246e1
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56573570"
---
# <a name="hspluginsendkeepalive-function"></a>HS\_プラグイン\_送信\_保持\_ALIVE 関数

[!include[Wi-Fi Hotspot Offloading deprecation](wi-fi-hotspot-offloading-deprecation.md)]


**HS\_プラグイン\_送信\_保持\_ALIVE**関数は、ネットワーク接続のキープ アライブ メッセージの送信先ホストによって呼び出されます。 指定された頻度で呼び出される、 **dwKeepAliveTimeMins**のプラグインのメンバー [ **HS\_プラグイン\_プロファイル**](hs-plugin-profile.md)構造体.

<a name="syntax"></a>構文
------

```ManagedCPlusPlus
 typedef DWORD (WINAPI *HS_PLUGIN_SEND_KEEP_ALIVE)(
    
);
```

<a name="parameters"></a>パラメーター
----------

この関数には、パラメーターがありません。

**   

<a name="return-value"></a>戻り値
------------

この関数は、プラグインを使用して通信するためにホストによって呼び出され、値は返されません。

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


[**HS\_プラグイン\_プロファイル**](hs-plugin-profile.md)

 

 




