---
title: RemoveTarget 関数
description: RemoveTarget WMI メソッドは、WMI クライアントに指定されたターゲットに関連付けられたイベントを渡すことを停止するように、WMI プロバイダーを構成します。
ms.assetid: 413cee3c-5e3a-4012-925b-b4699fbd2e1b
keywords:
- 記憶装置の RemoveTarget 関数
topic_type:
- apiref
api_name:
- RemoveTarget
api_location:
- Hbapiwmi.h
api_type:
- HeaderDef
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: a1faffa08cb47dba596f0e6cb1fbdb34b2381689
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56577682"
---
# <a name="removetarget-function"></a>RemoveTarget 関数


**RemoveTarget** WMI メソッドを WMI クライアントに指定されたターゲットに関連付けられたイベントを渡すことを停止するように、WMI プロバイダーを構成します。

<a name="syntax"></a>構文
------

```ManagedCPlusPlus
void RemoveTarget(
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
イベントは、WMI クライアントに報告するポートの一覧から削除するか、リモート検出されたポートを示す WWN します。

*AllTargets*   
レポートを停止するイベントです。 このメンバーが 0 の場合は、WMI プロバイダーのクライアントはレポートで示されたポートに関連付けられたイベントに停止*DiscoveredPortWWN*します。 このメンバーが 0 以外の場合は、WMI プロバイダーは任意のターゲットがすべてのイベントに関連付けられているレポートを停止します。

*HBAStatus*   
に返された場合、操作の状態を格納します。 使用できる値とその説明の一覧は、[HBA\_状態](hba-status.md)を参照してください。 ミニポート ドライバーには、この情報が返されます、 **HBAStatus**のメンバー、 [ **RemoveTarget\_アウト**](https://msdn.microsoft.com/library/windows/hardware/ff564039)構造体。

<a name="return-value"></a>戻り値
------------

WMI メソッドには適用されません。

<a name="remarks"></a>コメント
-------

この WMI メソッドが属する、 [MSFC\_EventControl WMI クラス](msfc-eventcontrol-wmi-class.md)します。

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
</tbody>
</table>

## <a name="span-idseealsospansee-also"></a><span id="see_also"></span>参照してください。


[**RemoveTarget\_IN**](https://msdn.microsoft.com/library/windows/hardware/ff564033)

[**RemoveTarget\_アウト**](https://msdn.microsoft.com/library/windows/hardware/ff564039)

 

 






