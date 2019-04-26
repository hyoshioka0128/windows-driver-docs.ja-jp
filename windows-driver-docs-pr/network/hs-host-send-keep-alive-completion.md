---
title: HS_HOST_SEND_KEEP_ALIVE_COMPLETION 関数
description: HS_HOST_SEND_KEEP_ALIVE_COMPLETION 関数は、ネットワーク送信キープ アライブ メッセージの要求の成否を示します。
ms.assetid: 19fc1210-2c3a-46ca-96fb-dccafa9e9eef
keywords:
- Windows Vista 以降のドライバーをネットワーク typedef DWORD (WINAPI HS_HOST_SEND_KEEP_ALIVE_COMPLETION) 関数
ms.date: 07/31/2017
ms.localizationpriority: medium
ms.openlocfilehash: c1d73877e83584b147e1159ef5b025a5dc1ed623
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63349653"
---
# <a name="hshostsendkeepalivecompletion-function"></a>HS\_ホスト\_送信\_保持\_ALIVE\_完了関数

[!include[Wi-Fi Hotspot Offloading deprecation](wi-fi-hotspot-offloading-deprecation.md)]


**HS\_ホスト\_送信\_保持\_ALIVE\_完了**関数は、ネットワーク送信キープ アライブ メッセージの要求の成否を示します。

<a name="syntax"></a>構文
------

```ManagedCPlusPlus
 typedef DWORD (WINAPI *HS_HOST_SEND_KEEP_ALIVE_COMPLETION)(
  _In_ HANDLE hPluginContext,
  _In_ DWORD  dwResult
);
```

<a name="parameters"></a>パラメーター
----------

*hPluginContext* \[in\]  
この関数を呼び出すプラグインのコンテキスト ハンドル。

*dwResult* \[in\]  
結果コード。

<a name="return-value"></a>戻り値
------------

この関数は、ホストと通信するようにプラグインによって呼び出され、値は返されません。

<a name="remarks"></a>注釈
-------

このプラグインは、以前の呼び出しの結果のホストに通知するには、この関数を呼び出す必要があります[ **HS\_プラグイン\_送信\_保持\_ALIVE**](hs-plugin-send-keep-alive.md)します。

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


[**HS\_プラグイン\_送信\_保持\_ALIVE**](hs-plugin-send-keep-alive.md)

 

 




