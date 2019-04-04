---
title: ScsiInquiry 関数
description: ScsiInquiry WMI メソッドでは、指定されたデバイスを照会の SCSI コマンドを送信します。
ms.assetid: 31bde910-5a2a-4836-9096-d243c792e295
keywords:
- 記憶装置の ScsiInquiry 関数
topic_type:
- apiref
api_name:
- ScsiInquiry
api_location:
- Hbaapi.lib
- Hbaapi.dll
api_type:
- LibDef
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: c573cc59dd2510df307511d061f0e251170e3fde
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56570085"
---
# <a name="scsiinquiry-function"></a>ScsiInquiry 関数


**ScsiInquiry** WMI メソッドは、指定されたデバイスに SCSI 問い合わせコマンドを送信します。

<a name="syntax"></a>構文
------

```ManagedCPlusPlus
void ScsiInquiry(
   [out, HBA_STATUS_QUALIFIERS] HBA_STATUS      HBAStatus,
   [in] uint8                                   Cdb[6],
   [in, HBAType("HBA_WWN")] uint8               HbaPortWWN[8],
   [in, HBAType("HBA_WWN")] uint8               DiscoveredPortWWN[8],
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
に返された場合、操作の状態を格納します。 使用できる値とその説明の一覧は、[HBA\_状態](hba-status.md)を参照してください。 ミニポート ドライバーには、この情報が返されます、 **HBAStatus**のメンバー、 [ **ScsiInquiry\_アウト**](https://msdn.microsoft.com/library/windows/hardware/ff564604)構造体。

*Cdb*   
ターゲット デバイスに送信される SCSI 照会コマンドを保持するコマンドの記述子ブロックします。 この情報は、ミニポート ドライバーに配信される、 **Cdb**のメンバー、 [ **ScsiInquiry\_IN** ](https://msdn.microsoft.com/library/windows/hardware/ff564598)構造体。

*HbaPortWWN*   
ターゲットにアクセスする HBA の世界中の名前。 この情報は、ミニポート ドライバーに配信される、 **HbaPortWWN**のメンバー、 [ **ScsiInquiry\_IN** ](https://msdn.microsoft.com/library/windows/hardware/ff564598)構造体。

*DiscoveredPortWWN*   
ターゲット デバイスにアクセスするポートの世界中の名前。 この情報は、ミニポート ドライバーに配信される、 **DiscoveredPortWWN**のメンバー、 [ **ScsiInquiry\_IN** ](https://msdn.microsoft.com/library/windows/hardware/ff564598)構造体。

*FcLun*   
照会の SCSI コマンドを受信する論理ユニットの論理ユニットの数。 この情報は、ミニポート ドライバーに配信される、 **FcLun**のメンバー、 [ **ScsiInquiry\_IN** ](https://msdn.microsoft.com/library/windows/hardware/ff564598)構造体。

*ResponseBufferSize*   
SCSI 問い合わせコマンドの結果を保持するバッファーのバイト サイズ。 ミニポート ドライバーには、この情報が返されます、 **ResponseBufferSize**のメンバー、 [ **ScsiInquiry\_アウト**](https://msdn.microsoft.com/library/windows/hardware/ff564604)構造体。

*SenseBufferSize*   
SCSI のセンス データが格納されるバッファーのバイト単位のサイズは、SCSI 問い合わせコマンドの結果です。 ミニポート ドライバーには、この情報が返されます、 **SenseBufferSize**のメンバー、 [ **ScsiInquiry\_アウト**](https://msdn.microsoft.com/library/windows/hardware/ff564604)構造体。

*ScsiStatus*   
SCSI 問い合わせコマンドの状態。 ミニポート ドライバーには、この情報が返されます、 **ScsiStatus**のメンバー、 [ **ScsiInquiry\_アウト**](https://msdn.microsoft.com/library/windows/hardware/ff564604)構造体。

*ResponseBuffer*   
SCSI 問い合わせコマンドの結果。 ミニポート ドライバーには、この情報が返されます、 **ResponseBuffer**のメンバー、 [ **ScsiInquiry\_アウト**](https://msdn.microsoft.com/library/windows/hardware/ff564604)構造体。

*SenseBuffer*   
照会の SCSI コマンドに起因する SCSI センス データ。 ミニポート ドライバーには、この情報が返されます、 **SenseBuffer**のメンバー、 [ **ScsiInquiry\_アウト**](https://msdn.microsoft.com/library/windows/hardware/ff564604)構造体。

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


[HBA\_状態](hba-status.md)

[**ScsiInquiry\_IN**](https://msdn.microsoft.com/library/windows/hardware/ff564598)

[**ScsiInquiry\_OUT**](https://msdn.microsoft.com/library/windows/hardware/ff564604)

 

 






