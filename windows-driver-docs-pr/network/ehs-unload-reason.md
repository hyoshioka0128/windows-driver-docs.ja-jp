---
title: eHS_UNLOAD_REASON 列挙型
description: EHS_UNLOAD_REASON 列挙体は、アンロードするようにプラグインの理由を示します。
ms.assetid: 1e658dd3-f66d-4803-ad3c-84bfa1890a86
keywords:
- Windows Vista 以降のドライバーをネットワーク eHS_UNLOAD_REASON 列挙型
ms.date: 07/31/2017
ms.localizationpriority: medium
ms.openlocfilehash: ce0db9474ca5f9c714bc396503549020004714cd
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56535716"
---
# <a name="ehsunloadreason-enumeration"></a>eHS\_アンロード\_理由の列挙型

[!include[Wi-Fi Hotspot Offloading deprecation](wi-fi-hotspot-offloading-deprecation.md)]


**EHS\_アンロード\_理由**列挙型はアンロードするようにプラグインの理由を示します。

<a name="syntax"></a>構文
------

```ManagedCPlusPlus
typedef enum _eHS_UNLOAD_REASON { 
  HS_UNLOAD_REASON_NONE,
  HS_UNLOAD_REASON_PLUGN_INIT_FAILED,
  HS_UNLOAD_REASON_NO_NETWORKS_SUPPORTED,
  HS_UNLOAD_REASON_NO_PROVIDE_NAME_ID,
  HS_UNLOAD_REASON_ZERO_SIM_COUNT,
  HS_UNLOAD_REASON_DISPLAY_FLAG_BUT_NO_DISPLAY_STRING_ID,
  HS_UNLOAD_REASON_CUSTOM_REALM_FLAG_BUT_NO_REALM_STRING,
  HS_UNLOAD_REASON_DUPLICATE_PLUGIN_LOADED,
  HS_UNLOAD_REASON_RELOAD_REQUESTED_BY_PLUGIN,
  HS_UNLOAD_REASON_EXCEPTION_DURING_PLUGIN_CALL,
  HS_UNLOAD_REASON_EXCEPTION_IN_PLUGIN_HOST,
  HS_UNLOAD_REASON_ASYNC_INITIALIZATION_FAILED,
  HS_UNLOAD_REASON_UNSUPPORTED_AUTH_CAPABILITY_REQUESTED,
  HS_UNLOAD_REASON_FAILED_TO_LOAD_PROVIDER_NAME_STRING,
  HS_UNLOAD_REASON_FAILED_TO_LOAD_ADVANCED_PAGE_STRING,
  HS_UNLOAD_REASON_FAILED_TO_LOAD_NETWORK_NAME_STRING,
  HS_UNLOAD_REASON_FAILED_TO_CONFIGURE_HIDDEN_NETWORK,
  HS_UNLOAD_REASON_HIDDEN_NETWORK_ALREADY_CONFIGURED,
  HS_UNLOAD_REASON_FAILED_TO_QUERY_SIMS,
  HS_UNLOAD_REASON_PLUGIN_REQUIRED_SIM_NOT_PRESENT,
  HS_UNLOAD_REASON_SIM_CONFIG_CHANGED,
  HS_UNLOAD_REASON_WIFI_SWITCHED_OFF_IN_OS,
  HS_UNLOAD_REASON_MAX
} eHS_UNLOAD_REASON;
```

<a name="constants"></a>定数
---------

<a href="" id="hs-unload-reason-none"></a>**HS\_アンロード\_理由\_NONE**  
アンロード操作の特定の理由がありません。

<a href="" id="hs-unload-reason-plugn-init-failed"></a>**HS\_アンロード\_理由\_PLUGN\_INIT\_失敗**  
プラグインが正常に初期化できなかったため、アンロードされています。

<a href="" id="hs-unload-reason-no-networks-supported"></a>**HS\_アンロード\_理由\_いいえ\_ネットワーク\_サポートされています。**  
プラグインがアンロードされているため、プラグインの[ **HS\_プラグイン\_プロファイル**](hs-plugin-profile.md)構造体が有効な値を指定していなかった**dwNumNetworksSupported**.

<a href="" id="hs-unload-reason-no-provide-name-id"></a>**HS\_アンロード\_理由\_いいえ\_指定\_名前\_ID**  
プラグインがアンロードされているため、プラグインの[ **HS\_プラグイン\_プロファイル**](hs-plugin-profile.md)構造での文字列 ID を指定しなかった**dwProviderNameStringID**.

<a href="" id="hs-unload-reason-zero-sim-count"></a>**HS\_アンロード\_理由\_0\_SIM\_数**  
プラグインは、SIM カードがないためにアンロードされています。

<a href="" id="hs-unload-reason-display-flag-but-no-display-string-id"></a>**HS\_アンロード\_理由\_表示\_フラグ\_が\_いいえ\_表示\_文字列\_ID**  
プラグインがアンロードされているため、プラグインの[ **HS\_プラグイン\_プロファイル**](hs-plugin-profile.md)構造体は、HTTP または EAP SIM ベースの認証が必要ですが、の値が指定されませんでした**dwSupportedSIMCount します。**

<a href="" id="hs-unload-reason-custom-realm-flag-but-no-realm-string"></a>**HS\_アンロード\_理由\_カスタム\_レルム\_フラグ\_が\_いいえ\_レルム\_文字列**  
プラグインがアンロードされているため、プラグインの[ **HS\_プラグイン\_プロファイル**](hs-plugin-profile.md)指定された構造体、 **HS\_フラグ\_機能\_ネットワーク\_カスタム\_レルム**機能に対して有効な文字列はいえませんでしたが、 **szRealm**します。

<a href="" id="hs-unload-reason-duplicate-plugin-loaded"></a>**HS\_アンロード\_理由\_複製\_プラグイン\_LOADED**  
プラグインは、別のプラグインが同じ DLL を使用しているためにアンロードされています。

<a href="" id="hs-unload-reason-reload-requested-by-plugin"></a>**HS\_アンロード\_理由\_再読み込み\_要求された\_BY\_プラグイン**  
プラグインは、アンロード、および指定することによって再読み込みする必要があるため、プラグインがアンロードされている、 **HS\_UPDATE\_結果\_アクション\_再読み込み**ェマル[ **eHS\_UPDATE\_結果**](ehs-update-result.md)列挙体。

<a href="" id="hs-unload-reason-exception-during-plugin-call"></a>**HS\_アンロード\_理由\_例外\_に\_プラグイン\_を呼び出す**  
プラグインは、ホスト プロセスには、プラグインへの呼び出し中に例外が発生したためにアンロードされています。

<a href="" id="hs-unload-reason-exception-in-plugin-host"></a>**HS\_アンロード\_理由\_例外\_IN\_プラグイン\_ホスト**  
プラグインは、ホット スポットのホストには、例外が発生したためにアンロードされています。

<a href="" id="hs-unload-reason-async-initialization-failed"></a>**HS\_アンロード\_理由\_ASYNC\_初期化\_失敗**  
プラグインは、プラグインからの通知に登録する、ホット スポットのサービスが失敗したためにアンロードされています。

<a href="" id="hs-unload-reason-unsupported-auth-capability-requested"></a>**HS\_アンロード\_理由\_UNSUPPORTED\_AUTH\_機能\_要求**  
プラグインは、プラグインによって要求された認証機能のいずれも使用できないため、アンロードされています。

<a href="" id="hs-unload-reason-failed-to-load-provider-name-string"></a>**HS\_アンロード\_理由\_FAILED\_TO\_ロード\_プロバイダー\_名前\_文字列**  
ホット スポットのサービスがマップされていないため、プラグインがアンロードされている、 **dwProviderNameStringID**プラグインの指定された ID を文字列[ **HS\_プラグイン\_プロファイル**](hs-plugin-profile.md)に有効な文字列の構造体。

<a href="" id="hs-unload-reason-failed-to-load-advanced-page-string"></a>**HS\_アンロード\_理由\_FAILED\_TO\_ロード\_詳細\_ページ\_文字列**  
プラグインがアンロードされているため、プラグインの[ **HS\_プラグイン\_プロファイル**](hs-plugin-profile.md)構造体を指定する (省略可能) **dwAdvancedPageStringID**文字列 ID が有効な文字列にマップしなかった。

<a href="" id="hs-unload-reason-failed-to-load-network-name-string"></a>**HS\_アンロード\_理由\_FAILED\_TO\_ロード\_ネットワーク\_名前\_文字列**  
プラグインがアンロードされているため、プラグインの[ **HS\_プラグイン\_プロファイル**](hs-plugin-profile.md)構造体を指定する (省略可能) **dwGenericNetworkNameStringID**文字列の ID が有効な文字列にマップしなかった。

<a href="" id="hs-unload-reason-failed-to-configure-hidden-network"></a>**HS\_アンロード\_理由\_FAILED\_TO\_構成\_HIDDEN\_ネットワーク**  
プラグインには、非表示のネットワークが指定されているため、プラグインはアンロードされています (を使用して、 **HS\_フラグ\_機能\_ネットワーク\_型\_HIDDEN**機能) が、ホット スポットのサービスは、非表示のネットワークを構成できませんでした。

<a href="" id="hs-unload-reason-hidden-network-already-configured"></a>**HS\_UNLOAD\_REASON\_HIDDEN\_NETWORK\_ALREADY\_CONFIGURED**  
プラグインを使用して非表示のネットワークを指定するため、プラグインがアンロードされている、 **HS\_フラグ\_機能\_ネットワーク\_型\_HIDDEN**機能が、別のプラグインでは、非表示のネットワークのスロットは既に要求します。

<a href="" id="hs-unload-reason-failed-to-query-sims"></a>**HS\_アンロード\_理由\_FAILED\_TO\_クエリ\_SIM**  
プラグインがアンロードされているため、呼び出し[ **HS\_プラグイン\_クエリ\_サポートされている\_SIM** ](hs-plugin-query-supported-sims.md)できませんでした。

<a href="" id="hs-unload-reason-plugin-required-sim-not-present"></a>**HS\_アンロード\_理由\_プラグイン\_REQUIRED\_SIM\_いない\_存在**  
プラグインは、プラグインが必要な Sim は、デバイスに存在しないため、アンロードされています。

<a href="" id="hs-unload-reason-sim-config-changed"></a>**HS\_アンロード\_理由\_SIM\_CONFIG\_CHANGED**  
プラグインは、SIM 構成が変更をアンロードして再読み込み、プラグインを必要とするためにアンロードされています。

<a href="" id="hs-unload-reason-wifi-switched-off-in-os"></a>**HS\_アンロード\_理由\_WIFI\_交換\_OFF\_IN\_OS**  
プラグインは、OS で Wi-fi 機能がオフにされたため、アンロードされています。

<a href="" id="hs-unload-reason-max"></a>**HS\_アンロード\_理由\_MAX**  
範囲外の値を示します。

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
<td><p>Windows 10 Mobile</p></td>
</tr>
<tr class="even">
<td><p>Header</p></td>
<td>Hotspotoffloadplugin.h (Hotspotoffloadplugin.h を含む)</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>関連項目


[**HS\_プラグイン\_プロファイル**](hs-plugin-profile.md)

[**eHS\_UPDATE\_結果**](ehs-update-result.md)

[**HS\_プラグイン\_クエリ\_サポートされている\_SIM**](hs-plugin-query-supported-sims.md)

 

 




