---
title: SM\_GetLUNStatistics 関数
description: SMHBA\_GetLUNStatistics メソッドは、特定のローカル HBA を FCP プロトコルまたは SSP のプロトコルを使用して提供される特定の SCSI 論理ユニットのトラフィック統計情報を返します。
ms.assetid: c4e85c59-8b8d-4b68-9ab7-adf1e12fc50c
keywords:
- 記憶装置の SM_GetLUNStatistics 関数
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
ms.openlocfilehash: 0f271bee889a5d502c1dfd231848248b8d045dba
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56538231"
---
# <a name="smgetlunstatistics-function"></a>SM\_GetLUNStatistics 関数


SMHBA\_GetLUNStatistics メソッドは、特定のローカル HBA を FCP プロトコルまたは SSP のプロトコルを使用して提供される特定の SCSI 論理ユニットのトラフィック統計情報を返します。

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
型の構造体[ **HBA\_ScsiId** ](https://msdn.microsoft.com/library/windows/hardware/ff557191) SCSI 論理ユニットを識別するために、オペレーティング システムによって使用される情報を格納します。

*HBAStatus*   
操作の状態。 使用できる値とその説明の一覧は、[HBA\_状態](hba-status.md)を参照してください。 ミニポート ドライバーでは、この情報を返します、SM の HBAStatus メンバー\_GetLUNStatistics\_構造体。

*ProtocolStatistics*   
型の構造体[ **MS\_SMHBA\_PROTOCOLSTATISTICS** ](https://msdn.microsoft.com/library/windows/hardware/ff563172)ポートでプロトコルのトラフィックの統計情報をレポートに使用されます。

<a name="return-value"></a>戻り値
------------

WMI メソッドには適用されません。

<a name="remarks"></a>注釈
-------

この WMI メソッドは、ミリ秒に属する\_SM\_TargetInformationMethods WMI クラスです。

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
<td align="left">Hbapiwmi.h</td>
</tr>
</tbody>
</table>

## <a name="span-idseealsospansee-also"></a><span id="see_also"></span>参照してください。


[HBA\_状態](hba-status.md)

[**SM\_GetLUNStatistics\_IN**](https://msdn.microsoft.com/library/windows/hardware/ff566238)

[**SM\_GetLUNStatistics\_アウト**](https://msdn.microsoft.com/library/windows/hardware/ff566241)

 

 






