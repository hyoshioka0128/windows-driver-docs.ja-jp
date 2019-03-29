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
ms.openlocfilehash: b420920bf57c4a27de06a54abe86adc2410ddad3
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56571048"
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
に返された場合、操作の状態を示す WMI 修飾子の値を格納します。 使用できる値とその説明の一覧は、次を参照してください。 [HBA\_状態](hba-status.md)します。 ミニポート ドライバーには、この情報が返されます、 **HBAStatus**のメンバー、 [ **GetFC4Statistics\_アウト**](https://msdn.microsoft.com/library/windows/hardware/ff553960)構造体。

*PortWWN*   
Nx 型のローカル ポートの世界中の名前\_がトラフィックの統計情報が報告されることをポート。 この情報は、ミニポート ドライバーに配信される、 **PortWWN**のメンバー、 [ **GetFC4Statistics\_IN** ](https://msdn.microsoft.com/library/windows/hardware/ff553958)構造体。

*FC4Type*   
FC 4 プロトコルの種類を示す値。 FC4 型の詳細については、T11 委員会を参照してください。*ファイバー チャネル汎用サービス - 4*仕様。 この情報は、ミニポート ドライバーに配信される、 **FC4Type**のメンバー、 [ **GetFC4Statistics\_IN** ](https://msdn.microsoft.com/library/windows/hardware/ff553958)構造体。

*FC4Statistics*   
返された場合は、型の構造体が含まれています。 [ **MSFC\_FC4STATISTICS** ](https://msdn.microsoft.com/library/windows/hardware/ff562492)指定 FC 4 プロトコルの統計情報を保持しています。 ミニポート ドライバーには、この情報が返されます、 **FC4Statistics**のメンバー、 [ **GetFC4Statistics\_アウト**](https://msdn.microsoft.com/library/windows/hardware/ff553960)構造体。

<a name="return-value"></a>戻り値
------------

WMI メソッドには適用されません。

<a name="remarks"></a>コメント
-------

この WMI メソッドが属する、 [MSFC\_HBAAdapterMethods WMI クラス](msfc-hbaadaptermethods-wmi-class.md)します。

<a name="requirements"></a>必要条件
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


[**GetFC4Statistics\_IN**](https://msdn.microsoft.com/library/windows/hardware/ff553958)

[**GetFC4Statistics\_アウト**](https://msdn.microsoft.com/library/windows/hardware/ff553960)

[HBA\_状態](hba-status.md)

[**MSFC\_FC4STATISTICS**](https://msdn.microsoft.com/library/windows/hardware/ff562492)

 

 






