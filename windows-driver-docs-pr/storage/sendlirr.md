---
title: SendLIRR 関数
description: SendLIRR WMI メソッドでは、リンクのインシデント レコードの登録 (LIRR) コマンドを指定のローカル ポートを介して、指定したリモート ポートに送信します。
ms.assetid: ca54161d-d5fe-4775-a38c-dfaf3fd8c00b
keywords:
- 記憶装置の SendLIRR 関数
topic_type:
- apiref
api_name:
- SendLIRR
api_location:
- Hbaapi.lib
- Hbaapi.dll
api_type:
- LibDef
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: d3d5fd4d4f87928abda7e1c91e3bc9a42e8e5c44
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67362674"
---
# <a name="sendlirr-function"></a>SendLIRR 関数


**SendLIRR** WMI メソッドは、指定したリモート ポートに示されたローカル ポートを通じてリンク インシデント レコードの登録 (LIRR) コマンドを送信します。

<a name="syntax"></a>構文
------

```ManagedCPlusPlus
void SendLIRR(
   [out, HBA_STATUS_QUALIFIERS] HBA_STATUS       HBAStatus,
   [in, HBAType("HBA_WWN")] uint8                SourceWWN[8],
   [in, HBAType("HBA_WWN")] uint8                DestWWN[8],
   [in] uint8                                    Function,
   [in] uint8                                    Type,
   [out] uint32                                  TotalRspBufferSize,
   [out] uint32                                  ActualRspBufferSize,
   [out, WmiSizeIs("ActualRspBufferSize")] uint8 RspBuffer[]
);
```

<a name="parameters"></a>パラメーター
----------

*HBAStatus*   
に返された場合、操作の状態を格納します。 使用できる値とその説明の一覧は、次を参照してください。 [HBA\_状態](hba-status.md)します。 ミニポート ドライバーには、この情報が返されます、 **HBAStatus**のメンバー、 [ **SendLIRR\_アウト**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/hbapiwmi/ns-hbapiwmi-_sendlirr_out)構造体。

*SourceWWN*   
LIRR コマンドを送信するローカル ポートに世界中の名前。 この情報は、ミニポート ドライバーに配信される、 **SourceWWN**のメンバー、 [ **SendLIRR\_IN** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/hbapiwmi/ns-hbapiwmi-_sendlirr_in)構造体。

*DestWWN*   
接続先ポートの世界中の名前。 この情報は、ミニポート ドライバーに配信される、 **DestWWN**のメンバー、 [ **SendLIRR\_IN** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/hbapiwmi/ns-hbapiwmi-_sendlirr_in)構造体。

*関数*   
登録関数を識別するコードの実行します。 詳細についてはこのメンバーにする値を割り当てることができます、T11 委員会を参照してください。*ファイバー チャネルのフレームとシグナリング*仕様。 この情報は、ミニポート ドライバーに配信される、**関数**のメンバー、 [ **SendLIRR\_IN** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/hbapiwmi/ns-hbapiwmi-_sendlirr_in)構造体。

*型*   
リンクの情報が要求されたデバイスの種類。 詳細についてはこのメンバーにする値を割り当てることができます、T11 委員会を参照してください。*ファイバー チャネルのフレームとシグナリング*仕様。 この情報は、ミニポート ドライバーに配信される、**関数**のメンバー、 [ **SendLIRR\_IN** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/hbapiwmi/ns-hbapiwmi-_sendlirr_in)構造体。

*TotalRspBufferSize*   
LIRR コマンドの結果のバイト単位のサイズ。 ミニポート ドライバーには、この情報が返されます、 **TotalRspBufferSize**のメンバー、 [ **SendLIRR\_アウト**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/hbapiwmi/ns-hbapiwmi-_sendlirr_out)構造体。

*ActualRspBufferSize*   
実際に取得されたデータのバイト単位のサイズ。 ミニポート ドライバーには、この情報が返されます、 **ActualRspBufferSize**のメンバー、 [ **SendLIRR\_アウト**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/hbapiwmi/ns-hbapiwmi-_sendlirr_out)構造体。

*RspBuffer*   
LIRR コマンドの結果。 ミニポート ドライバーには、この情報が返されます、 **RspBuffer**のメンバー、 [ **SendLIRR\_アウト**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/hbapiwmi/ns-hbapiwmi-_sendlirr_out)構造体。

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

[**SendLIRR\_IN**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/hbapiwmi/ns-hbapiwmi-_sendlirr_in)

[**SendLIRR\_アウト**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/hbapiwmi/ns-hbapiwmi-_sendlirr_out)

 

 






