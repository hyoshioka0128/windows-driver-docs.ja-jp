---
title: SM\_ScsiInquiry 関数
description: SM\_ScsiInquiry WMI メソッドは、指定されたデバイスに SCSI 照会コマンドを送信します。
ms.assetid: 7af1c25a-1823-49e0-a2c5-6533bd22f606
keywords:
- SM_ScsiInquiry 関数記憶装置
topic_type:
- apiref
api_name:
- SM_ScsiInquiry
api_location:
- Hbapiwmi.h
api_type:
- HeaderDef
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: d63d1cdb083e32003ae24d73504e2693585e7a12
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72845469"
---
# <a name="sm_scsiinquiry-function"></a>SM\_ScsiInquiry 関数


SM\_ScsiInquiry WMI メソッドは、指定されたデバイスに SCSI 照会コマンドを送信します。

<a name="syntax"></a>構文
------

```ManagedCPlusPlus
void SM_ScsiInquiry(
   [in, HBAType("HBA_WWN")] uint8               HbaPortWWN[8],
   [in, HBAType("HBA_WWN")] uint8               DiscoveredPortWWN[8],
   [in, HBAType("HBA_WWN")] uint8               DomainPortWWN[8],
   [in, HBAType("HBA_SCSILUN")] uint64          SmhbaLUN,
   [in] uint8                                   Cdb[6],
   [in] uint32                                  InRespBufferMaxSize,
   [in] uint32                                  InSenseBufferMaxSize,
   [out, HBA_STATUS_QUALIFIERS] HBA_STATUS      HBAStatus,
   [out] uint8                                  ScsiStatus,
   [out] uint32                                 OutRespBufferSize,
   [out] uint32                                 OutSenseBufferSize,
   [out, WmiSizeIs("OutRespBufferSize")] uint8  RespBuffer[],
   [out, WmiSizeIs("OutSenseBufferSize")] uint8 SenseBuffer[]
);
```

<a name="parameters"></a>パラメーター
----------

*HbaPortWWN*   
ターゲットへのアクセスに使用される HBA のワールド名 (WWN)。 この情報は、構造体の[**ScsiInquiry\_** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/iscsiop/ns-iscsiop-_scsiinquiry_in)の HbaPortWWN メンバーのミニポートドライバーに配信されます。

*DiscoveredPortWWN*   
ターゲットデバイスへのアクセスに使用するポートのワールド名 (WWN)。 この情報は、構造体の[**ScsiInquiry\_** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/iscsiop/ns-iscsiop-_scsiinquiry_in)の DiscoveredPortWWN メンバーのミニポートドライバーに配信されます。

*DomainPortWWN*   
コールバックのワールド名 (WWN)。 これは、物理ポートを使用して検出された SMP ポートの任意のポート\_識別子の最小値を持つポート\_識別子です。 物理ポートを使用して SMP ポートが検出されていない場合、この値は0になります。

*Smh定率*   
SCSI 照会コマンドを受信する論理ユニットの論理ユニット番号。 この情報は、構造[**内の ScsiInquiry\_** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/iscsiop/ns-iscsiop-_scsiinquiry_in)の Smh定率解除メンバーのミニポートドライバーに配信されます。

*Cdb*   
ターゲットデバイスに送信される SCSI 照会コマンドを保持するコマンド記述子ブロック。 この情報は、構造[**内の ScsiInquiry\_** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/iscsiop/ns-iscsiop-_scsiinquiry_in)の Cdb メンバーのミニポートドライバーに配信されます。

*In火炎 Buffermaxsize*   
応答バッファーの最大サイズ (バイト単位)。

*Insensebuffermaxsize*   
応答内のセンスバッファーの最大サイズ (バイト単位)。

*Hbastatus*   
操作の状態。 許可される値とその説明の一覧については、「 [HBA\_STATUS](hba-status.md)」を参照してください。 ミニポートドライバーは、 [**ScsiInquiry\_OUT**](https://docs.microsoft.com/windows-hardware/drivers/ddi/iscsiop/ns-iscsiop-_scsiinquiry_out)構造体の HBAStatus メンバーにこの情報を返します。

*ScsiStatus*   
SCSI 照会コマンドの状態。 ミニポートドライバーは、 [**ScsiInquiry\_OUT**](https://docs.microsoft.com/windows-hardware/drivers/ddi/iscsiop/ns-iscsiop-_scsiinquiry_out)構造体の ScsiStatus メンバーにこの情報を返します。

* *  
SCSI 照会コマンドの結果を保持するバッファーのサイズ (バイト単位)。 ミニポートドライバーは、 [**ScsiInquiry\_OUT**](https://docs.microsoft.com/windows-hardware/drivers/ddi/iscsiop/ns-iscsiop-_scsiinquiry_out)構造体の responsebuffersize メンバーにこの情報を返します。

*Outsensebuffersize*   
SCSI 照会コマンドの結果として生成される SCSI センスデータを保持するバッファーのサイズ (バイト単位)。 ミニポートドライバーは、 [**ScsiInquiry\_OUT**](https://docs.microsoft.com/windows-hardware/drivers/ddi/iscsiop/ns-iscsiop-_scsiinquiry_out)構造体の SenseBufferSize メンバーでこの情報を返します。

* *  
SCSI 照会コマンドの結果。 ミニポートドライバーは、 [**ScsiInquiry\_OUT**](https://docs.microsoft.com/windows-hardware/drivers/ddi/iscsiop/ns-iscsiop-_scsiinquiry_out)構造体の responsebuffer メンバーでこの情報を返します。

*Sensebuffer*   
SCSI 照会コマンドの結果として生成される SCSI sense データ。 ミニポートドライバーは、 [**ScsiInquiry\_OUT**](https://docs.microsoft.com/windows-hardware/drivers/ddi/iscsiop/ns-iscsiop-_scsiinquiry_out)構造体の SenseBuffer メンバーでこの情報を返します。

<a name="return-value"></a>戻り値
------------

WMI メソッドには適用されません。

<a name="remarks"></a>注釈
-------

この WMI メソッドは、MS\_SM\_ScsiInformationMethods WMI クラスに属しています。

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

 

 






