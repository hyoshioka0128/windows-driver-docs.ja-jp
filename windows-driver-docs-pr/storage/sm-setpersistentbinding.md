---
title: SM\_SetPersistentBinding 関数
description: SM\_SetPersistentBinding メソッドは、OS 固有の LUN 情報を論理ユニットのファイバーチャネルプロトコル (FCP) 識別子にマップするために、HBA ミニポートドライバーによって使用されるバインドを設定します。
ms.assetid: 722f7216-9ff4-4f12-a4fe-e1f8f9e594e1
keywords:
- SM_SetPersistentBinding 関数記憶装置
topic_type:
- apiref
api_name:
- SM_SetPersistentBinding
api_location:
- Hbapiwmi.h
api_type:
- HeaderDef
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: f56405988affefbc05a1bee820130cd67414fca7
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72845447"
---
# <a name="sm_setpersistentbinding-function"></a>SM\_SetPersistentBinding 関数


SM\_SetPersistentBinding メソッドは、OS 固有の LUN 情報を論理ユニットのファイバーチャネルプロトコル (FCP) 識別子にマップするために、HBA ミニポートドライバーによって使用されるバインドを設定します。

<a name="syntax"></a>構文
------

```ManagedCPlusPlus
void SM_SetPersistentBinding(
   [in, HBAType("HBA_WWN")] uint8                        HbaPortWWN[8],
   [in, HBAType("HBA_WWN")] uint8                        DomainPortWWN[8],
   [in] uint32                                           InEntryCount,
   [in, WmiSizeIs("InEntryCount")] MS_SMHBA_BINDINGENTRY Entry[],
   [out, HBA_STATUS_QUALIFIERS] HBA_STATUS               HBAStatus,
   [out] uint32                                          OutStatusCount,
   [out, HBA_STATUS_QUALIFIERS] HBA_STATUS               EntryStatus
);
```

<a name="parameters"></a>パラメーター
----------

*HbaPortWWN*   
永続的なバインドが設定されるポートのワールド名 (WWN)。

*DomainPortWWN*   
コールバックのワールド名 (WWN)。 これは、物理ファイバーチャネルポートを使用して検出された SMP ポートの任意のポート\_識別子の最小値を持つポート\_識別子です。 物理ファイバーチャネルポートを使用して SMP ポートが検出されていない場合、この値は0になります。

*Inentrycount*   
エントリパラメーターで WMI プロバイダーが報告できるバインドエントリの数。

*エントリ*   
オペレーティングシステムと SAS 識別子の間の HBA のバインドを記述する SMHBA\_SCSIENTRY 型の構造体の配列。

*Hbastatus*   
操作の状態。 許可される値とその説明の一覧については、「 [HBA\_STATUS](hba-status.md)」を参照してください。 ミニポートドライバーは、GetPersistentBinding\_OUT 構造体の HBAStatus メンバーにこの情報を返します。

*Outstatuscount*   
SM\_GetPersistentBinding メソッドによって取得される永続的なバインディングの合計数。 この値は TotalEntryCount 以下です。

*Entrystatus*   
操作の状態。 許可される値とその説明の一覧については、「 [HBA\_STATUS](hba-status.md)」を参照してください。 ミニポートドライバーは、GetPersistentBinding\_OUT 構造体の HBAStatus メンバーにこの情報を返します。

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

[**SM\_SetPersistentBinding\_** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/hbapiwmi/ns-hbapiwmi-_sm_setpersistentbinding_in)

[**SM\_SetPersistentBinding\_OUT**](https://docs.microsoft.com/windows-hardware/drivers/ddi/hbapiwmi/ns-hbapiwmi-_sm_setpersistentbinding_out)

 

 






