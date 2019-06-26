---
title: HS_PLUGIN_CELLULAR_EXCEPTION_HOSTS 構造体
description: HS_PLUGIN_CELLULAR_EXCEPTION_HOSTS 構造体には、プラグインが携帯電話のベアラーを介した認証プロセス中にのみ接続を必要とするホストの一覧が含まれています。
ms.assetid: cc7ad05b-d03b-463a-9d22-1982aee882e8
keywords:
- Windows Vista 以降のドライバーをネットワーク HS_PLUGIN_CELLULAR_EXCEPTION_HOSTS が構造体します。
- Windows Vista 以降のドライバーをネットワーク PHS_PLUGIN_CELLULAR_EXCEPTION_HOSTS 構造体ポインター
ms.date: 07/31/2017
ms.localizationpriority: medium
ms.openlocfilehash: bb3c47df78b984ea70990ce97e121944788b2aba
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67368612"
---
# <a name="hsplugincellularexceptionhosts-structure"></a>HS\_プラグイン\_移動体通信\_例外\_ホスト構造体

[!include[Wi-Fi Hotspot Offloading deprecation](wi-fi-hotspot-offloading-deprecation.md)]


**HS\_プラグイン\_移動体通信\_例外\_ホスト**構造体には、プラグインが中にのみ移動体通信ベアラーを介した接続を必要とするホストの一覧が含まれています、認証プロセスです。 これは、プラグインが要求できるオプションの機能です。 詳細については、次を参照してください。 [ **HS\_プラグイン\_クエリ\_移動体通信\_例外\_ホスト**](hs-plugin-query-cellular-exception-hosts.md)します。

<a name="syntax"></a>構文
------

```ManagedCPlusPlus
typedef struct _HS_PLUGIN_CELLULAR_EXCEPTION_HOSTS {
  DWORD               dwCount;
  HS_PLUGIN_HOST_NAME pExceptions[*];
  HS_PLUGIN_HOST_NAME pExceptions[1];
} HS_PLUGIN_CELLULAR_EXCEPTION_HOSTS, *PHS_PLUGIN_CELLULAR_EXCEPTION_HOSTS;
```

<a name="members"></a>メンバー
-------

**dwCount**  
リスト内のホスト名の数が指す**pExceptions**します。

**pExceptions**  
MIDL を使用する場合に使用されます。 サイズは、一意である (dwCount) です。

ホスト名の一覧へのポインター。

**pExceptions**  
MIDL が利用されていない場合に使用します。

ホスト名の一覧へのポインター。

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


[**HS\_プラグイン\_クエリ\_移動体通信\_例外\_ホスト**](hs-plugin-query-cellular-exception-hosts.md)

[Microsoft インターフェイス定義言語](https://docs.microsoft.com/windows/desktop/Midl/midl-start-page)

 

 




