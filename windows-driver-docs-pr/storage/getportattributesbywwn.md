---
title: Getport属性 Bywwn 関数
description: Getportattributes Bywwn メソッドは、ポート名によって指定されたポートの属性を取得します。
ms.assetid: 24b62b1c-9f47-40f1-aa72-849fabcbfbae
keywords:
- Getport属性 Bywwn 関数のストレージデバイス
topic_type:
- apiref
api_name:
- GetPortAttributesByWWN
api_location:
- Hbaapi.lib
- Hbaapi.dll
api_type:
- LibDef
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 7cc93093dc035af8611b0224d3c0b8197a3721cd
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72837565"
---
# <a name="getportattributesbywwn-function"></a>Getport属性 Bywwn 関数


**Getportattributes bywwn**メソッドは、ポート名によって指定されたポートの属性を取得します。

<a name="syntax"></a>構文
------

```ManagedCPlusPlus
void GetPortAttributesByWWN(
   [in, HBAType("HBA_WWN")] uint8                                     wwn[8],
   [out, HBA_STATUS_QUALIFIERS] HBA_STATUS                            HBAStatus,
   [out, HBAType("HBA_PORTATTRIBUTES")] MSFC_HBAPortAttributesResults PortAttributes
);
```

<a name="parameters"></a>パラメーター
----------

*wwn\[8\]*    
属性を照会するポートの名前。 この情報は、構造[**内の Getport属性 Bywwn\_** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/hbapiwmi/ns-hbapiwmi-_getportattributesbywwn_in)の**wwn**メンバーのミニポートドライバーに配信されます。

*Hbastatus*   
戻ると、操作の状態が格納されます。 許可される値とその説明の一覧については、「 [HBA\_STATUS](hba-status.md)」を参照してください。 ミニポートドライバーは、 [**Getport属性 Bywwn\_OUT**](https://docs.microsoft.com/windows-hardware/drivers/ddi/hbapiwmi/ns-hbapiwmi-_getportattributesbywwn_out)構造の**hbastatus**メンバーにこの情報を返します。

*Portattributes*   
検出された FC\_ポートの属性を返すことができる[**Msfc\_HBAPortAttributesResults**](https://docs.microsoft.com/windows-hardware/drivers/ddi/hbapiwmi/ns-hbapiwmi-_msfc_hbaportattributesresults)型の構造体。 ミニポートドライバーは、 [**GetDiscoveredPortAttributes\_OUT**](https://docs.microsoft.com/windows-hardware/drivers/ddi/hbapiwmi/ns-hbapiwmi-_getdiscoveredportattributes_out)構造体の**portattributes**メンバーにこの情報を返します。

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


[**の Getport属性 Bywwn\_** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/hbapiwmi/ns-hbapiwmi-_getportattributesbywwn_in)

[**Getport属性 Bywwn\_OUT**](https://docs.microsoft.com/windows-hardware/drivers/ddi/hbapiwmi/ns-hbapiwmi-_getportattributesbywwn_out)

[**MSFC\_HBAPortAttributesResults**](https://docs.microsoft.com/windows-hardware/drivers/ddi/hbapiwmi/ns-hbapiwmi-_msfc_hbaportattributesresults)

 

 






