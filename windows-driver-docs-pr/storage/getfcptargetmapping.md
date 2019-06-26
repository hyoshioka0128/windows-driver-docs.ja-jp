---
title: GetFcpTargetMapping 関数
description: GetFcpTargetMapping WMI メソッドは、これらの論理単位の一連のオペレーティング システムの論理ユニットを一意に識別する情報とファイバー チャネルのプロトコル (FCP) 識別子の間のマッピングを取得します。
ms.assetid: 2e4b3554-31de-4eaa-9228-844639a219d5
keywords:
- 記憶装置の GetFcpTargetMapping 関数
topic_type:
- apiref
api_name:
- GetFcpTargetMapping
api_location:
- Hbaapi.lib
- Hbaapi.dll
api_type:
- LibDef
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: a75f142476a2863f5b6aa7afb9cf70fd18a38696
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67378538"
---
# <a name="getfcptargetmapping-function"></a>GetFcpTargetMapping 関数


**GetFcpTargetMapping** WMI メソッドは、これらの論理単位の一連のオペレーティング システムの論理ユニットを一意に識別する情報とファイバー チャネルのプロトコル (FCP) 識別子の間のマッピングを取得します。

<a name="syntax"></a>構文
------

```ManagedCPlusPlus
void GetFcpTargetMapping(
   [in, HBAType("HBA_WWN")] uint8                    HbaPortWWN[8],
   [in] uint32                                       InEntryCount,
   [out, HBA_STATUS_QUALIFIERS] HBA_STATUS           HBAStatus,
   [out] uint32                                      TotalEntryCount,
   [out] uint32                                      OutEntryCount,
   [out, WmiSizeIs("OutEntryCount")] HBAFCPScsiEntry Entry[]
);
```

<a name="parameters"></a>パラメーター
----------

*HbaPortWWN\[8\]*    
ポート マッピングのテーブルが含まれるが取得するには世界中の名前。 この情報は、ミニポート ドライバーに配信される、 **HbaPortWWN**のメンバー、 [ **GetFcpTargetMapping\_IN** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/hbapiwmi/ns-hbapiwmi-_getfcptargetmapping_in)構造体。

*InEntryCount*   
WMI プロバイダーをレポートできるバインド エントリの数を示す、*エントリ*パラメーター。

*HBAStatus*   
に返された場合、操作の状態を格納します。 使用できる値とその説明の一覧は、次を参照してください。 [HBA\_状態](hba-status.md)します。 ミニポート ドライバーには、この情報が返されます、 **HBAStatus**のメンバー、 [ **GetFcpTargetMapping\_アウト**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/hbapiwmi/ns-hbapiwmi-_getfcptargetmapping_out)構造体。

*TotalEntryCount*   
HBA に関連付けられた永続的なバインドの合計数を示します。

*OutEntryCount*   
によって取得されたマッピングの合計数を示す、 **GetFcpTargetMapping**メソッド。 この値の場合に等しいまたはそれよりも少なくなります*TotalEntryCount*します。

*エントリ\[\]*    
型の構造体の配列[ **HBAFCPScsiEntry** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/hbapiwmi/ns-hbapiwmi-_hbafcpscsientry)オペレーティング システムとプロトコル (FCP) 識別子のファイバー チャネル HBA のバインディングを記述します。

<a name="return-value"></a>戻り値
------------

WMI メソッドには適用されません。

<a name="remarks"></a>注釈
-------

この WMI メソッドが属する、 [MSFC\_HBAFCPInfo WMI クラス](msfc-hbafcpinfo-wmi-class.md)します。

<a name="requirements"></a>要件
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p>対象プラットフォーム</p></td>
<td align="left">Desktop</td>
</tr>
<tr class="even">
<td align="left"><p>Header</p></td>
<td align="left">Hbapiwmi.h (Hbapiwmi.h、Hbaapi.h、Hbaapi.h など)</td>
</tr>
<tr class="odd">
<td align="left"><p>Library</p></td>
<td align="left">Hbaapi.lib</td>
</tr>
</tbody>
</table>

## <a name="span-idseealsospansee-also"></a><span id="see_also"></span>参照してください。


[HBA\_状態](hba-status.md)

[**GetFcpTargetMapping\_IN**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/hbapiwmi/ns-hbapiwmi-_getfcptargetmapping_in)

[**GetFcpTargetMapping\_OUT**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/hbapiwmi/ns-hbapiwmi-_getfcptargetmapping_out)

 

 






