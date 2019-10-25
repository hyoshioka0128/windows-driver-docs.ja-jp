---
title: ScsiReportLuns 関数
description: ScsiReportLuns WMI メソッドは、指定されたデバイスに SCSI レポート Lun コマンドを送信します。
ms.assetid: 12c9138d-41b7-404f-8431-08d7cf9cc330
keywords:
- ScsiReportLuns function Storage デバイス
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
ms.openlocfilehash: d4a9454d7c0257649a2c1289bd904901f6119587
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72844316"
---
# <a name="scsireportluns-function"></a>ScsiReportLuns 関数


**ScsiReportLuns** WMI メソッドは、指定されたデバイスに SCSI レポート lun コマンドを送信します。

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

*Hbastatus*   
戻ると、操作の状態が格納されます。 許可される値とその説明の一覧については、「 [HBA\_STATUS](hba-status.md)」を参照してください。 ミニポートドライバーは、 [**ScsiReportLuns\_OUT**](https://docs.microsoft.com/windows-hardware/drivers/ddi/hbapiwmi/ns-hbapiwmi-_scsireportluns_out)構造体の**hbastatus**メンバーにこの情報を返します。

*Cdb*   
ターゲットデバイスに送信される SCSI レポート Lun コマンドを保持するコマンド記述子ブロック。 この情報は、構造[**内の ScsiReportLuns\_** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/hbapiwmi/ns-hbapiwmi-_scsireportluns_in)の**Cdb**メンバーのミニポートドライバーに配信されます。

*HbaPortWWN*   
ターゲットへのアクセスに使用される HBA のワールド名。 この情報は、構造体の[**ScsiReportLuns\_** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/hbapiwmi/ns-hbapiwmi-_scsireportluns_in)の**HbaPortWWN**メンバーのミニポートドライバーに配信されます。

*DiscoveredPortWWN*   
ターゲットデバイスへのアクセスに使用するポートの世界規模の名前。 この情報は、構造体の[**ScsiReportLuns\_** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/hbapiwmi/ns-hbapiwmi-_scsireportluns_in)の**DiscoveredPortWWN**メンバーのミニポートドライバーに配信されます。

*Responsebuffersize*   
SCSI レポート Lun コマンドの結果を保持するバッファーのサイズ (バイト単位)。 ミニポートドライバーは、 [**ScsiReportLuns\_OUT**](https://docs.microsoft.com/windows-hardware/drivers/ddi/hbapiwmi/ns-hbapiwmi-_scsireportluns_out)構造体の**responsebuffersize**メンバーにこの情報を返します。

*Sensebuffersize*   
SCSI レポート Lun コマンドの結果として生成される SCSI センスデータを保持するバッファーのサイズ (バイト単位)。 ミニポートドライバーは、 [**ScsiReportLuns\_OUT**](https://docs.microsoft.com/windows-hardware/drivers/ddi/hbapiwmi/ns-hbapiwmi-_scsireportluns_out)構造体の**sensebuffersize**メンバーでこの情報を返します。

*ScsiStatus*   
SCSI レポート Lun コマンドの状態。 ミニポートドライバーは、 [**ScsiReportLuns\_OUT**](https://docs.microsoft.com/windows-hardware/drivers/ddi/hbapiwmi/ns-hbapiwmi-_scsireportluns_out)構造体の**ScsiStatus**メンバーにこの情報を返します。

*Responsebuffer*   
SCSI レポート Lun コマンドの結果。 ミニポートドライバーは、 [**ScsiReportLuns\_OUT**](https://docs.microsoft.com/windows-hardware/drivers/ddi/hbapiwmi/ns-hbapiwmi-_scsireportluns_out)構造体の**responsebuffer**メンバーでこの情報を返します。

*Sensebuffer*   
SCSI レポート Lun コマンドの結果として生成される SCSI sense データ。 ミニポートドライバーは、 [**ScsiReportLuns\_OUT**](https://docs.microsoft.com/windows-hardware/drivers/ddi/hbapiwmi/ns-hbapiwmi-_scsireportluns_out)構造体の**sensebuffer**メンバーでこの情報を返します。

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


[HBA\_の状態](hba-status.md)

[**ScsiReportLuns\_** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/hbapiwmi/ns-hbapiwmi-_scsireportluns_in)

[**ScsiReportLuns\_** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/hbapiwmi/ns-hbapiwmi-_scsireportluns_out)

 

 






