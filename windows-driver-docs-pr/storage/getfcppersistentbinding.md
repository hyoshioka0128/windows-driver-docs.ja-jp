---
title: GetFcpPersistentBinding 関数
description: GetFcpPersistentBinding メソッドは、論理ユニットのファイバー チャネル プロトコル (FCP) 識別子に、論理ユニットを識別するために、オペレーティング システムを使用する情報をマップする HBA のミニポート ドライバーを使用するバインディングを取得します。
ms.assetid: ee675022-51f7-4b81-863c-ee608b0284b0
keywords:
- 記憶装置の GetFcpPersistentBinding 関数
topic_type:
- apiref
api_name:
- GetFcpPersistentBinding
api_location:
- Hbaapi.lib
- Hbaapi.dll
api_type:
- LibDef
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 9d29af748b40b47e5143c81f5b006a4d714d90f7
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67378540"
---
# <a name="getfcppersistentbinding-function"></a>GetFcpPersistentBinding 関数


**GetFcpPersistentBinding**メソッドは、オペレーティング システムをファイバー チャネルのプロトコル (FCP) 識別子を論理ユニットを識別するために使用する情報をマップする HBA のミニポート ドライバーを使用するバインディングを取得します論理ユニットです。

<a name="syntax"></a>構文
------

```ManagedCPlusPlus
void GetFcpPersistentBinding(
   [in] uint32                                          InEntryCount,
   [out, HBA_STATUS_QUALIFIERS] HBA_STATUS              HBAStatus,
   [out] uint32                                         TotalEntryCount,
   [out] uint32                                         OutEntryCount,
   [out, WmiSizeIs("OutEntryCount")] HBAFCPBindingEntry Entry[]
);
```

<a name="parameters"></a>パラメーター
----------

*InEntryCount*   
WMI プロバイダーをレポートできるバインド エントリの数を示す、*エントリ*パラメーター。

*HBAStatus*   
に返された場合、操作の状態を格納します。 使用できる値とその説明の一覧は、次を参照してください。 [HBA\_状態](hba-status.md)します。 ミニポート ドライバーには、この情報が返されます、 **HBAStatus**のメンバー、 [ **GetFcpPersistentBinding\_アウト**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/hbapiwmi/ns-hbapiwmi-_getfcppersistentbinding_out)構造体。

*TotalEntryCount*   
HBA に関連付けられた永続的なバインドの合計数を示します。

*OutEntryCount*   
によって取得された永続的なバインドの合計数を示す、 **GetFcpPersistentBinding**メソッド。 この値の場合に等しいまたはそれよりも少なくなります*TotalEntryCount*します。

*エントリ\[\]*    
型の構造体の配列[ **HBAFCPBindingEntry** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/hbapiwmi/ns-hbapiwmi-_hbafcpbindingentry)オペレーティング システムとプロトコル (FCP) 識別子のファイバー チャネル HBA のバインディングを記述します。

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


[**GetFcpPersistentBinding\_IN**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/hbapiwmi/ns-hbapiwmi-_getfcppersistentbinding_in)

[**GetFcpPersistentBinding\_OUT**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/hbapiwmi/ns-hbapiwmi-_getfcppersistentbinding_out)

[**HBAFCPBindingEntry**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/hbapiwmi/ns-hbapiwmi-_hbafcpbindingentry)

 

 






