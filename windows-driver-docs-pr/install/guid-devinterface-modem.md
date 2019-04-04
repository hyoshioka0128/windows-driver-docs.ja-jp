---
title: GUID_DEVINTERFACE_MODEM
description: GUID_DEVINTERFACE_MODEM
ms.assetid: 80f5c063-8b22-422f-8102-4ac1e62241c8
keywords:
- GUID_DEVINTERFACE_MODEM デバイスとドライバーのインストール
topic_type:
- apiref
api_name:
- GUID_DEVINTERFACE_MODEM
api_location:
- Ntddmodm.h
api_type:
- HeaderDef
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 9f8776a4c7b6a684ccb1d216bf8bf519d78e6482
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56527887"
---
# <a name="guiddevinterfacemodem"></a>GUID_DEVINTERFACE_MODEM


GUID_DEVINTERFACE_MODEM[デバイス インターフェイス クラス](https://msdn.microsoft.com/library/windows/hardware/ff541339)が定義されている[モデム デバイス](https://msdn.microsoft.com/library/windows/hardware/ff542573)します。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">属性</th>
<th align="left">設定</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>識別子</p></td>
<td align="left"><p>GUID_DEVINTERFACE_MODEM</p></td>
</tr>
<tr class="even">
<td align="left"><p>クラス GUID</p></td>
<td align="left"><p>{2C7089AA-2E0E-11D1-B114-00C04FC2AAE4}</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>注釈
-------

モデム デバイス用のドライバーでは、オペレーティング システムとモデム デバイスの存在をアプリケーションに通知するこのデバイスのインターフェイス クラスのインスタンスを登録します。

GUID_DEVINTERFACE_MODEM *Ntddmodm.h*のインクルードする前に、正しいバージョンの INITGUID と DEFINE_GUID マクロが定義されている場合にのみ正しく定義する*Ntddmodm.h*します。 DEFINE_GUID マクロが定義されている、 *Guiddef.h*します。 INITGUID、DEFINE_GUID、および GUID_DEVINTERFACE_MODEM が正しく定義されていることを確認するには、ヘッダー ファイルに次のコードを含めます。

```cpp
#ifndef INITGUID
#define INITGUID
#include <guiddef.h>
#undef INITGUID
#else 
#include <guiddef.h>
#endif

#include <ntddmodm.h>
...
```

モデム デバイスについては、[モデム デバイスの設計ガイド](https://msdn.microsoft.com/library/windows/hardware/ff542476)を参照してください。

このデバイスのインターフェイス クラスを使用しての例は、次を参照してください。、 [FakeModem - ユニモデム コント ローラーのないモデム サンプル ドライバー](https://go.microsoft.com/fwlink/p/?linkid=256110) WDK で提供されるサンプル。

[**GUID_CLASS_MODEM** ](guid-class-modem.md)このデバイス インターフェイス クラスの古い形式の識別子は、このクラスの新しいインスタンスが GUID_DEVINTERFACE_MODEM を代わりに使用します。

<a name="requirements"></a>要件
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p>バージョン</p></td>
<td align="left"><p>Microsoft Windows 2000 および以降のバージョンの Windows で使用できます。</p></td>
</tr>
<tr class="even">
<td align="left"><p>Header</p></td>
<td align="left">Ntddmodm.h (include Ntddmodm.h)</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>関連項目


[**GUID_CLASS_MODEM**](guid-class-modem.md)

 

 






