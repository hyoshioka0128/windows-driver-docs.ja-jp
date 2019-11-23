---
title: SM\_GetTargetMapping 関数
description: SM\_GetTargetMapping WMI メソッドは、オペレーティングシステムの一連の論理ユニットとこれらの論理ユニットのファイバーチャネルプロトコル (FCP) 識別子を一意に識別する情報間のマッピングを取得します。
ms.assetid: db18920c-327d-4349-8821-6d7fb68eccbd
keywords:
- SM_GetTargetMapping 関数記憶装置
topic_type:
- apiref
api_name:
- SM_GetTargetMapping
api_location:
- Hbapiwmi.h
api_type:
- HeaderDef
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 1460e2c75d8327b635eefee2b9035720bfef31ad
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72845479"
---
# <a name="sm_gettargetmapping-function"></a>SM\_GetTargetMapping 関数


SM\_GetTargetMapping WMI メソッドは、オペレーティングシステムの一連の論理ユニットとこれらの論理ユニットのファイバーチャネルプロトコル (FCP) 識別子を一意に識別する情報間のマッピングを取得します。

<a name="syntax"></a>構文
------

```ManagedCPlusPlus
void SM_GetTargetMapping(
   [in, HBAType("HBA_WWN")] uint8                       HbaPortWWN[8],
   [in, HBAType("HBA_WWN")] uint8                       DomainPortWWN[8],
   [in] uint32                                          InEntryCount,
   [out, HBA_STATUS_QUALIFIERS] HBA_STATUS              HBAStatus,
   [out] uint32                                         TotalEntryCount,
   [out] uint32                                         OutEntryCount,
   [out, WmiSizeIs("OutEntryCount")] MS_SMHBA_SCSIENTRY Entry[]
);
```

<a name="parameters"></a>パラメーター
----------

*HbaPortWWN*   
マッピングのテーブルを取得するポートのワールド名 (WWN)。 この情報は、構造内の GetTargetMapping\_の HbaPortWWN メンバーのミニポートドライバーに配信されます。

*DomainPortWWN*   
コールバックのワールド名 (WWN)。 これは、物理ファイバーチャネルポートを使用して検出された SMP ポートの\_識別子の最小値を持つポート\_識別子です。 物理ファイバーチャネルポートを使用して SMP ポートが検出されていない場合、この値は0になります。

*Inentrycount*   
エントリパラメーターで WMI プロバイダーが報告できるバインドエントリの数。

*Hbastatus*   
操作の状態。 許可される値とその説明の一覧については、「 [HBA\_状態](hba-status.md)の構造」を参照してください。 ミニポートドライバーは、GetFcpTargetMapping\_OUT 構造体の HBAStatus メンバーにこの情報を返します。

*Totalentrycount*   
HBA に関連付けられている永続的なバインドの合計数。

*Outentrycount*   
SM\_GetTargetMapping メソッドによって取得されるマッピングの合計数。 この値は TotalEntryCount 以下です。

*エントリ*   
オペレーティングシステムとファイバーチャネルプロトコル (FCP) 識別子の間の HBA のバインドを記述する、MS\_SMHBA\_SCSIENTRY 型の構造体の配列。

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

[**SM\_GetTargetMapping\_** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/hbapiwmi/ns-hbapiwmi-_sm_gettargetmapping_in)

[**SM\_GetTargetMapping\_OUT**](https://docs.microsoft.com/windows-hardware/drivers/ddi/hbapiwmi/ns-hbapiwmi-_sm_gettargetmapping_out)

 

 






