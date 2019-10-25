---
title: RemoveLink 関数
description: RemoveLink WMI メソッドは、wmi プロバイダーを構成して、ファブリックリンクイベント情報が WMI クライアントに渡されないようにします。
ms.assetid: 8c9f78ba-fdb8-4d6c-ab99-3492e0887572
keywords:
- RemoveLink 関数のストレージデバイス
topic_type:
- apiref
api_name:
- RemoveLink
api_location:
- Hbapiwmi.h
api_type:
- HeaderDef
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: e9eaf74cbb13368bd7935cefaa4fc705b1b44532
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72842711"
---
# <a name="removelink-function"></a>RemoveLink 関数


**Removelink** wmi メソッドは、wmi プロバイダーを構成して、ファブリックリンクイベント情報が wmi クライアントに渡されないようにします。

<a name="syntax"></a>構文
------

```ManagedCPlusPlus
void RemoveLink(
   [out, HBA_STATUS_QUALIFIERS] HBA_STATUS HBAStatus
);
```

<a name="parameters"></a>パラメーター
----------

*Hbastatus*   
戻ると、操作の状態が格納されます。 許可される値とその説明の一覧については、「 [HBA\_STATUS](hba-status.md)」を参照してください。 ミニポートドライバーは、 [**Removelink\_OUT**](https://docs.microsoft.com/windows-hardware/drivers/ddi/hbapiwmi/ns-hbapiwmi-_removelink_out)構造体の**hbastatus**メンバーでこの情報を返します。

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


[**RemoveLink\_OUT**](https://docs.microsoft.com/windows-hardware/drivers/ddi/hbapiwmi/ns-hbapiwmi-_removelink_out)

 

 






