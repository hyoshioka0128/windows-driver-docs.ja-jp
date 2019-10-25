---
title: AddPort 関数
description: AddPort WMI メソッドは、指定されたポートに関連付けられているイベントを WMI クライアントに通知するように WMI プロバイダーを構成します。
ms.assetid: d20021c8-2326-4fd8-b098-70ab8bf53ed3
keywords:
- AddPort 関数のストレージデバイス
topic_type:
- apiref
api_name:
- AddPort
api_location:
- Hbapiwmi.h
api_type:
- HeaderDef
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: e378cbe309642583e4895dd32c45f3bde19c7b72
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72845113"
---
# <a name="addport-function"></a>AddPort 関数


**Addport** wmi メソッドは、指定されたポートに関連付けられているイベントを wmi クライアントに通知するように wmi プロバイダーを構成します。

<a name="syntax"></a>構文
------

```ManagedCPlusPlus
void AddPort(
   [in, HBAType("HBA_WWN")] uint8          PortWWN[8],
   [out, HBA_STATUS_QUALIFIERS] HBA_STATUS HBAStatus
);
```

<a name="parameters"></a>パラメーター
----------

*PortWWN\[8\]*    
イベントが報告されるポートを示す世界的な名前。

*Hbastatus*   
戻ると、操作の状態が格納されます。 許可される値とその説明の一覧については、「 [HBA\_STATUS](hba-status.md)」を参照してください。 ミニポートドライバーは、 [**Addport\_OUT**](https://docs.microsoft.com/windows-hardware/drivers/ddi/hbapiwmi/ns-hbapiwmi-_addport_out)構造体の**hbastatus**メンバーにこの情報を返します。

<a name="return-value"></a>戻り値
------------

WMI メソッドには適用されません。

<a name="remarks"></a>注釈
-------

この WMI メソッドは、 [Msfc\_EventControl WMI クラス](msfc-eventcontrol-wmi-class.md)に属しています。

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


[**AddPort\_** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/hbapiwmi/ns-hbapiwmi-_addport_in)

[**AddPort\_OUT**](https://docs.microsoft.com/windows-hardware/drivers/ddi/hbapiwmi/ns-hbapiwmi-_addport_out)

 

 






