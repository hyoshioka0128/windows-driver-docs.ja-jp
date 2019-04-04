---
title: HS_PLUGIN_PROFILE 構造体
description: HS_PLUGIN_PROFILE 構造体は、プラグインについての情報を提供します。 この構造体のメンバーは、ホストによって呼び出される HSPluginInitPlugin 関数の実行中に、プラグインによって設定されます。
ms.assetid: 0c4f7088-737e-479a-b46e-a55e96719775
keywords:
- Windows Vista 以降のドライバーをネットワーク HS_PLUGIN_PROFILE 構造体
- Windows Vista 以降のドライバーをネットワーク PHS_PLUGIN_PROFILE 構造体ポインター
ms.date: 07/31/2017
ms.localizationpriority: medium
ms.openlocfilehash: d3b5e46347b4008af7c7e14926e9ffa32a9ae982
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56581544"
---
# <a name="hspluginprofile-structure"></a>HS\_プラグイン\_プロファイルの構造

[!include[Wi-Fi Hotspot Offloading deprecation](wi-fi-hotspot-offloading-deprecation.md)]


**HS\_プラグイン\_プロファイル**構造は、プラグインについての情報を提供します。 この構造体のメンバーは、の実行中に、プラグインによって設定されます、 [ **HSPluginInitPlugin** ](hsplugininitplugin.md)ホストによって呼び出される関数。

<a name="syntax"></a>構文
------

```ManagedCPlusPlus
typedef struct _HS_PLUGIN_PROFILE {
  DWORD dwPluginCapabilities;
  DWORD dwNumNetworksSupported;
  DWORD dwProviderNameStringID;
  DWORD dwGenericNetworkNameStringID;
  DWORD dwAdvancedPageStringID;
  DWORD dwProfileUpdateTimeDays;
  WCHAR szRealm[HS_CONST_MAX_REALM_LENGTH+1];
  DWORD dwSupportedSIMCount;
} HS_PLUGIN_PROFILE, *PHS_PLUGIN_PROFILE;
```

<a name="members"></a>メンバー
-------

**dwPluginCapabilities**  
必須。

使用可能なサブセット**HS\_フラグ\_機能\_ネットワーク\_\\*** 値。 ホット スポットのホスト機能の詳細については、[ **Wi-fi ホット スポットのオフロード定数**](wi-fi-hotspot-offloading-constants.md)を参照してください。

**dwNumNetworksSupported**  
必須。

このプラグインでサポートされているネットワークの合計数。

**dwProviderNameStringID**  
必須。

ユーザーに表示されるネットワーク プロバイダーの名前。 文字列の最大サイズ = 最大\_プロバイダー\_名前\_長さ。

**dwGenericNetworkNameStringID**  
任意。

ネットワーク名です。 文字列の最大サイズ = 最大\_ネットワーク\_表示\_名前\_長さ。

**dwAdvancedPageStringID**  
任意。

文字列の最大サイズ = HS\_CONST\_最大\_詳細\_ページ\_文字列\_長さ。

**dwProfileUpdateTimeDays**  
任意。

HS 以上にする必要があります\_CONST\_MIN\_プロファイル\_UPDATE\_時間\_IN\_日。

**szRealm**  
場合に、必ず HS\_フラグ\_機能\_ネットワーク\_カスタム\_領域を設定します。

ネットワーク固有の領域の値。

**dwSupportedSIMCount**  
リストのサイズが指す**pSupported Sim**します。

<a name="requirements"></a>必要条件
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

[**Wi-fi ホット スポットの定数がオフロード**](wi-fi-hotspot-offloading-constants.md)

 

 




