---
title: SM\_RemovePort 関数
description: SM\_RemovePort WMI メソッドを WMI クライアントに指定されたポートに関連付けられているイベントを渡すことを停止するように、WMI プロバイダーを構成します。
ms.assetid: aa868e5d-32d3-4bb0-9128-5f213bf62146
keywords:
- 記憶装置の SM_RemovePort 関数
topic_type:
- apiref
api_name:
- SM_RemovePort
api_location:
- Hbapiwmi.h
api_type:
- HeaderDef
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 148989e8ba7bcbd2d18c7bfb109432bdb2377aac
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67384302"
---
# <a name="smremoveport-function"></a>SM\_RemovePort 関数


SM\_RemovePort WMI メソッドを WMI クライアントに指定されたポートに関連付けられているイベントを渡すことを停止するように、WMI プロバイダーを構成します。

<a name="syntax"></a>構文
------

```ManagedCPlusPlus
void SM_RemovePort(
   [in, HBAType("HBA_WWN")] uint8          PortWWN[8],
   [in, EVENT_TYPES_QUALIFIERS] uint32     EventType,
   [out, HBA_STATUS_QUALIFIERS] HBA_STATUS HBAStatus
);
```

<a name="parameters"></a>パラメーター
----------

*PortWWN*   
イベントは、WMI クライアントに報告するポートの一覧から削除するポートを示す世界中名 (WWN)。

*イベントの種類*   
イベントの種類。 このメンバーに割り当てることができる値は、イベントによって定義されます\_型\_修飾子の WMI クラスの修飾子。

*HBAStatus*   
操作の状態。 使用できる値とその説明の一覧は、次を参照してください。 [HBA\_状態](hba-status.md)します。 ミニポート ドライバーでは、この情報を返します、SM の HBAStatus メンバー\_RemovePort\_構造体。

<a name="return-value"></a>戻り値
------------

WMI メソッドには適用されません。

<a name="remarks"></a>注釈
-------

この WMI メソッドは、ミリ秒に属する\_SM\_EventControl WMI クラスです。

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

[**SM\_RemovePort\_IN**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/hbapiwmi/ns-hbapiwmi-_sm_removeport_in)

[**SM\_RemovePort\_アウト**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/hbapiwmi/ns-hbapiwmi-_sm_removeport_out)

 

 






