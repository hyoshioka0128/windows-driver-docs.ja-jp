---
title: GetFC4Statistics 関数
description: Nx の種類のポートでトラフィックの統計情報を報告 GetFC4Statistics WMI\_示された FC 4 プロトコルのポート。
ms.assetid: f57f11bf-57b8-4ae9-96b3-4191f412c80c
keywords:
- 記憶装置の GetFC4Statistics 関数
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
ms.openlocfilehash: b98234d86b502aeda0f5958c623a7f6aaf61e0c8
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67378546"
---
# <a name="getfc4statistics-function"></a>GetFC4Statistics 関数


**GetFC4Statistics** WMI メソッドは、Nx の種類のポートでトラフィックの統計情報を報告\_示された FC 4 プロトコルのポート。

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

*HBAStatus*   
に返された場合、操作の状態を示す WMI 修飾子の値を格納します。 使用できる値とその説明の一覧は、次を参照してください。 [HBA\_状態](hba-status.md)します。 ミニポート ドライバーには、この情報が返されます、 **HBAStatus**のメンバー、 [ **GetFC4Statistics\_アウト**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/hbapiwmi/ns-hbapiwmi-_getfc4statistics_out)構造体。

*PortWWN*   
Nx 型のローカル ポートの世界中の名前\_がトラフィックの統計情報が報告されることをポート。 この情報は、ミニポート ドライバーに配信される、 **PortWWN**のメンバー、 [ **GetFC4Statistics\_IN** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/hbapiwmi/ns-hbapiwmi-_getfc4statistics_in)構造体。

*FC4Type*   
FC 4 プロトコルの種類を示す値。 FC4 型の詳細については、T11 委員会を参照してください。*ファイバー チャネル汎用サービス - 4*仕様。 この情報は、ミニポート ドライバーに配信される、 **FC4Type**のメンバー、 [ **GetFC4Statistics\_IN** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/hbapiwmi/ns-hbapiwmi-_getfc4statistics_in)構造体。

*FC4Statistics*   
返された場合は、型の構造体が含まれています。 [ **MSFC\_FC4STATISTICS** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/hbapiwmi/ns-hbapiwmi-_msfc_fc4statistics)指定 FC 4 プロトコルの統計情報を保持しています。 ミニポート ドライバーには、この情報が返されます、 **FC4Statistics**のメンバー、 [ **GetFC4Statistics\_アウト**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/hbapiwmi/ns-hbapiwmi-_getfc4statistics_out)構造体。

<a name="return-value"></a>戻り値
------------

WMI メソッドには適用されません。

<a name="remarks"></a>注釈
-------

この WMI メソッドが属する、 [MSFC\_HBAAdapterMethods WMI クラス](msfc-hbaadaptermethods-wmi-class.md)します。

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
<td align="left">Hbapiwmi.h (Hbapiwmi.h、Hbaapi.h、Hbaapi.h など)</td>
</tr>
<tr class="odd">
<td align="left"><p>Library</p></td>
<td align="left">Hbaapi.lib</td>
</tr>
</tbody>
</table>

## <a name="span-idseealsospansee-also"></a><span id="see_also"></span>参照してください。


[**GetFC4Statistics\_IN**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/hbapiwmi/ns-hbapiwmi-_getfc4statistics_in)

[**GetFC4Statistics\_アウト**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/hbapiwmi/ns-hbapiwmi-_getfc4statistics_out)

[HBA\_状態](hba-status.md)

[**MSFC\_FC4STATISTICS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/hbapiwmi/ns-hbapiwmi-_msfc_fc4statistics)

 

 






