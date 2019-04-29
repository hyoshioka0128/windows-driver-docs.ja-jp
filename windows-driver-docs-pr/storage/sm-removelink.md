---
title: SM\_RemoveLink 関数
description: SM\_RemoveLink WMI メソッドを WMI クライアント fabric リンク イベント情報を渡すことを停止するように、WMI プロバイダーを構成します。
ms.assetid: 25f6b807-f921-44b6-b087-e5c6ec8c72ec
keywords:
- 記憶装置の SM_RemoveLink 関数
topic_type:
- apiref
api_name:
- SM_RemoveLink
api_location:
- Hbapiwmi.h
api_type:
- HeaderDef
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: e8a12ed7cadcd80d0a588d96f14bc087a2d1bd85
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63339064"
---
# <a name="smremovelink-function"></a>SM\_RemoveLink 関数


SM\_RemoveLink WMI メソッドを WMI クライアント fabric リンク イベント情報を渡すことを停止するように、WMI プロバイダーを構成します。

<a name="syntax"></a>構文
------

```ManagedCPlusPlus
void SM_RemoveLink(
   [out, HBA_STATUS_QUALIFIERS] HBA_STATUS HBAStatus
);
```

<a name="parameters"></a>パラメーター
----------

*HBAStatus*   
操作の状態。 使用できる値とその説明の一覧は、次を参照してください。 [HBA\_状態](hba-status.md)します。 ミニポート ドライバーでは、この情報を返します、SM の HBAStatus メンバー\_RemoveLink\_構造体。

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

[**SM\_RemoveLink\_アウト**](https://msdn.microsoft.com/library/windows/hardware/ff566265)

 

 






