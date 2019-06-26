---
title: SM\_GetBindingSupport 関数
description: SM\_GetBindingSupport メソッドは、指定されたポートが現在有効になっているバインディング機能を取得します。
ms.assetid: 0ca24cdf-b589-4096-a490-2acfdd576a91
keywords:
- 記憶装置の SM_GetBindingSupport 関数
topic_type:
- apiref
api_name:
- SM_GetBindingSupport
api_location:
- Hbapiwmi.h
api_type:
- HeaderDef
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 01dee510e2802b333174c24cf64aa222ccee9c1e
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67384315"
---
# <a name="smgetbindingsupport-function"></a>SM\_GetBindingSupport 関数


SM\_GetBindingSupport メソッドは、指定されたポートが現在有効になっているバインディング機能を取得します。

<a name="syntax"></a>構文
------

```ManagedCPlusPlus
void SM_GetBindingSupport(
   [in, HBAType("HBA_WWN")] uint8                 HbaPortWWN[8],
   [in, HBAType("HBA_WWN")] uint8                 DomainPortWWN[8],
   [out, HBA_STATUS_QUALIFIERS] HBA_STATUS        HBAStatus,
   [out, HBAType("SMHBA_BIND_CAPABILITY")] uint32 Flags
);
```

<a name="parameters"></a>パラメーター
----------

*HbaPortWWN*   
永続的なバインドを取得するポートの世界中の名 (WWN)。

*DomainPortWWN*   
世界中のコールバック名 (WWN) ポートは\_を任意のポートの最小値を持つ識別子\_物理ファイバー チャネル ポートを使用して検出された SMP ポートの識別子。 値が 0 の物理ファイバー チャネル ポートを使用して SMP ポートが検出されない場合があります。

*HBAStatus*   
操作の状態。 使用できる値とその説明の一覧は、次を参照してください。、 [HBA\_状態](hba-status.md)構造体。 ミニポート ドライバーでは、この情報を返します、GetBindingSupport の HBAStatus メンバー\_構造体。

*フラグ*   
永続的なバインディングに関連する機能の特定のセットを提供するには、HBA の機能とそのミニポート ドライバーを示すビットマップ。 このパラメーターには値の一覧は、HBA の説明を参照してください。\_バインド\_型 WMI クラスの修飾子。

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

[**SM\_GetBindingSupport\_IN**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/hbapiwmi/ns-hbapiwmi-_sm_getbindingsupport_in)

[**SM\_GetBindingSupport\_アウト**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/hbapiwmi/ns-hbapiwmi-_sm_getbindingsupport_out)

 

 






