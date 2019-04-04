---
title: HOTSPOT_HOST_HANDLERS 構造体
description: HOTSPOT_HOST_HANDLERS 構造体には、ホット スポット ホスト ハンドラー関数のテーブルが含まれています。
ms.assetid: b381e471-7713-401a-b3fa-eae1801b0e81
keywords:
- Windows Vista 以降のドライバーをネットワーク HOTSPOT_HOST_HANDLERS が構造体します。
- Windows Vista 以降のドライバーをネットワーク PHOTSPOT_HOST_HANDLERS 構造体ポインター
ms.date: 07/31/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6fceb6db6fb58d26326ffa84bdd5140fbe985901
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56535687"
---
# <a name="hotspothosthandlers-structure"></a>ホット スポット\_ホスト\_ハンドラー構造体

[!include[Wi-Fi Hotspot Offloading deprecation](wi-fi-hotspot-offloading-deprecation.md)]


**ホット スポット\_ホスト\_ハンドラー**構造体には、ホット スポット ホスト ハンドラー関数のテーブルが含まれています。 この関数のテーブルは、プラグインに渡されるときに[ **HSPluginInitPlugin** ](hsplugininitplugin.md)はそれを初期化するために呼び出されます。 テーブルには、ホット スポットのホストと通信するようにプラグインによって呼び出される関数が含まれています。

<a name="syntax"></a>構文
------

```ManagedCPlusPlus
typedef struct _HOTSPOT_HOST_HANDLERS {
  HS_HOST_ALLOCATE_MEMORY                          HSHostAllocateMemory;
  HS_HOST_FREE_MEMORY                              HSHostFreeMemory;
  HS_HOST_POST_CONNECT_AUTH_COMPLETION             HSHostPostConnectAuthCompletion;
  HS_HOST_SEND_KEEP_ALIVE_COMPLETION               HSHostSendKeepAliveCompletion;
  HS_HOST_UPDATE_CONFIGURATION_COMPLETION          HSHostUpdateConfigurationCompletion;
  HS_HOST_SEND_USER_MESSAGE                        HSHostSendUserMessage;
} HOTSPOT_HOST_HANDLERS, *PHOTSPOT_HOST_HANDLERS;
```

<a name="members"></a>Members
-------

**HSHostAllocateMemory**  
省略可能なメモリ管理のハンドラー。

プラグインは、プラグインによって必要なメモリを割り当てることによって呼び出される関数へのハンドルします。 詳細については、[ **HS\_ホスト\_ALLOCATE\_メモリ**](hs-host-allocate-memory.md)を参照してください。

**HSHostFreeMemory**  
省略可能なメモリ管理のハンドラー。

割り当てられているすべてのメモリを解放するプラグインによって呼び出される関数へのハンドルへの呼び出しによって以前[ **HS\_ホスト\_ALLOCATE\_メモリ**](hs-host-allocate-memory.md)します。 詳細については、[ **HS\_ホスト\_FREE\_メモリ**](hs-host-free-memory.md)を参照してください。

**HSHostPostConnectAuthCompletion**  
接続処理のハンドラーが必要です。

次の Wi-fi 接続のセットアップを層 2 では、認証の試行の結果の成功または失敗の状態を示すプラグインによって呼び出される関数へのハンドルします。 詳細については、[ **HS\_プラグイン\_開始\_POST\_CONNECT\_AUTH**](hs-plugin-start-post-connect-auth.md)を参照してください。

**HSHostSendKeepAliveCompletion**  
省略可能な定期的な要求。

Keep Alive の送信要求の結果の成功または失敗の状態を示すプラグインによって呼び出される関数へのハンドルします。 詳細については、[ **HS\_プラグイン\_送信\_保持\_ALIVE**](hs-plugin-send-keep-alive.md)を参照してください。

**HSHostUpdateConfigurationCompletion**  
省略可能な定期的な要求。

成功した場合または更新プログラムの確認の呼び出しの失敗を示すプラグインによって呼び出される関数へのハンドルします。 詳細については、[ **HS\_プラグイン\_確認\_の\_更新**](hs-plugin-check-for-updates.md)を参照してください。

**HSHostSendUserMessage**  
省略可能な定期的な要求。

ユーザーとの通信のために呼び出される関数へのハンドルします。 詳細については、[ **HS\_ホスト\_送信\_ユーザー\_メッセージ**](hs-host-send-user-message.md)を参照してください。

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


[**HSPluginInitPlugin**](hsplugininitplugin.md)

[**HS\_ホスト\_ALLOCATE\_メモリ**](hs-host-allocate-memory.md)

[**HS\_ホスト\_FREE\_メモリ**](hs-host-free-memory.md)

[**HS\_プラグイン\_開始\_POST\_CONNECT\_認証**](hs-plugin-start-post-connect-auth.md)

[**HS\_プラグイン\_送信\_保持\_ALIVE**](hs-plugin-send-keep-alive.md)

[**HS\_プラグイン\_確認\_の\_更新プログラム**](hs-plugin-check-for-updates.md)

[**HS\_ホスト\_送信\_ユーザー\_メッセージ**](hs-host-send-user-message.md)

 

 




