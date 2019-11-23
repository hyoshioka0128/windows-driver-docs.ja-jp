---
title: SM\_RemovePersistentBinding 関数
description: SM\_RemovePersistentBinding メソッドは、指定されたアダプターポートについて、指定された SCSI Id に対して1つ以上の永続的なバインドを削除します。
ms.assetid: 475c2f5f-4a1c-48b4-9a43-81d03b1b737d
keywords:
- SM_RemovePersistentBinding 関数記憶装置
topic_type:
- apiref
api_name:
- SM_RemovePersistentBinding
api_location:
- Hbapiwmi.h
api_type:
- HeaderDef
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 0bc577d50fd214358cb10addfb44e799f1de7cdd
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72845475"
---
# <a name="sm_removepersistentbinding-function"></a>SM\_RemovePersistentBinding 関数


SM\_RemovePersistentBinding メソッドは、指定されたアダプターポートについて、指定された SCSI Id に対して1つ以上の永続的なバインドを削除します。

<a name="syntax"></a>構文
------

```ManagedCPlusPlus
void SM_RemovePersistentBinding(
   [in, HBAType("HBA_WWN")] uint8                      HbaPortWWN[8],
   [in, HBAType("HBA_WWN")] uint8                      DomainPortWWN[8],
   [in] uint32                                         EntryCount,
   [in, WmiSizeIs("EntryCount")] MS_SMHBA_BINDINGENTRY Entry[],
   [out, HBA_STATUS_QUALIFIERS] HBA_STATUS             HBAStatus
);
```

<a name="parameters"></a>パラメーター
----------

*HbaPortWWN*   
永続的なバインドが削除されるポートのワールド名 (WWN)。

*DomainPortWWN*   
コールバックのワールド名 (WWN)。 これは、物理ファイバーチャネルポートを使用して検出された SMP ポートの任意のポート\_識別子の最小値を持つポート\_識別子です。 物理ファイバーチャネルポートを使用して SMP ポートが検出されていない場合、この値は0になります。

*Entrycount*   
エントリパラメーターで WMI プロバイダーが報告できるバインドエントリの数。

*エントリ*   
永続的バインドのための MS\_SMHBA\_BINDINGENTRY 型の一覧。

*Hbastatus*   
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

[**SM\_RemovePersistentBinding\_** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/hbapiwmi/ns-hbapiwmi-_sm_removepersistentbinding_in)

[**SM\_RemovePersistentBinding\_OUT**](https://docs.microsoft.com/windows-hardware/drivers/ddi/hbapiwmi/ns-hbapiwmi-_sm_removepersistentbinding_out)

 

 






