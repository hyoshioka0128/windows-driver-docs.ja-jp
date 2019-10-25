---
title: SM\_GetBindingSupport 関数
description: SM\_GetBindingSupport メソッドは、指定されたポートに対して現在有効なバインド機能を取得します。
ms.assetid: 0ca24cdf-b589-4096-a490-2acfdd576a91
keywords:
- SM_GetBindingSupport function Storage デバイス
topic_type:
- apiref
api_name:
- SM_GetBindingSupport
api_location:
- Hbapiwmi.h
api_type:
- HeaderDef
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 300ffaf82b5115177a1feabb6bb13afb6204b5a7
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72842601"
---
# <a name="sm_getbindingsupport-function"></a>SM\_GetBindingSupport 関数


SM\_GetBindingSupport メソッドは、指定されたポートに対して現在有効なバインド機能を取得します。

<a name="syntax"></a>構文
------

```ManagedCPlusPlus
void SM_GetBindingSupport(
   [in, HBAType("HBA_WWN")] uint8                 HbaPortWWN[8],
   [in, HBAType("HBA_WWN")] uint8                 DomainPortWWN[8],
   [out, HBA_STATUS_QUALIFIERS] HBA_STATUS        HBAStatus,
   [out, HBAType("SMHBA_BIND_CAPABILITY")] uint32 Flags
);
```

<a name="parameters"></a>パラメーター
----------

*HbaPortWWN*   
永続的なバインドを取得するポートのワールド名 (WWN)。

*DomainPortWWN*   
コールバックのワールド名 (WWN)。 これは、物理ファイバーチャネルポートを使用して検出された SMP ポートの任意のポート\_識別子の最小値を持つポート\_識別子です。 物理ファイバーチャネルポートを使用して SMP ポートが検出されていない場合、この値は0になります。

*Hbastatus*   
操作の状態。 許可される値とその説明の一覧については、「 [HBA\_状態](hba-status.md)の構造」を参照してください。 ミニポートドライバーは、GetBindingSupport\_OUT 構造体の HBAStatus メンバーでこの情報を返します。

*フラグ*   
永続的なバインディングに関連する特定の機能セットを提供する、HBA とそのミニポートドライバーの機能を示すビットマップ。 このパラメーターに指定できる値の一覧については、「WMI クラス修飾子の\_バインド\_HBA の説明を参照してください。

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

[**SM\_GetBindingSupport\_IN**](https://docs.microsoft.com/windows-hardware/drivers/ddi/hbapiwmi/ns-hbapiwmi-_sm_getbindingsupport_in)

[**SM\_GetBindingSupport\_OUT**](https://docs.microsoft.com/windows-hardware/drivers/ddi/hbapiwmi/ns-hbapiwmi-_sm_getbindingsupport_out)

 

 






