---
title: SM\_GetBindingCapability 関数
description: SM\_GetBindingCapability メソッドは、指定されたポートのバインド機能を取得します。
ms.assetid: 11b7df8b-2694-4c49-a97a-ed475f3e841f
keywords:
- 記憶装置の SM_GetBindingCapability 関数
topic_type:
- apiref
api_name:
- SM_GetBindingCapability
api_location:
- Hbapiwmi.h
api_type:
- HeaderDef
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 89cf5cd97caac3b8eef64b46e0b919dc0c13c5cc
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63356702"
---
# <a name="smgetbindingcapability-function"></a>SM\_GetBindingCapability 関数


SM\_GetBindingCapability メソッドは、指定されたポートのバインド機能を取得します。

<a name="syntax"></a>構文
------

```ManagedCPlusPlus
void SM_GetBindingCapability(
   [in, HBAType("HBA_WWN")] uint8                 HbaPortWWN[8],
   [in, HBAType("HBA_WWN")] uint8                 DomainPortWWN[8],
   [out, HBA_STATUS_QUALIFIERS] HBA_STATUS        HBAStatus,
   [out, HBAType("SMHBA_BIND_CAPABILITY")] uint32 HBAType
);
```

<a name="parameters"></a>パラメーター
----------

*HbaPortWWN*   
永続的なバインドを取得するポートの世界中の名 (WWN)。

*DomainPortWWN*   
世界中のコールバック名 (WWN) ポートは\_を任意のポートの最小値を持つ識別子\_物理ファイバー チャネル ポートを使用して検出された SMP ポートの識別子。 値が 0 の物理ファイバー チャネル ポートを使用して SMP ポートが検出されない場合があります。

*HBAStatus*   
操作の状態。 使用できる値とその説明の一覧は、次を参照してください。、 [HBA\_状態](hba-status.md)構造体。 ミニポート ドライバーでは、この情報を返します、GetBindingCapability の HBAStatus メンバー\_構造体。

*HBAType*   
永続的なバインディングに関連する機能の特定のセットを提供する HBA とそのミニポート ドライバーの機能。 このパラメーターには値の一覧は、HBA の説明を参照してください。\_バインド\_型 WMI クラスの修飾子。

<a name="return-value"></a>戻り値
------------

WMI メソッドには適用されません。

<a name="remarks"></a>注釈
-------

SM\_GetBindingSupport メソッド返すは、現在有効になっているバインディング機能に対し、SM\_GetBindingCapability メソッドかどうかを指定せず、ポートのバインド機能を示す特定のバインド有効ですか。 この WMI メソッドは、ミリ秒に属する\_SM\_TargetInformationMethods WMI クラスです。

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

[**SM\_GetBindingCapability\_IN**](https://msdn.microsoft.com/library/windows/hardware/ff566224)

[**SM\_GetBindingCapability\_アウト**](https://msdn.microsoft.com/library/windows/hardware/ff566227)

 

 






