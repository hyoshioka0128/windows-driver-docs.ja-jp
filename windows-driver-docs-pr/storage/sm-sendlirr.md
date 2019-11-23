---
title: SM\_SendLIRR 関数
description: SM\_SendLIRR WMI メソッドは、指定されたローカルポートを介して、指定されたリモートポートにリンクインシデントレコード登録 (LIRR) コマンドを送信します。
ms.assetid: 52564ec3-4a42-4df0-b89f-2a8415404172
keywords:
- SM_SendLIRR 関数記憶装置
topic_type:
- apiref
api_name:
- SM_SendLIRR
api_location:
- Hbapiwmi.h
api_type:
- HeaderDef
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 0231e283b74e88a692be2d2194bb4def07f77322
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72845462"
---
# <a name="sm_sendlirr-function"></a>SM\_SendLIRR 関数


SM\_SendLIRR WMI メソッドは、指定されたローカルポートを介して、指定されたリモートポートにリンクインシデントレコード登録 (LIRR) コマンドを送信します。

<a name="syntax"></a>構文
------

```ManagedCPlusPlus
void SM_SendLIRR(
   [in, HBAType("HBA_WWN")]                    SourceWWN[8],
   [in, HBAType("HBA_WWN")]                    DestWWN[8],
   [in] uint8                                  Function,
   [in] uint8                                  Type,
   [in] uint32                                 InRespBufferMaxSize,
   [out, HBA_STATUS_QUALIFIERS] HBA_STATUS     HBAStatus,
   [out] uint32                                TotalRespBufferSize,
   [out] uint32                                OutRespBufferSize,
   [out, WmiSizeIs("OutRespBufferSize")] uint8 RespBuffer[]
);
```

<a name="parameters"></a>パラメーター
----------

*Sourcewwn*   
LIRR コマンドの送信に使用されるローカルポートのワールド名 (WWN)。 この情報は、構造内の SM\_SendLIRR\_の SourceWWN メンバーのミニポートドライバーに配信されます。

*Destwwn*   
宛先ポートのワールド名 (WWN)。 この情報は、構造内の SM\_SendLIRR\_の DestWWN メンバーのミニポートドライバーに配信されます。

*関数*   
実行する登録関数を識別するコード。 このメンバーに割り当てることができる値の説明については、T11 委員会のファイバーチャネルフレーミングとシグナリングの仕様を参照してください。 この情報は、構造内の SM\_SendLIRR\_の関数メンバーのミニポートドライバーに配信されます。

*型*   
リンク情報が要求されるデバイスの種類。 このメンバーに割り当てることができる値の説明については、T11 委員会の*ファイバーチャネルフレーミングとシグナリング*の仕様を参照してください。 この情報は、構造内の SM\_SendLIRR\_の関数メンバーのミニポートドライバーに配信されます。

*In火炎 Buffermaxsize*   
応答バッファーの最大サイズ (バイト単位)。

*Hbastatus*   
操作の状態。 許可される値とその説明の一覧については、「 [HBA\_STATUS](hba-status.md)」を参照してください。 ミニポートドライバーは、SM\_SendLIRR\_OUT 構造の HBAStatus メンバーにこの情報を返します。

*Total火炎 buffersize*   
LIRR コマンドの結果のサイズ (バイト単位)。 ミニポートドライバーは、SM\_SendLIRR\_OUT 構造体の Totalの値のメンバーにこの情報を返します。

* *  
実際に取得されたデータのサイズ (バイト単位)。 ミニポートドライバーは、SM\_SendLIRR\_OUT 構造体の外部のメンバーにこの情報を返します。

* *  
LIRR コマンドの結果。 ミニポートドライバーは、SM\_SendLIRR\_OUT 構造体の、この情報を返します。

<a name="return-value"></a>戻り値
------------

WMI メソッドには適用されません。

<a name="remarks"></a>注釈
-------

この WMI メソッドは、MS\_SM\_FabricAndDomainManagementMethods WMI クラスに属しています。

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

[**SM\_SendLIRR\_OUT**](https://docs.microsoft.com/windows-hardware/drivers/ddi/hbapiwmi/ns-hbapiwmi-_sm_sendlirr_out)

 

 






