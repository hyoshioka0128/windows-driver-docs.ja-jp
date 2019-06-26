---
title: ScsiReadCapacity 関数
description: ScsiReadCapacity WMI メソッドでは、SCSI の読み取りに指定されたデバイスの容量コマンドを送信します。
ms.assetid: 2e865ed8-a835-40e7-8ba3-babb9d18eb23
keywords:
- 記憶装置の ScsiReadCapacity 関数
topic_type:
- apiref
api_name:
- ScsiReadCapacity
api_location:
- Hbaapi.lib
- Hbaapi.dll
api_type:
- LibDef
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 1c137a8d629f4a3d8a7528bbb77be2e0d075d031
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67363352"
---
# <a name="scsireadcapacity-function"></a>ScsiReadCapacity 関数


**ScsiReadCapacity** WMI メソッドは、SCSI 読み取り容量コマンドは、指定されたデバイスを送信します。

<a name="syntax"></a>構文
------

```ManagedCPlusPlus
void ScsiReadCapacity(
   [out, HBA_STATUS_QUALIFIERS] HBA_STATUS      HBAStatus,
   [in] uint8                                   Cdb[10],
   [in, HBAType("HBA_WWN")] uint8               HbaPortWWN[10],
   [in, HBAType("HBA_WWN")] uint8               DiscoveredPortWWN[10],
   [in] uint64                                  FcLun,
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
に返された場合、操作の状態を格納します。 使用できる値とその説明の一覧は、次を参照してください。 [HBA\_状態](hba-status.md)します。 ミニポート ドライバーには、この情報が返されます、 **HBAStatus**のメンバー、 [ **ScsiReadCapacity\_アウト**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/hbapiwmi/ns-hbapiwmi-_scsireadcapacity_out)構造体。

*Cdb*   
SCSI を保持するコマンド記述子ブロックの読み取り、ターゲット デバイスに送信される容量コマンド。 この情報は、ミニポート ドライバーに配信される、 **Cdb**のメンバー、 [ **ScsiReadCapacity\_IN** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/hbapiwmi/ns-hbapiwmi-_scsireadcapacity_in)構造体。

*HbaPortWWN*   
ターゲットにアクセスする HBA の世界中の名前。 この情報は、ミニポート ドライバーに配信される、 **HbaPortWWN**のメンバー、 [ **ScsiReadCapacity\_IN** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/hbapiwmi/ns-hbapiwmi-_scsireadcapacity_in)構造体。

*DiscoveredPortWWN*   
ターゲット デバイスにアクセスするポートの世界中の名前。 この情報は、ミニポート ドライバーに配信される、 **DiscoveredPortWWN**のメンバー、 [ **ScsiReadCapacity\_IN** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/hbapiwmi/ns-hbapiwmi-_scsireadcapacity_in)構造体。

*FcLun*   
論理ユニットの数、SCSI を受信する論理ユニットの読み取り容量コマンド。 この情報は、ミニポート ドライバーに配信される、 **FcLun**のメンバー、 [ **ScsiReadCapacity\_IN** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/hbapiwmi/ns-hbapiwmi-_scsireadcapacity_in)構造体。

*ResponseBufferSize*   
読み取り能力のコマンドの結果を保持するバッファーのバイト サイズ。 ミニポート ドライバーには、この情報が返されます、 **ResponseBufferSize**のメンバー、 [ **ScsiReadCapacity\_アウト**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/hbapiwmi/ns-hbapiwmi-_scsireadcapacity_out)構造体。

*SenseBufferSize*   
SCSI のセンス データが格納されるバッファーのバイト単位のサイズは、SCSI 問い合わせコマンドの結果です。 ミニポート ドライバーには、この情報が返されます、 **SenseBufferSize**のメンバー、 [ **ScsiReadCapacity\_アウト**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/hbapiwmi/ns-hbapiwmi-_scsireadcapacity_out)構造体。

*ScsiStatus*   
SCSI の状態は読み取り容量コマンドです。 ミニポート ドライバーには、この情報が返されます、 **ScsiStatus**のメンバー、 [ **ScsiReadCapacity\_アウト**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/hbapiwmi/ns-hbapiwmi-_scsireadcapacity_out)構造体。

*ResponseBuffer*   
SCSI の結果は読み取り容量コマンドです。 ミニポート ドライバーには、この情報が返されます、 **ResponseBuffer**のメンバー、 [ **ScsiReadCapacity\_アウト**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/hbapiwmi/ns-hbapiwmi-_scsireadcapacity_out)構造体。

*SenseBuffer*   
SCSI に起因する SCSI センス データは読み取り容量コマンドです。 ミニポート ドライバーには、この情報が返されます、 **SenseBuffer**のメンバー、 [ **ScsiReadCapacity\_アウト**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/hbapiwmi/ns-hbapiwmi-_scsireadcapacity_out)構造体。

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

[**ScsiReadCapacity\_IN**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/hbapiwmi/ns-hbapiwmi-_scsireadcapacity_in)

[**ScsiReadCapacity\_OUT**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/hbapiwmi/ns-hbapiwmi-_scsireadcapacity_out)

 

 






