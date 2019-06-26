---
title: SM\_RemoveTarget 関数
description: SM\_RemoveTarget WMI メソッドを WMI クライアントに指定されたターゲットに関連付けられているイベントを渡すことを停止するように、WMI プロバイダーを構成します。
ms.assetid: 9be2a40c-299a-4d92-b9a2-ef60eb6d90e9
keywords:
- 記憶装置の SM_RemoveTarget 関数
topic_type:
- apiref
api_name:
- SM_RemoveTarget
api_location:
- Hbapiwmi.h
api_type:
- HeaderDef
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 21ff7bacbebb76a7f10a361a05be93ea36b6de1e
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67384305"
---
# <a name="smremovetarget-function"></a>SM\_RemoveTarget 関数


SM\_RemoveTarget WMI メソッドを WMI クライアントに指定されたターゲットに関連付けられているイベントを渡すことを停止するように、WMI プロバイダーを構成します。

<a name="syntax"></a>構文
------

```ManagedCPlusPlus
void SM_RemoveTarget(
   [in, HBAType("HBA_WWN")] uint8          HbaPortWWN[8],
   [in, HBAType("HBA_WWN")] uint8          DiscoveredPortWWN[8],
   [in] uint32                             AllTargets,
   [out, HBA_STATUS_QUALIFIERS] HBA_STATUS HBAStatus
);
```

<a name="parameters"></a>パラメーター
----------

*HbaPortWWN*   
64 ビット世界名 (WWN) イベントは、WMI クライアントに報告するポートの一覧から削除するローカル ポートを一意に識別します。 世界中の名の詳細については、T11 委員会を参照してください。*ファイバー チャネル HBA API*仕様。

*DiscoveredPortWWN*   
イベントは、WMI クライアントに報告するポートの一覧から削除するか、リモート検出されたポートを示す世界中名 (WWN)。

*AllTargets*   
レポートを停止するイベントです。 このメンバーがゼロの場合、WMI プロバイダーのクライアントは DiscoveredPortWWN で示されたポートに関連付けられているイベントの報告を停止します。 このメンバーが 0 以外の場合は、WMI プロバイダーは、すべてのイベントには、どのターゲットが関連付けられているレポートを停止します。

*HBAStatus*   
操作の状態。 使用できる値とその説明の一覧は、次を参照してください。 [HBA\_状態](hba-status.md)します。 ミニポート ドライバーでは、この情報を返します、SM の HBAStatus メンバー\_RemoveTarget\_構造体。

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

[**SM\_RemoveTarget\_IN**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/hbapiwmi/ns-hbapiwmi-_sm_removetarget_in)

[**SM\_RemoveTarget\_アウト**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/hbapiwmi/ns-hbapiwmi-_sm_removetarget_out)

 

 






