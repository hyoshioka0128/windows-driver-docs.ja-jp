---
title: SM\_GetPersistentBinding 関数
description: SM\_GetPersistentBinding メソッドは、HBA ミニポートドライバーが使用するバインドを取得します。 これらのバインドは、OS 固有の LUN 情報を論理ユニットのファイバーチャネルプロトコル (FCP) 識別子にマップします。
ms.assetid: 74a67e91-c3b3-462a-8810-a9eae64e02a7
keywords:
- SM_GetPersistentBinding function Storage デバイス
topic_type:
- apiref
api_name:
- SM_GetPersistentBinding
api_location:
- Hbapiwmi.h
api_type:
- HeaderDef
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: d5f3dc03504c1a084644f2e4f3ce46fb2fcfa796
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72845483"
---
# <a name="sm_getpersistentbinding-function"></a>SM\_GetPersistentBinding 関数


SM\_GetPersistentBinding メソッドは、HBA ミニポートドライバーが使用するバインドを取得します。 これらのバインドは、OS 固有の LUN 情報を論理ユニットのファイバーチャネルプロトコル (FCP) 識別子にマップします。

<a name="syntax"></a>構文
------

```ManagedCPlusPlus
void SM_GetPersistentBinding(
   [in, HBAType("HBA_WWN")] uint8                          HbaPortWWN[8],
   [in, HBAType("HBA_WWN")] uint8                          DomainPortWWN[8],
   [in] uint32                                             InEntryCount,
   [out, HBA_STATUS_QUALIFIERS] HBA_STATUS                 HBAStatus,
   [out] uint32                                            TotalEntryCount,
   [out] uint32                                            OutEntryCount,
   [out, WmiSizeIs("OutEntryCount")] MS_SMHBA_BINDINGENTRY Bindings[]
);
```

<a name="parameters"></a>パラメーター
----------

*HbaPortWWN*   
永続的なバインドを取得するポートのワールド名 (WWN)。

*DomainPortWWN*   
コールバックのワールド名 (WWN)。 これは、物理ファイバーチャネルポートを使用して検出された SMP ポートの任意のポート\_識別子の最小値を持つポート\_識別子です。 物理ファイバーチャネルポートを使用して SMP ポートが検出されていない場合、この値は0になります。

*Inentrycount*   
エントリパラメーターで WMI プロバイダーが報告できるバインドエントリの数。

*Hbastatus*   
操作の状態。 許可される値とその説明の一覧については、「 [HBA\_状態](hba-status.md)の構造」を参照してください。 ミニポートドライバーは、GetPersistentBinding\_OUT 構造体の HBAStatus メンバーにこの情報を返します。

*Totalentrycount*   
HBA に関連付けられている永続的なバインドの合計数。

*Outentrycount*   
SM\_GetPersistentBinding メソッドによって取得される永続的なバインディングの合計数。 この値は TotalEntryCount 以下です。

*バインド*   
オペレーティングシステムとファイバーチャネルプロトコル (FCP) 識別子との間の HBA のバインドを記述する、MS\_SMHBA\_BINDINGENTRY 型の構造体の配列。

<a name="return-value"></a>戻り値
------------

WMI メソッドには適用されません。

<a name="remarks"></a>注釈
-------

この WMI メソッドは、MS\_SM\_TargetInformationMethods WMI クラスに属しています。

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
<td align="left">Hbapiwmi</td>
</tr>
</tbody>
</table>

## <a name="span-idsee_alsospansee-also"></a><span id="see_also"></span>関連項目


[HBA\_の状態](hba-status.md)

[**SM\_GetPersistentBinding\_** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/hbapiwmi/ns-hbapiwmi-_sm_getpersistentbinding_in)

[**SM\_GetPersistentBinding\_OUT**](https://docs.microsoft.com/windows-hardware/drivers/ddi/hbapiwmi/ns-hbapiwmi-_sm_getpersistentbinding_out)

 

 






