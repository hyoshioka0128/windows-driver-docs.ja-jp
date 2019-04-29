---
title: デバイス\_データ\_管理\_設定\_アクション
description: デバイス\_データ\_管理\_設定\_アクション定数は、デバイスのデータ セットの属性をドライバーによって実行される管理アクションの種類を指定します。
ms.assetid: cc64c7ad-7d1c-45c7-b236-a43e57086f8d
topic_type:
- apiref
api_name:
- DeviceDsmAction_None
- DeviceDsmAction_Trim
- DeviceDsmAction_Notification
- DeviceDsmAction_OffloadRead
- DeviceDsmAction_OffloadWrite
- DeviceDsmAction_Allocation
- DeviceDsmAction_Repair
- DeviceDsmAction_Scrub
- DeviceDsmAction_DrtQuery
- DeviceDsmAction_DrtClear
- DeviceDsmAction_DrtDisable
- DeviceDsmAction_NvCache_Change_Priority
- DeviceDsmAction_NvCache_Evict
api_location:
- ntddstor.h
api_type:
- HeaderDef
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: aee94d1032653ec6c8846556dcb0762d69c30db5
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63331736"
---
# <a name="devicedatamanagementsetaction"></a>デバイス\_データ\_管理\_設定\_アクション


A**デバイス\_データ\_管理\_設定\_アクション**定数は、デバイスのデータ セットの属性をドライバーによって実行される管理アクションの種類を指定します。

管理アクションがで指定された、 [**デバイス\_管理\_データ\_設定\_属性**](https://msdn.microsoft.com/library/windows/hardware/ff552527)のシステムのバッファーに含まれている構造体、[ **IOCTL\_ストレージ\_管理\_データ\_設定\_属性**](https://msdn.microsoft.com/library/windows/hardware/ff560573)要求。

<span id="DeviceDsmAction_None"></span><span id="devicedsmaction_none"></span><span id="DEVICEDSMACTION_NONE"></span>**DeviceDsmAction\_None**のみを目的として構造体の初期化の場合は 0。

<span id="DeviceDsmAction_Trim"></span><span id="devicedsmaction_trim"></span><span id="DEVICEDSMACTION_TRIM"></span>**DeviceDsmAction\_トリミング**1 ドライバーはトリム操作を実行します。

<span id="DeviceDsmAction_Notification"></span><span id="devicedsmaction_notification"></span><span id="DEVICEDSMACTION_NOTIFICATION"></span>**DeviceDsmAction\_通知**(2 |DeviceDsmActionFlag\_NonDestructive) ドライバーは、通知の操作を実行します。

このアクションの場合、 **ParameterBlockOffset**と**ParameterBlockLength**のメンバー、 [**デバイス\_管理\_データ\_設定\_属性**](https://msdn.microsoft.com/library/windows/hardware/ff552527)構造体は、通知操作のパラメーターを指定します。 これらのパラメーターとして書式設定、 [**デバイス\_DSM\_通知\_パラメーター** ](https://msdn.microsoft.com/library/windows/hardware/ff819207)構造体。

&gt; \[!注\] &gt; Windows 7 および Windows の以降のバージョンでサポートされています。

 

<span id="DeviceDsmAction_OffloadRead"></span><span id="devicedsmaction_offloadread"></span><span id="DEVICEDSMACTION_OFFLOADREAD"></span>**DeviceDsmAction\_OffloadRead** (3 |DeviceDsmActionFlag\_NonDestructive) ドライバーは、オフロードの読み取り操作を実行します。

このアクションの場合、 **ParameterBlockOffset**と**ParameterBlockLength**のメンバー、 [**デバイス\_管理\_データ\_設定\_属性**](https://msdn.microsoft.com/library/windows/hardware/ff552527)構造体は、オフロードのパラメーターの読み取り操作を指定します。 これらのパラメーターとして書式設定、 [**デバイス\_DSM\_オフロード\_読み取り\_パラメーター** ](https://msdn.microsoft.com/library/windows/hardware/hh439639)構造体。

&gt; \[!注\] &gt; Windows 8 および Windows の以降のバージョンでサポートされています。

 

<span id="DeviceDsmAction_OffloadWrite"></span><span id="devicedsmaction_offloadwrite"></span><span id="DEVICEDSMACTION_OFFLOADWRITE"></span>**DeviceDsmAction\_OffloadWrite**ドライバーは、4、オフロード書き込み操作です。

このアクションの場合、 **ParameterBlockOffset**と**ParameterBlockLength**のメンバー、 [**デバイス\_管理\_データ\_設定\_属性**](https://msdn.microsoft.com/library/windows/hardware/ff552527)構造体は、オフロードのパラメーターの書き込み操作を指定します。 これらのパラメーターとして書式設定、 [**デバイス\_DSM\_オフロード\_書き込み\_パラメーター** ](https://msdn.microsoft.com/library/windows/hardware/hh439644)構造体。

&gt; \[!注\] &gt; Windows 8 および Windows の以降のバージョンでサポートされています。

 

<span id="DeviceDsmAction_Allocation"></span><span id="devicedsmaction_allocation"></span><span id="DEVICEDSMACTION_ALLOCATION"></span>**DeviceDsmAction\_割り当て**(5 |DeviceDsmActionFlag\_NonDestructive) ドライバーはプロビジョニング操作の論理ブロックを実行します。

1 つの論理ブロックの範囲が指定された[**デバイス\_データ\_設定\_範囲**](https://msdn.microsoft.com/library/windows/hardware/ff552523)構造体。

&gt; \[!注\] &gt; Windows 8 および Windows の以降のバージョンでサポートされています。

 

<span id="DeviceDsmAction_Repair"></span><span id="devicedsmaction_repair"></span><span id="DEVICEDSMACTION_REPAIR"></span>**DeviceDsmAction\_修復**(6 |DeviceDsmActionFlag\_NonDestructive) ドライバーは、記憶域スペースの修復操作を実行します。

1 つの論理ブロックの範囲が指定された[**デバイス\_データ\_設定\_範囲**](https://msdn.microsoft.com/library/windows/hardware/ff552523)構造体。 修復のコピーの数がで指定された、**デバイス\_データ\_設定\_修復\_パラメーター**構造体で指定された入力バッファーにある、 **ParameterBlockOffset**のメンバー、 [**デバイス\_管理\_データ\_設定\_属性**](https://msdn.microsoft.com/library/windows/hardware/ff552527)構造体。

&gt; \[!注\] &gt; Windows 8 および Windows の以降のバージョンでサポートされています。

 

<span id="DeviceDsmAction_Scrub"></span><span id="devicedsmaction_scrub"></span><span id="DEVICEDSMACTION_SCRUB"></span>**DeviceDsmAction\_スクラブ**(7 |DeviceDsmActionFlag\_NonDestructive) ドライバーは、ストレージ スペース スクラブ操作を実行します。

1 つの論理ブロックの範囲が指定された[**デバイス\_データ\_設定\_範囲**](https://msdn.microsoft.com/library/windows/hardware/ff552523)構造体。

&gt; \[!注\] &gt; Windows 8 および Windows の以降のバージョンでサポートされています。

 

<span id="DeviceDsmAction_DrtQuery"></span><span id="devicedsmaction_drtquery"></span><span id="DEVICEDSMACTION_DRTQUERY"></span>**DeviceDsmAction\_DrtQuery** (8 |DeviceDsmActionFlag\_NonDestructive) ドライバーは、追跡、記憶域スペースのダーティ範囲に含まれている場合に、指定された論理ブロックの範囲とチェックのクエリが実行されます。 範囲の同期状態が返された、 **OperationStatus**のメンバー、 [**デバイス\_管理\_データ\_設定\_属性\_出力**](https://msdn.microsoft.com/library/windows/hardware/hh439656)構造体。

入力、1 つの論理ブロックの範囲が指定されて[**デバイス\_データ\_設定\_範囲**](https://msdn.microsoft.com/library/windows/hardware/ff552523)構造体。

&gt; \[!注\] &gt; Windows 8 および Windows の以降のバージョンでサポートされています。

 

<span id="DeviceDsmAction_DrtClear"></span><span id="devicedsmaction_drtclear"></span><span id="DEVICEDSMACTION_DRTCLEAR"></span>**DeviceDsmAction\_DrtClear** (9 |DeviceDsmActionFlag\_NonDestructive) の範囲のダーティ状態がクリアされます、ドライバー、指定された範囲の論理ブロックにします。

1 つの論理ブロックの範囲が指定された[**デバイス\_データ\_設定\_範囲**](https://msdn.microsoft.com/library/windows/hardware/ff552523)構造体。

&gt; \[!注\] &gt; Windows 8 および Windows の以降のバージョンでサポートされています。

 

<span id="DeviceDsmAction_DrtDisable"></span><span id="devicedsmaction_drtdisable"></span><span id="DEVICEDSMACTION_DRTDISABLE"></span>**DeviceDsmAction\_DrtDisable** (10 |DeviceDsmActionFlag\_NonDestructive) ドライバーがダーティの範囲を指定した論理ブロックの範囲の追跡を無効になります。

1 つの論理ブロックの範囲が指定された[**デバイス\_データ\_設定\_範囲**](https://msdn.microsoft.com/library/windows/hardware/ff552523)構造体。

&gt; \[!注\] &gt; Windows 8 および Windows の以降のバージョンでサポートされています。

 

<span id="DeviceDsmAction_NvCache_Change_Priority"></span><span id="devicedsmaction_nvcache_change_priority"></span><span id="DEVICEDSMACTION_NVCACHE_CHANGE_PRIORITY"></span>**DeviceDsmAction\_NvCache\_変更\_優先度**(14 |DeviceDsmActionFlag\_NonDestructive) ドライバーは論理ブロックの指定した範囲のキャッシュの優先順位を変更します。

新しいターゲットの優先順位が設定されて、**デバイス\_DSM\_NVCACHE\_変更\_優先度\_パラメーター**構造にある**ParameterBlockOffset**で[**デバイス\_管理\_データ\_設定\_属性**](https://msdn.microsoft.com/library/windows/hardware/ff552527)します。 1 つまたは複数の優先順位を変更する論理ブロック範囲が与えられます[**デバイス\_データ\_設定\_範囲**](https://msdn.microsoft.com/library/windows/hardware/ff552523)構造体。

**デバイス\_DSM\_NVCACHE\_変更\_優先度\_パラメーター**で定義されている*ntddstor.h*とは、次がありますメンバー:

<span id="Size"></span><span id="size"></span><span id="SIZE"></span>サイズ  
この構造体のサイズ。 設定**sizeof**(デバイス\_DSM\_NVCACHE\_変更\_優先度\_パラメーター)。

<span id="TargetPriority"></span><span id="targetpriority"></span><span id="TARGETPRIORITY"></span>TargetPriority  
論理ブロックの新しいターゲット優先順位は、指定された範囲です。

<span id="Resrved_3_"></span><span id="resrved_3_"></span><span id="RESRVED_3_"></span>Resrved\[3\]  
予約済みのバイト数。

&gt; \[!注\] &gt; Windows 8.1 と Windows の以降のバージョンでサポートされています。

 

<span id="DeviceDsmAction_NvCache_Evict"></span><span id="devicedsmaction_nvcache_evict"></span><span id="DEVICEDSMACTION_NVCACHE_EVICT"></span>**DeviceDsmAction\_NvCache\_削除**(15 |DeviceDsmActionFlag\_NonDestructive) ドライバーはキャッシュの中からデータを削除します。 すべてのデータを削除するには、デバイスを設定\_DSM\_フラグ\_全体\_データ\_設定\_範囲フラグ、**フラグ**のメンバー [ **デバイス\_管理\_データ\_設定\_属性**](https://msdn.microsoft.com/library/windows/hardware/ff552527)は含まれませんと[**デバイス\_データ\_設定\_範囲**](https://msdn.microsoft.com/library/windows/hardware/ff552523)構造体。

削除する特定の論理ブロックの範囲が 1 つまたは複数指定された[**デバイス\_データ\_設定\_範囲**](https://msdn.microsoft.com/library/windows/hardware/ff552523)構造体。

**DeviceDsmAction\_NvCache\_削除**アクションが同期的に実行します。 削除アクションが成功または失敗するまで、その他のアクションを処理はできません。 デバイスを使用してアプリケーションへの影響を制限するために各**DeviceDsmAction\_NvCache\_削除**発行アクションは、比較的小さなデータ範囲を含める必要があります。 10 MB を超えるし、理想的には 2 MB 未満であることが必要がありますされません。 これには、デバイス上のデータにアクセスするときにユーザー レベルのアプリケーションで顕著な遅延が発生こと可能性が最小化します。

&gt; \[!注\] &gt; Windows 8.1 と Windows の以降のバージョンでサポートされています。

 

<a name="remarks"></a>注釈
-------

ビットごとの場合**または**の**デバイス\_データ\_管理\_設定\_アクション**定数値、および**DeviceDsmActionFlag\_NonDestructive**フラグが実行されるため、指定の操作は非破壊的な。 ドライバーを安全に転送できるこのフラグが設定されている場合、 [ **IOCTL\_ストレージ\_管理\_データ\_設定\_属性**](https://msdn.microsoft.com/library/windows/hardware/ff560573)要求いても、スタックで [次へ] の下位のドライバーをドライバーは、指定されたアクションを処理しません。

&gt; \[!注\]&gt;を転送する前に、 [ **IOCTL\_ストレージ\_管理\_データ\_設定\_属性**](https://msdn.microsoft.com/library/windows/hardware/ff560573)要求と、ドライバーで指定されているデータ セットの範囲のブロックの通常の処理を実行します、 [**デバイス\_管理\_データ\_設定\_属性**](https://msdn.microsoft.com/library/windows/hardware/ff552527)構造体。 このブロックは**DataSetRangesOffset**として書式設定された 1 つ以上の連続したエントリで構成される[**デバイス\_データ\_設定\_範囲**](https://msdn.microsoft.com/library/windows/hardware/ff552523)構造体。 データ セットの範囲の長さ、(バイト単位) を設定、 **DataSetRangesLength**のメンバー**デバイス\_管理\_データ\_設定\_属性**します。

 

<a name="requirements"></a>要件
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p>バージョン</p></td>
<td align="left"><p>Windows 7 以降で利用できます。</p></td>
</tr>
<tr class="even">
<td align="left"><p>Header</p></td>
<td align="left">Ntddstor.h (include Ntddstor.h)</td>
</tr>
</tbody>
</table>

## <a name="span-idseealsospansee-also"></a><span id="see_also"></span>参照してください。


[**デバイス\_DSM\_通知\_パラメーター**](https://msdn.microsoft.com/library/windows/hardware/ff819207)

[**デバイス\_管理\_データ\_設定\_属性**](https://msdn.microsoft.com/library/windows/hardware/ff552527)

[**IOCTL\_ストレージ\_管理\_データ\_設定\_属性**](https://msdn.microsoft.com/library/windows/hardware/ff560573)

 

 






