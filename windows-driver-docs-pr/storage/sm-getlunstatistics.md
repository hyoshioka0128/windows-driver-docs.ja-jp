---
title: SM\_GetLUNStatistics 関数
description: SMHBA\_GetLUNStatistics メソッドは、特定のローカル HBA で FCP プロトコルまたは SSP プロトコルを使用して提供されている特定の SCSI 論理ユニットのトラフィック統計を返します。
ms.assetid: c4e85c59-8b8d-4b68-9ab7-adf1e12fc50c
keywords:
- SM_GetLUNStatistics function Storage デバイス
topic_type:
- apiref
api_name:
- SM_GetLUNStatistics
api_location:
- Hbapiwmi.h
api_type:
- HeaderDef
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 040ae128405d41e6f00a769819ec072098afc327
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72845485"
---
# <a name="sm_getlunstatistics-function"></a>SM\_GetLUNStatistics 関数


SMHBA\_GetLUNStatistics メソッドは、特定のローカル HBA で FCP プロトコルまたは SSP プロトコルを使用して提供されている特定の SCSI 論理ユニットのトラフィック統計を返します。

<a name="syntax"></a>構文
------

```ManagedCPlusPlus
void SM_GetLUNStatistics(
   [in, HBAType("HBA_SCSIID")] HBAScsiID                                     Lunit,
   [out, HBA_STATUS_QUALIFIERS] HBA_STATUS                                   HBAStatus,
   [out, HBAType("MS_SMHBA_PROTOCOLSTATISTICS")] MS_SMHBA_PROTOCOLSTATISTICS ProtocolStatistics
);
```

<a name="parameters"></a>パラメーター
----------

*Lunit*   
SCSI 論理ユニットを識別するためにオペレーティングシステムによって使用される情報を含む[**HBA\_ScsiId**](https://msdn.microsoft.com/library/windows/hardware/ff557191)の構造。

*Hbastatus*   
操作の状態。 許可される値とその説明の一覧については、「 [HBA\_STATUS](hba-status.md)」を参照してください。 ミニポートドライバーは、SM の HBAStatus メンバー\_GetLUNStatistics\_OUT 構造体にこの情報を返します。

*Protocolstatistics*   
ポートのプロトコルトラフィックの統計情報をレポートするために使用される、 [**MS\_SMHBA\_protocolstatistics**](https://docs.microsoft.com/windows-hardware/drivers/ddi/hbapiwmi/ns-hbapiwmi-_ms_smhba_protocolstatistics)型の構造。

<a name="return-value"></a>戻り値
------------

WMI メソッドには適用されません。

<a name="remarks"></a>注釈
-------

この WMI メソッドは、MS\_SM\_TargetInformationMethods WMI クラスに属しています。

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
<td align="left">Hbapiwmi</td>
</tr>
</tbody>
</table>

## <a name="span-idsee_alsospansee-also"></a><span id="see_also"></span>関連項目


[HBA\_の状態](hba-status.md)

[**SM\_GetLUNStatistics\_** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/hbapiwmi/ns-hbapiwmi-_sm_getlunstatistics_in)

[**SM\_GetLUNStatistics\_OUT**](https://docs.microsoft.com/windows-hardware/drivers/ddi/hbapiwmi/ns-hbapiwmi-_sm_getlunstatistics_out)

 

 






