---
title: GetPersistentBinding2 関数
description: GetPersistentBinding2 メソッドは、HBA ミニポートドライバーが論理ユニットを識別するために使用する情報を論理ユニットのファイバーチャネルプロトコル (FCP) 識別子にマップするために使用するバインドを取得します。
ms.assetid: 17734973-fa82-4f54-b882-d9a2f5ce2066
keywords:
- GetPersistentBinding2 function Storage デバイス
topic_type:
- apiref
api_name:
- GetPersistentBinding2
api_location:
- Hbapiwmi.h
api_type:
- HeaderDef
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 42113e99635b85e419f902cac0cb8b44f1b255be
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72844689"
---
# <a name="getpersistentbinding2-function"></a>GetPersistentBinding2 関数


**GetPersistentBinding2**メソッドは、HBA ミニポートドライバーが論理ユニットを識別するために使用する情報を論理ユニットのファイバーチャネルプロトコル (FCP) 識別子にマップするために使用するバインドを取得します。

<a name="syntax"></a>構文
------

```ManagedCPlusPlus
void GetPersistentBinding2(
   [in, HBAType("HBA_WWN")] uint8                        PortWWN[8],
   [in] uint32                                           InEntryCount,
   [out, HBA_STATUS_QUALIFIERS] HBA_STATUS               HBAStatus,
   [out] uint32                                          TotalEntryCount,
   [out] uint32                                          OutEntryCount,
   [out, WmiSizeIs("OutEntryCount")] HBAFCPBindingEntry2 Bindings[]
);
```

<a name="parameters"></a>パラメーター
----------

*PortWWN\[8\]*    
永続的なバインドを取得するポートを示す、世界規模の名前。

*Inentrycount*   
WMI プロバイダーが*エントリ*パラメーターで報告できるバインドエントリの数を示します。

*Hbastatus*   
戻ると、操作の状態が格納されます。 許可される値とその説明の一覧については、「 [HBA\_STATUS](hba-status.md)」を参照してください。 ミニポートドライバーは、 [**GetFcpPersistentBinding\_OUT**](https://docs.microsoft.com/windows-hardware/drivers/ddi/hbapiwmi/ns-hbapiwmi-_getfcppersistentbinding_out)構造体の**hbastatus**メンバーにこの情報を返します。

*Totalentrycount*   
HBA に関連付けられている永続的なバインドの合計数を示します。

*Outentrycount*   
**GetPersistentBinding2**メソッドによって取得された永続的なバインディングの合計数を示します。 この値は*Totalentrycount*以下です。

*バインド\[\]*    
[**HBAFCPBindingEntry2**](https://docs.microsoft.com/windows-hardware/drivers/ddi/hbapiwmi/ns-hbapiwmi-_hbafcpbindingentry2)型の構造体の配列。これは、オペレーティングシステムとファイバーチャネルプロトコル (FCP) の識別子の間の HBA のバインドを記述します。

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
</tbody>
</table>

## <a name="span-idsee_alsospansee-also"></a><span id="see_also"></span>関連項目


[**GetFcpPersistentBinding\_** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/hbapiwmi/ns-hbapiwmi-_getfcppersistentbinding_in)

[**GetFcpPersistentBinding\_** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/hbapiwmi/ns-hbapiwmi-_getfcppersistentbinding_out)

[**HBAFCPBindingEntry2**](https://docs.microsoft.com/windows-hardware/drivers/ddi/hbapiwmi/ns-hbapiwmi-_hbafcpbindingentry2)

 

 






