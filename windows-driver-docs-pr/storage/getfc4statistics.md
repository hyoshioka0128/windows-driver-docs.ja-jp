---
title: GetFC4Statistics 関数
description: GetFC4Statistics WMI メソッドは、指定された FC-4 プロトコルについて、種類が Nx\_ポートのトラフィック統計を報告します。
ms.assetid: f57f11bf-57b8-4ae9-96b3-4191f412c80c
keywords:
- GetFC4Statistics function Storage デバイス
topic_type:
- apiref
api_name:
- GetFC4Statistics
api_location:
- Hbaapi.lib
- Hbaapi.dll
api_type:
- LibDef
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 18f8af9884f1d3735d3638647d69da594220105e
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72837965"
---
# <a name="getfc4statistics-function"></a>GetFC4Statistics 関数


**GetFC4Statistics** WMI メソッドは、指定された FC-4 プロトコルについて、種類が Nx\_ポートのトラフィック統計を報告します。

<a name="syntax"></a>構文
------

```ManagedCPlusPlus
void GetFC4Statistics(
   [out, HBA_STATUS_QUALIFIERS] HBA_STATUS HBAStatus,
   [in, HBAType("HBA_WWN")] uint8          PortWWN,
   [in] uint8                              FC4Type,
   [out] MSFC_FC4STATISTICS                FC4Statistics
);
```

<a name="parameters"></a>パラメーター
----------

*Hbastatus*   
返されるときに、操作の状態を示す WMI 修飾子値を格納します。 許可される値とその説明の一覧については、「 [HBA\_STATUS](hba-status.md)」を参照してください。 ミニポートドライバーは、 [**GetFC4Statistics\_OUT**](https://docs.microsoft.com/windows-hardware/drivers/ddi/hbapiwmi/ns-hbapiwmi-_getfc4statistics_out)構造体の**hbastatus**メンバーにこの情報を返します。

*PortWWN*   
トラフィックの統計情報が報告されるローカルポートの種類 Nx\_ポートの世界規模の名前。 この情報は、構造体の[**GetFC4Statistics\_** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/hbapiwmi/ns-hbapiwmi-_getfc4statistics_in)の**PortWWN**メンバーのミニポートドライバーに配信されます。

*FC4Type*   
FC-4 プロトコルの種類を示す値。 FC4 の種類の詳細については、「T11 委員会の*ファイバーチャネル汎用サービス-4*の仕様」を参照してください。 この情報は、構造体の[**GetFC4Statistics\_** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/hbapiwmi/ns-hbapiwmi-_getfc4statistics_in)の**FC4Type**メンバーのミニポートドライバーに配信されます。

*FC4Statistics*   
返されると、指定した FC-4 プロトコルの統計を保持する[**Msfc\_FC4STATISTICS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/hbapiwmi/ns-hbapiwmi-_msfc_fc4statistics)型の構造体が含まれます。 ミニポートドライバーは、 [**GetFC4Statistics\_OUT**](https://docs.microsoft.com/windows-hardware/drivers/ddi/hbapiwmi/ns-hbapiwmi-_getfc4statistics_out)構造体の**FC4Statistics**メンバーにこの情報を返します。

<a name="return-value"></a>戻り値
------------

WMI メソッドには適用されません。

<a name="remarks"></a>注釈
-------

この WMI メソッドは、 [Msfc\_HBAAdapterMethods WMI クラス](msfc-hbaadaptermethods-wmi-class.md)に属しています。

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


[**GetFC4Statistics\_** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/hbapiwmi/ns-hbapiwmi-_getfc4statistics_in)

[**GetFC4Statistics\_** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/hbapiwmi/ns-hbapiwmi-_getfc4statistics_out)

[HBA\_の状態](hba-status.md)

[**MSFC\_FC4STATISTICS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/hbapiwmi/ns-hbapiwmi-_msfc_fc4statistics)

 

 






