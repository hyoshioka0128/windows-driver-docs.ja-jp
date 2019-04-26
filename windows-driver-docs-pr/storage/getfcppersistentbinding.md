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
ms.openlocfilehash: e672db16988d010505521263f186a24beafdbdeb
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63354080"
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
に返された場合、操作の状態を格納します。 使用できる値とその説明の一覧は、次を参照してください。 [HBA\_状態](hba-status.md)します。 ミニポート ドライバーには、この情報が返されます、 **HBAStatus**のメンバー、 [ **GetFcpPersistentBinding\_アウト**](https://msdn.microsoft.com/library/windows/hardware/ff554936)構造体。

*TotalEntryCount*   
HBA に関連付けられた永続的なバインドの合計数を示します。

*OutEntryCount*   
によって取得された永続的なバインドの合計数を示す、 **GetFcpPersistentBinding**メソッド。 この値の場合に等しいまたはそれよりも少なくなります*TotalEntryCount*します。

*エントリ\[\]*   
型の構造体の配列[ **HBAFCPBindingEntry** ](https://msdn.microsoft.com/library/windows/hardware/ff556034)オペレーティング システムとプロトコル (FCP) 識別子のファイバー チャネル HBA のバインディングを記述します。

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


[**GetFcpPersistentBinding\_IN**](https://msdn.microsoft.com/library/windows/hardware/ff554933)

[**GetFcpPersistentBinding\_OUT**](https://msdn.microsoft.com/library/windows/hardware/ff554936)

[**HBAFCPBindingEntry**](https://msdn.microsoft.com/library/windows/hardware/ff556034)

 

 






