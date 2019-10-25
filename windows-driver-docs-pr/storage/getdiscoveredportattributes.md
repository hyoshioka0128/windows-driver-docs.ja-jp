---
title: GetDiscoveredPortAttributes 関数
description: GetDiscoveredPortAttributes WMI メソッドは、指定されたリモートファイバーチャネルポートの属性を取得します。
ms.assetid: f71a02cf-035a-4de2-bb28-e1141a92795c
keywords:
- GetDiscoveredPortAttributes function Storage デバイス
topic_type:
- apiref
api_name:
- GetDiscoveredPortAttributes
api_location:
- Hbaapi.lib
- Hbaapi.dll
api_type:
- LibDef
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 2ae58ad5bd0bbf7649f5d7858ae9f1268eb4a9ce
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72837847"
---
# <a name="getdiscoveredportattributes-function"></a>GetDiscoveredPortAttributes 関数


**GetDiscoveredPortAttributes** WMI メソッドは、指定されたリモートファイバーチャネルポートの属性を取得します。

<a name="syntax"></a>構文
------

```ManagedCPlusPlus
void GetDiscoveredPortAttributes(
   [in] uint32                                                        PortIndex,
   [in] uint32                                                        DiscoveredPortIndex,
   [out, HBA_STATUS_QUALIFIERS] HBA_STATUS                            HBAStatus,
   [out, HBAType("HBA_PORTATTRIBUTES")] MSFC_HBAPortAttributesResults PortAttributes
);
```

<a name="parameters"></a>パラメーター
----------

*Portindex*   
検出されたリモートポートのクエリを実行するために使用される Nx\_ポートの種類のローカルポートのインデックス。 この情報は、構造[**内の GetDiscoveredPortAttributes\_** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/hbapiwmi/ns-hbapiwmi-_getdiscoveredportattributes_in)の**portindex**メンバーのミニポートドライバーに配信されます。

*DiscoveredPortIndex*   
照会するリモートポートのインデックス。 この情報は、構造体の[**GetDiscoveredPortAttributes\_** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/hbapiwmi/ns-hbapiwmi-_getdiscoveredportattributes_in)の**DiscoveredPortIndex**メンバーのミニポートドライバーに配信されます。

*Hbastatus*   
返されるときに、操作の状態を示す WMI 修飾子値を格納します。 許可される値とその説明の一覧については、「 [HBA\_STATUS](hba-status.md)」を参照してください。 ミニポートドライバーは、 [**GetDiscoveredPortAttributes\_OUT**](https://docs.microsoft.com/windows-hardware/drivers/ddi/hbapiwmi/ns-hbapiwmi-_getdiscoveredportattributes_out)構造体の**hbastatus**メンバーにこの情報を返します。

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


[**GetDiscoveredPortAttributes\_** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/hbapiwmi/ns-hbapiwmi-_getdiscoveredportattributes_in)

[**GetDiscoveredPortAttributes\_** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/hbapiwmi/ns-hbapiwmi-_getdiscoveredportattributes_out)

[**MSFC\_HBAPortAttributesResults**](https://docs.microsoft.com/windows-hardware/drivers/ddi/hbapiwmi/ns-hbapiwmi-_msfc_hbaportattributesresults)

 

 






