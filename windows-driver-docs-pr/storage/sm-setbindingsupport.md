---
title: SM\_SetBindingSupport 関数
description: SM\_SetBindingSupport メソッドは、指定されたポートのバインド機能を設定します。
ms.assetid: 31a37fa5-db3c-4944-bf93-e221fb42dc6d
keywords:
- SM_SetBindingSupport 関数記憶装置
topic_type:
- apiref
api_name:
- SM_SetBindingSupport
api_location:
- Hbapiwmi.h
api_type:
- HeaderDef
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 2ed744d8ccee6307cfdb1403f5cb3a0894ea600b
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72845449"
---
# <a name="sm_setbindingsupport-function"></a>SM\_SetBindingSupport 関数


SM\_SetBindingSupport メソッドは、指定されたポートのバインド機能を設定します。

<a name="syntax"></a>構文
------

```ManagedCPlusPlus
void SM_SetBindingSupport(
   [in, HBAType("HBA_WWN")] uint8                HbaPortWWN[8],
   [in, HBAType("HBA_WWN")] uint8                DomainPortWWN[8],
   [in, HBAType("SMHBA_BIND_CAPABILITY")] uint32 Flags,
   [out, HBA_STATUS_QUALIFIERS] HBA_STATUS       HBAStatus
);
```

<a name="parameters"></a>パラメーター
----------

*HbaPortWWN*   
永続的なバインドを取得するポートのワールド名 (WWN)。

*DomainPortWWN*   
コールバックのワールド名 (WWN)。 これは、物理ファイバーチャネルポートを使用して検出された SMP ポートの任意のポート\_識別子の最小値を持つポート\_識別子です。 物理ファイバーチャネルポートを使用して SMP ポートが検出されていない場合、この値は0になります。

*フラグ*   
永続的なバインディングに関連する特定の機能セットを提供する、HBA とそのミニポートドライバーの機能を示すビットマップ。 このパラメーターに指定できる値の一覧については、「WMI クラス修飾子の\_バインド\_HBA の説明を参照してください。

*Hbastatus*   
操作の状態。 許可される値とその説明の一覧については、「 [HBA\_STATUS](hba-status.md)」を参照してください。 ミニポートドライバーは、SetBindingSupport\_OUT 構造体の HBAStatus メンバーにこの情報を返します。

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

[**SM\_SetBindingSupport\_** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/hbapiwmi/ns-hbapiwmi-_sm_setbindingsupport_in)

[**SM\_SetBindingSupport\_OUT**](https://docs.microsoft.com/windows-hardware/drivers/ddi/hbapiwmi/ns-hbapiwmi-_sm_setbindingsupport_out)

 

 






