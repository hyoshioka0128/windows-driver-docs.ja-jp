---
title: SM\_SendLIRR 関数
description: SM\_SendLIRR WMI メソッドは、指定したリモート ポートに示されたローカル ポートを通じてリンク インシデント レコードの登録 (LIRR) コマンドを送信します。
ms.assetid: 52564ec3-4a42-4df0-b89f-2a8415404172
keywords:
- 記憶装置の SM_SendLIRR 関数
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
ms.openlocfilehash: 59622f5b9150f7195c3cd172505be221bf83b1a3
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56551856"
---
# <a name="smsendlirr-function"></a>SM\_SendLIRR 関数


SM\_SendLIRR WMI メソッドは、指定したリモート ポートに示されたローカル ポートを通じてリンク インシデント レコードの登録 (LIRR) コマンドを送信します。

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

*SourceWWN*   
LIRR コマンドを送信するローカル ポートの世界中の名 (WWN)。 この情報は、SM の SourceWWN メンバーのミニポート ドライバーに配信\_SendLIRR\_構造体。

*DestWWN*   
接続先ポートの世界中の名 (WWN)。 この情報は、SM の DestWWN メンバーのミニポート ドライバーに配信\_SendLIRR\_構造体。

*関数*   
登録関数を識別するコードの実行します。 詳細についてはこのメンバーにする値を割り当てることができます、T11 委員会のファイバー チャネルのフレームとシグナリングの仕様を参照してください。 この情報は、SM の関数メンバーのミニポート ドライバーに配信\_SendLIRR\_構造体。

*型*   
リンクの情報が要求されたデバイスの種類。 詳細についてはこのメンバーにする値を割り当てることができます、T11 委員会を参照してください。*ファイバー チャネルのフレームとシグナリング*仕様。 この情報は、SM の関数メンバーのミニポート ドライバーに配信\_SendLIRR\_構造体。

*InRespBufferMaxSize*   
応答バッファーのバイト単位で最大サイズ。

*HBAStatus*   
操作の状態。 使用できる値とその説明の一覧は、[HBA\_状態](hba-status.md)を参照してください。 ミニポート ドライバーでは、この情報を返します、SM の HBAStatus メンバー\_SendLIRR\_構造体。

*TotalRespBufferSize*   
LIRR コマンドの結果のバイト単位のサイズ。 ミニポート ドライバーでは、この情報を返します、SM の TotalRespBufferSize メンバー\_SendLIRR\_構造体。

*OutRespBufferSize*   
実際に取得されたデータのバイト単位のサイズ。 ミニポート ドライバーでは、この情報を返します、SM の OutRespBufferSize メンバー\_SendLIRR\_構造体。

*RespBuffer*   
LIRR コマンドの結果。 ミニポート ドライバーでは、この情報を返します、SM の RespBuffer メンバー\_SendLIRR\_構造体。

<a name="return-value"></a>戻り値
------------

WMI メソッドには適用されません。

<a name="remarks"></a>注釈
-------

この WMI メソッドは、ミリ秒に属する\_SM\_FabricAndDomainManagementMethods WMI クラスです。

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

[**SM\_SendLIRR\_アウト**](https://msdn.microsoft.com/library/windows/hardware/ff566302)

 

 






