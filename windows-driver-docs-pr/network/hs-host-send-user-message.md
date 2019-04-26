---
title: HS_HOST_SEND_USER_MESSAGE 関数
description: HS_HOST_SEND_USER_MESSAGE 関数は、ユーザーとの通信に呼び出されます。 メッセージの内容は、ホット スポットのオフロード サービスに渡されるカスタムの UI 表示文字列に含まれています。
ms.assetid: c4ab1fda-18eb-44e4-aa64-f7b37b4147a3
keywords:
- Windows Vista 以降のドライバーをネットワーク typedef DWORD (WINAPI HS_HOST_SEND_USER_MESSAGE) 関数
ms.date: 07/31/2017
ms.localizationpriority: medium
ms.openlocfilehash: af7f445d32f21ab001fe945f86b5d80aa822b0c5
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63349630"
---
# <a name="hshostsendusermessage-function"></a>HS\_ホスト\_送信\_ユーザー\_メッセージ関数

[!include[Wi-Fi Hotspot Offloading deprecation](wi-fi-hotspot-offloading-deprecation.md)]


**HS\_ホスト\_送信\_ユーザー\_メッセージ**関数は、ユーザーとの通信に呼び出されます。 メッセージの内容は、ホット スポットのオフロード サービスに渡されるカスタムの UI 表示文字列に含まれています。

<a name="syntax"></a>構文
------

```ManagedCPlusPlus
 typedef DWORD (WINAPI *HS_HOST_SEND_USER_MESSAGE)(
  _In_ HANDLE hPluginContext,
  _In_ DWORD  dwConnectionId,
  _In_ DWORD  dwStringID
);
```

<a name="parameters"></a>パラメーター
----------

*hPluginContext* \[in\]  
この関数を呼び出すプラグインのコンテキスト ハンドル。

*dwConnectionId* \[in\]  
ネットワーク接続の一意の識別子。

*dwStringID* \[in\]  
インデックスとして使用する文字列テーブルにメッセージが格納されている文字列 ID。

<a name="return-value"></a>戻り値
------------

この関数は、ホストと通信するようにプラグインによって呼び出され、値は返されません。

<a name="remarks"></a>注釈
-------

ホット スポットのプラグインでは、文字列テーブルに、メッセージを格納します。 プラグインは、文字列 Id を適切な文字列の読み込みを有効にする、ホット スポットのオフロード サービスに渡す必要があります。

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

 

 




