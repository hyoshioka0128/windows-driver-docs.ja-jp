---
title: HSPluginInitPlugin 関数
description: HSPluginInitPlugin 関数は、プラグイン DLL でエクスポートし、プラグインを初期化するために呼び出されます。
ms.assetid: db51267c-4f38-47bd-bde2-7b27a93dd2a7
keywords:
- Windows Vista 以降のドライバーをネットワーク HSPluginInitPlugin 関数
ms.date: 07/31/2017
ms.localizationpriority: medium
ms.openlocfilehash: eed897d595c0fa549e51dd86e6a445bcdcb02294
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56574846"
---
# <a name="hsplugininitplugin-function"></a>HSPluginInitPlugin 関数

[!include[Wi-Fi Hotspot Offloading deprecation](wi-fi-hotspot-offloading-deprecation.md)]


**HSPluginInitPlugin**関数がプラグイン DLL からエクスポートされ、プラグインを初期化します。

<a name="syntax"></a>構文
------

```ManagedCPlusPlus
DWORD HSPluginInitPlugin(
  _In_  HANDLE                hPluginContext,
  _In_  DWORD                 dwVerNumUsed,
  _In_  DWORD                 dwHostCapabilities,
  _In_  HS_DEVICE_IDENTITY    *pDeviceIdentity,
  _In_  HOTSPOT_HOST_HANDLERS *pHotspotHostHandlers,
  _Out_ HOTSPOT_PLUGIN_APIS   *pHotspotPluginAPIs,
  _Out_ HS_PLUGIN_PROFILE     *pPluginProfile
);
```

<a name="parameters"></a>パラメーター
----------

*hPluginContext* \[in\]  
ハンドルは、プラグインが保存してから、ハンドラー関数をホストを使用してホストに要求を行う必要があるときに必要である、ホストによって提供されます。

*dwVerNumUsed* \[in\]  
ホストの現在のバージョン番号。

*dwHostCapabilities* \[in\]  
ホストは、プラグインを提供できる機能の一覧を指定する値。 この値は、該当する機能フラグのビットごとの OR の組み合わせです。 機能フラグの詳細については、次を参照してください、 **HS\_フラグ\_機能\_\\*** で使用される定数[ **Wi-fi ホット スポットのオフロード定数**](wi-fi-hotspot-offloading-constants.md)。

**注**  ホストが、プラグインによって必要なすべての機能を提供していない場合、プラグインを初期化できません。

 

*\*pDeviceIdentity* \[in\]  
ポインターを[ **HS\_デバイス\_IDENTITY** ](hs-device-identity.md)デバイスの製造元とモデルに関する情報を含む構造体。

*\*pHotspotHostHandlers* \[in\]  
ポインターを[**ホット スポット\_ホスト\_ハンドラー** ](hotspot-host-handlers.md)ホット スポット ホスト ハンドラー関数のテーブルを含む構造体。 このテーブルには、ホット スポットのホストと通信するようにプラグインによって呼び出される関数へのポインターが含まれています。

*\*pHotspotPluginAPIs* \[アウト\]  
ポインター、 [**ホット スポット\_プラグイン\_API** ](hotspot-plugin-apis.md)ホット スポット プラグイン Api 関数のテーブルを含む構造体。 この表は、プラグインによって返され、プラグインを使用して通信するためにホストによって呼び出される関数へのポインターが含まれています。

*\*pPluginProfile* \[out\]  
ポインターを[ **HS\_プラグイン\_プロファイル**](hs-plugin-profile.md)プラグインについての情報を提供すると、プラグインによって返される構造体。

<a name="remarks"></a>コメント
-------

初期化中に、ホストは次のよう

-   プラグインのコンテキスト ハンドル
-   現在のバージョン番号
-   ホストは、プラグインを提供できる機能の一覧
-   により、プラグインは、ホストと通信できるホスト ハンドラー関数のテーブルへのポインター

プラグインは独自の関数のテーブルおよびへのポインターにポインターを返します、 [ **HS\_プラグイン\_プロファイル**](hs-plugin-profile.md)構造体。

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


[**Wi-fi ホット スポットの定数がオフロード**](wi-fi-hotspot-offloading-constants.md)

[**HS\_デバイス\_の ID**](hs-device-identity.md)

[**ホット スポット\_ホスト\_ハンドラー**](hotspot-host-handlers.md)

[**ホット スポット\_プラグイン\_API**](hotspot-plugin-apis.md)

[**HS\_プラグイン\_プロファイル**](hs-plugin-profile.md)

 

 




