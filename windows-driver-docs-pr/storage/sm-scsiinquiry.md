---
title: SM\_ScsiInquiry 関数
description: SM\_ScsiInquiry WMI メソッドは、指定されたデバイスに SCSI 問い合わせコマンドを送信します。
ms.assetid: 7af1c25a-1823-49e0-a2c5-6533bd22f606
keywords:
- 記憶装置の SM_ScsiInquiry 関数
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
ms.openlocfilehash: b2f50483830906a913e0aa6a40df8ff0c30eb8d0
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67384297"
---
# <a name="smscsiinquiry-function"></a>SM\_ScsiInquiry 関数


SM\_ScsiInquiry WMI メソッドは、指定されたデバイスに SCSI 問い合わせコマンドを送信します。

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
ターゲットにアクセスする HBA の世界中の名 (WWN)。 この情報は、の HbaPortWWN メンバーでは、ミニポート ドライバーに配信される、 [ **ScsiInquiry\_IN** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/iscsiop/ns-iscsiop-_scsiinquiry_in)構造体。

*DiscoveredPortWWN*   
ターゲット デバイスにアクセスするポートの世界中の名 (WWN)。 この情報は、の DiscoveredPortWWN メンバーでは、ミニポート ドライバーに配信される、 [ **ScsiInquiry\_IN** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/iscsiop/ns-iscsiop-_scsiinquiry_in)構造体。

*DomainPortWWN*   
世界中のコールバック名 (WWN) ポートは\_を任意のポートの最小値を持つ識別子\_物理ポートを使用して検出された SMP ポートの識別子。 値が 0 の物理ポートを使用して SMP ポートが検出されない場合があります。

*SmhbaLUN*   
照会の SCSI コマンドを受信する論理ユニットの論理ユニットの数。 この情報は、の SmhbaLUN メンバーでは、ミニポート ドライバーに配信される、 [ **ScsiInquiry\_IN** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/iscsiop/ns-iscsiop-_scsiinquiry_in)構造体。

*Cdb*   
ターゲット デバイスに送信される SCSI 照会コマンドを保持するコマンドの記述子ブロックします。 この情報は、の Cdb メンバーでは、ミニポート ドライバーに配信される、 [ **ScsiInquiry\_IN** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/iscsiop/ns-iscsiop-_scsiinquiry_in)構造体。

*InRespBufferMaxSize*   
応答バッファーのバイト単位で最大サイズ。

*InSenseBufferMaxSize*   
応答に意味がバッファーのバイト単位で最大サイズ。

*HBAStatus*   
操作の状態。 使用できる値とその説明の一覧は、次を参照してください。 [HBA\_状態](hba-status.md)します。 ミニポート ドライバーでは、この情報を返しますの HBAStatus メンバーでは、 [ **ScsiInquiry\_アウト**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/iscsiop/ns-iscsiop-_scsiinquiry_out)構造体。

*ScsiStatus*   
SCSI 問い合わせコマンドの状態。 ミニポート ドライバーでは、この情報を返しますの ScsiStatus メンバーでは、 [ **ScsiInquiry\_アウト**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/iscsiop/ns-iscsiop-_scsiinquiry_out)構造体。

*OutRespBufferSize*   
SCSI 問い合わせコマンドの結果を保持するバッファーのバイト単位のサイズ。 ミニポート ドライバーでは、この情報を返しますの ResponseBufferSize メンバーでは、 [ **ScsiInquiry\_アウト**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/iscsiop/ns-iscsiop-_scsiinquiry_out)構造体。

*OutSenseBufferSize*   
照会の SCSI コマンドに起因する SCSI 意味データを保持するバッファーのバイト単位のサイズ。 ミニポート ドライバーでは、この情報を返しますの SenseBufferSize メンバーでは、 [ **ScsiInquiry\_アウト**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/iscsiop/ns-iscsiop-_scsiinquiry_out)構造体。

*RespBuffer*   
SCSI 問い合わせコマンドの結果。 ミニポート ドライバーでは、この情報を返しますの ResponseBuffer メンバーでは、 [ **ScsiInquiry\_アウト**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/iscsiop/ns-iscsiop-_scsiinquiry_out)構造体。

*SenseBuffer*   
照会の SCSI コマンドに起因する SCSI センス データ。 ミニポート ドライバーでは、この情報を返しますの SenseBuffer メンバーでは、 [ **ScsiInquiry\_アウト**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/iscsiop/ns-iscsiop-_scsiinquiry_out)構造体。

<a name="return-value"></a>戻り値
------------

WMI メソッドには適用されません。

<a name="remarks"></a>注釈
-------

この WMI メソッドは、ミリ秒に属する\_SM\_ScsiInformationMethods WMI クラスです。

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

 

 






