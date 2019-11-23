---
title: GetFcpPersistentBinding 関数
description: GetFcpPersistentBinding メソッドは、HBA ミニポートドライバーが論理ユニットを識別するために使用する情報を論理ユニットのファイバーチャネルプロトコル (FCP) 識別子にマップするために使用するバインドを取得します。
ms.assetid: ee675022-51f7-4b81-863c-ee608b0284b0
keywords:
- GetFcpPersistentBinding function Storage デバイス
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
ms.openlocfilehash: 36cf385cd3c462837cb6f6c4327a3494e2505446
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72837963"
---
# <a name="getfcppersistentbinding-function"></a>GetFcpPersistentBinding 関数


**GetFcpPersistentBinding**メソッドは、HBA ミニポートドライバーが論理ユニットを識別するために使用する情報を論理ユニットのファイバーチャネルプロトコル (FCP) 識別子にマップするために使用するバインドを取得します。

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

*Inentrycount*   
WMI プロバイダーが*エントリ*パラメーターで報告できるバインドエントリの数を示します。

*Hbastatus*   
戻ると、操作の状態が格納されます。 許可される値とその説明の一覧については、「 [HBA\_STATUS](hba-status.md)」を参照してください。 ミニポートドライバーは、 [**GetFcpPersistentBinding\_OUT**](https://docs.microsoft.com/windows-hardware/drivers/ddi/hbapiwmi/ns-hbapiwmi-_getfcppersistentbinding_out)構造体の**hbastatus**メンバーにこの情報を返します。

*Totalentrycount*   
HBA に関連付けられている永続的なバインドの合計数を示します。

*Outentrycount*   
**GetFcpPersistentBinding**メソッドによって取得された永続的なバインディングの合計数を示します。 この値は*Totalentrycount*以下です。

*エントリ\[\]*    
オペレーティングシステムとファイバーチャネルプロトコル (FCP) 識別子の間の HBA のバインドを記述する、 [**Hbafcpbindingentry**](https://docs.microsoft.com/windows-hardware/drivers/ddi/hbapiwmi/ns-hbapiwmi-_hbafcpbindingentry)型の構造体の配列。

<a name="return-value"></a>戻り値
------------

WMI メソッドには適用されません。

<a name="remarks"></a>注釈
-------

この WMI メソッドは、 [Msfc\_HBAFCPInfo WMI クラス](msfc-hbafcpinfo-wmi-class.md)に属しています。

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
<td align="left">Hbapiwmi (Hbapiwmi、Hbaapi. h、または Hbaapi .h を含む)</td>
</tr>
<tr class="odd">
<td align="left"><p>Library</p></td>
<td align="left">Hbaapi .lib</td>
</tr>
</tbody>
</table>

## <a name="span-idsee_alsospansee-also"></a><span id="see_also"></span>関連項目


[**GetFcpPersistentBinding\_** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/hbapiwmi/ns-hbapiwmi-_getfcppersistentbinding_in)

[**GetFcpPersistentBinding\_** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/hbapiwmi/ns-hbapiwmi-_getfcppersistentbinding_out)

[**HBAFCPBindingEntry**](https://docs.microsoft.com/windows-hardware/drivers/ddi/hbapiwmi/ns-hbapiwmi-_hbafcpbindingentry)

 

 






