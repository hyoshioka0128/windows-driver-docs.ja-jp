---
title: ScsiReportLuns 関数
description: ScsiReportLuns WMI メソッドは、指定されたデバイスに SCSI レポート Lun のコマンドを送信します。
ms.assetid: 12c9138d-41b7-404f-8431-08d7cf9cc330
keywords:
- 記憶装置の ScsiReportLuns 関数
topic_type:
- apiref
api_name:
- ScsiReportLuns
api_location:
- Hbaapi.lib
- Hbaapi.dll
api_type:
- LibDef
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 5693d52c6646f94267de16d5f5cd5af65657e861
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63356700"
---
# <a name="scsireportluns-function"></a>ScsiReportLuns 関数


**ScsiReportLuns** WMI メソッドでは、SCSI レポート Lun コマンドが、指定されたデバイスを送信します。

<a name="syntax"></a>構文
------

```ManagedCPlusPlus
void ScsiReportLuns(
   [out, HBA_STATUS_QUALIFIERS] HBA_STATUS      HBAStatus,
   [in] uint8                                   Cdb[12],
   [in, HBAType("HBA_WWN")] uint8               HbaPortWWN[8],
   [in, HBAType("HBA_WWN")] uint8               DiscoveredPortWWN[8],
   [out] uint32                                 ResponseBufferSize,
   [out] uint32                                 SenseBufferSize,
   [out] uint8                                  ScsiStatus,
   [out, WmiSizeIs("ResponseBufferSize")] uint8 ResponseBuffer[],
   [out, WmiSizeIs("SenseBufferSize")] uint8    SenseBuffer[]
);
```

<a name="parameters"></a>パラメーター
----------

*HBAStatus*   
に返された場合、操作の状態を格納します。 使用できる値とその説明の一覧は、次を参照してください。 [HBA\_状態](hba-status.md)します。 ミニポート ドライバーには、この情報が返されます、 **HBAStatus**のメンバー、 [ **ScsiReportLuns\_アウト**](https://msdn.microsoft.com/library/windows/hardware/ff564937)構造体。

*Cdb*   
SCSI レポート対象のデバイスに送信される Lun のコマンドを保持するコマンドの記述子ブロックします。 この情報は、ミニポート ドライバーに配信される、 **Cdb**のメンバー、 [ **ScsiReportLuns\_IN** ](https://msdn.microsoft.com/library/windows/hardware/ff564932)構造体。

*HbaPortWWN*   
ターゲットにアクセスする HBA の世界中の名前。 この情報は、ミニポート ドライバーに配信される、 **HbaPortWWN**のメンバー、 [ **ScsiReportLuns\_IN** ](https://msdn.microsoft.com/library/windows/hardware/ff564932)構造体。

*DiscoveredPortWWN*   
ターゲット デバイスにアクセスするポートの世界中の名前。 この情報は、ミニポート ドライバーに配信される、 **DiscoveredPortWWN**のメンバー、 [ **ScsiReportLuns\_IN** ](https://msdn.microsoft.com/library/windows/hardware/ff564932)構造体。

*ResponseBufferSize*   
SCSI レポート Lun コマンドの結果を保持するバッファーのバイト サイズ。 ミニポート ドライバーには、この情報が返されます、 **ResponseBufferSize**のメンバー、 [ **ScsiReportLuns\_アウト**](https://msdn.microsoft.com/library/windows/hardware/ff564937)構造体。

*SenseBufferSize*   
SCSI のセンス データが格納されるバッファーのバイト単位のサイズは、SCSI レポート Lun コマンドの結果です。 ミニポート ドライバーには、この情報が返されます、 **SenseBufferSize**のメンバー、 [ **ScsiReportLuns\_アウト**](https://msdn.microsoft.com/library/windows/hardware/ff564937)構造体。

*ScsiStatus*   
SCSI レポート Lun コマンドの状態です。 ミニポート ドライバーには、この情報が返されます、 **ScsiStatus**のメンバー、 [ **ScsiReportLuns\_アウト**](https://msdn.microsoft.com/library/windows/hardware/ff564937)構造体。

*ResponseBuffer*   
SCSI の結果は、Lun のコマンドを報告します。 ミニポート ドライバーには、この情報が返されます、 **ResponseBuffer**のメンバー、 [ **ScsiReportLuns\_アウト**](https://msdn.microsoft.com/library/windows/hardware/ff564937)構造体。

*SenseBuffer*   
SCSI に起因する SCSI センス データは、Lun のコマンドを報告します。 ミニポート ドライバーには、この情報が返されます、 **SenseBuffer**のメンバー、 [ **ScsiReportLuns\_アウト**](https://msdn.microsoft.com/library/windows/hardware/ff564937)構造体。

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


[HBA\_状態](hba-status.md)

[**ScsiReportLuns\_IN**](https://msdn.microsoft.com/library/windows/hardware/ff564932)

[**ScsiReportLuns\_OUT**](https://msdn.microsoft.com/library/windows/hardware/ff564937)

 

 






