---
title: GetFCPStatistics 関数
description: GetFCPStatistics WMI メソッドは、指定されたローカル hba に指定された SCSI 論理ユニットの FCP トラフィック統計情報を返します。
ms.assetid: 566368d7-ee13-449d-97c3-1c214984fee5
keywords:
- 記憶装置の GetFCPStatistics 関数
topic_type:
- apiref
api_name:
- GetFCPStatistics
api_location:
- Hbaapi.lib
- Hbaapi.dll
api_type:
- LibDef
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 86c8b6a03b29267f97728e41e72e25aa54561c91
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56581577"
---
# <a name="getfcpstatistics-function"></a>GetFCPStatistics 関数


**GetFCPStatistics** WMI メソッドは、指定されたローカル HBA の指定された SCSI 論理ユニットの FCP トラフィック統計情報を返します。

<a name="syntax"></a>構文
------

```ManagedCPlusPlus
void GetFCPStatistics(
   [out, HBA_STATUS_QUALIFIERS] HBA_STATUS HBAStatus,
   [in] HBAScsiID                          ScsiId,
   [out] MSFC_FC4STATISTICS                FC4Statistics
);
```

<a name="parameters"></a>パラメーター
----------

*HBAStatus*   
に返された場合、操作の状態を示す WMI 修飾子の値を格納します。 使用できる値とその説明の一覧は、次を参照してください。 [HBA\_状態](hba-status.md)します。 ミニポート ドライバーには、この情報が返されます、 **HBAStatus**のメンバー、 [ **GetFCPStatistics\_アウト**](https://msdn.microsoft.com/library/windows/hardware/ff554944)構造体。

*ScsiId*   
返された場合は、型の構造体が含まれています。 [ **HBAScsiID** ](https://msdn.microsoft.com/library/windows/hardware/ff556042)デバイスを識別する情報を保持します。 この情報は、ミニポート ドライバーに配信される、 **ScsiId**のメンバー、 [ **GetFCPStatistics\_IN** ](https://msdn.microsoft.com/library/windows/hardware/ff554942)構造体。

*FC4Statistics*   
返された場合は、型の構造体が含まれています。 [ **MSFC\_FC4STATISTICS** ](https://msdn.microsoft.com/library/windows/hardware/ff562492)に指定された SCSI 論理ユニットの統計情報を保持しています。 ミニポート ドライバーには、この情報が返されます、 **FC4Statistics**のメンバー、 [ **GetFCPStatistics\_アウト**](https://msdn.microsoft.com/library/windows/hardware/ff554944)構造体。

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


[**GetFCPStatistics\_IN**](https://msdn.microsoft.com/library/windows/hardware/ff554942)

[**GetFCPStatistics\_アウト**](https://msdn.microsoft.com/library/windows/hardware/ff554944)

[**MSFC\_FC4STATISTICS**](https://msdn.microsoft.com/library/windows/hardware/ff562492)

 

 






