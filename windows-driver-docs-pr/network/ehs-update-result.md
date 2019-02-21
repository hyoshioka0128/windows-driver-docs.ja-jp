---
title: eHS_UPDATE_RESULT 列挙型
description: EHS_UPDATE_RESULT 列挙型では、「更新プログラムの確認」要求の結果を示します。
ms.assetid: 7b9b8ddc-3101-466a-9640-b936f6d14de4
keywords:
- Windows Vista 以降のドライバーをネットワーク eHS_UPDATE_RESULT 列挙型
ms.date: 07/31/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5e21d5a357a50a80211922019781688770539a1b
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56548595"
---
# <a name="ehsupdateresult-enumeration"></a>eHS\_UPDATE\_結果の列挙型

[!include[Wi-Fi Hotspot Offloading deprecation](wi-fi-hotspot-offloading-deprecation.md)]


**EHS\_UPDATE\_結果**列挙型を「更新プログラムの確認」要求の結果を示します。

<a name="syntax"></a>構文
------

```ManagedCPlusPlus
typedef enum _eHS_UPDATE_RESULT { 
  HS_UPDATE_RESULT_SUCCESS,
  HS_UPDATE_RESULT_ACTION_RECONNECT,
  HS_UPDATE_RESULT_ACTION_RELOAD,
  HS_UPDATE_RESULT_MAX
} eHS_UPDATE_RESULT;
```

<a name="constants"></a>定数
---------

<a href="" id="hs-update-result-success"></a>**HS\_UPDATE\_結果\_成功**  
更新が成功したことを示します。

<a href="" id="hs-update-result-action-reconnect"></a>**HS\_UPDATE\_結果\_アクション\_再接続**  
更新要求の結果には、サービスを切断および再接続が必要です。

<a href="" id="hs-update-result-action-reload"></a>**HS\_UPDATE\_結果\_アクション\_再読み込み**  
更新要求の結果では、サービスをアンロードし、プラグインを再読み込みする必要があります。

<a href="" id="hs-update-result-max"></a>**HS\_UPDATE\_結果\_MAX**  
範囲外の値を示します。

<a name="remarks"></a>注釈
-------

プラグインが使用してホット スポットのプラグインのホストにこの列挙値を渡す、 [ **HS\_ホスト\_UPDATE\_構成\_完了**](hs-host-update-configuration-completion.md)関数の呼び出しの結果のホット スポットのプラグインのホストに通知するために使用[ **HS\_プラグイン\_確認\_の\_更新**](hs-plugin-check-for-updates.md).

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


[**HS\_ホスト\_UPDATE\_構成\_完了**](hs-host-update-configuration-completion.md)

[**HS\_プラグイン\_確認\_の\_更新プログラム**](hs-plugin-check-for-updates.md)

 

 




