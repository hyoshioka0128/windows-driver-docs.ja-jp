---
title: SM\_SetBindingSupport 関数
description: SM\_SetBindingSupport メソッドは、指定されたポートのバインド機能を設定します。
ms.assetid: 31a37fa5-db3c-4944-bf93-e221fb42dc6d
keywords:
- 記憶装置の SM_SetBindingSupport 関数
topic_type:
- apiref
api_name:
- SM_SetBindingSupport
api_location:
- Hbapiwmi.h
api_type:
- HeaderDef
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: c022ee410efb7d7e97fe9be62eeff5a6a535842d
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63384833"
---
# <a name="smsetbindingsupport-function"></a>SM\_SetBindingSupport 関数


SM\_SetBindingSupport メソッドは、指定されたポートのバインド機能を設定します。

<a name="syntax"></a>構文
------

```ManagedCPlusPlus
void SM_SetBindingSupport(
   [in, HBAType("HBA_WWN")] uint8                HbaPortWWN[8],
   [in, HBAType("HBA_WWN")] uint8                DomainPortWWN[8],
   [in, HBAType("SMHBA_BIND_CAPABILITY")] uint32 Flags,
   [out, HBA_STATUS_QUALIFIERS] HBA_STATUS       HBAStatus
);
```

<a name="parameters"></a>パラメーター
----------

*HbaPortWWN*   
永続的なバインドを取得するポートの世界中の名 (WWN)。

*DomainPortWWN*   
世界中のコールバック名 (WWN) ポートは\_を任意のポートの最小値を持つ識別子\_物理ファイバー チャネル ポートを使用して検出 SMP ポートの識別子。 値が 0 の物理ファイバー チャネル ポートを使用して SMP ポートが検出されない場合があります。

*フラグ*   
永続的なバインディングに関連する機能の特定のセットを提供するには、HBA の機能とそのミニポート ドライバーを示すビットマップ。 このパラメーターには値の一覧は、HBA の説明を参照してください。\_バインド\_型 WMI クラスの修飾子。

*HBAStatus*   
操作の状態。 使用できる値とその説明の一覧は、次を参照してください。 [HBA\_状態](hba-status.md)します。 ミニポート ドライバーでは、この情報を返します、SetBindingSupport の HBAStatus メンバー\_構造体。

<a name="return-value"></a>戻り値
------------

WMI メソッドには適用されません。

<a name="remarks"></a>注釈
-------

この WMI メソッドは、ミリ秒に属する\_SM\_TargetInformationMethods WMI クラスです。

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

[**SM\_SetBindingSupport\_IN**](https://msdn.microsoft.com/library/windows/hardware/ff566330)

[**SM\_SetBindingSupport\_アウト**](https://msdn.microsoft.com/library/windows/hardware/ff566331)

 

 






