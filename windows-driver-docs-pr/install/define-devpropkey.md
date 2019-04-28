---
title: DEFINE_DEVPROPKEY
description: Windows Vista、Windows の以降のバージョンでは、DEFINE_DEVPROPKEY マクロは、統一されたデバイス プロパティのモデルでのデバイス プロパティのキーを表す DEVPROPKEY 構造体を作成します。
ms.assetid: 9723241d-939e-40b4-8f06-83c99b31c02e
keywords:
- DEFINE_DEVPROPKEY デバイスとドライバーのインストール
topic_type:
- apiref
api_name:
- DEFINE_DEVPROPKEY
api_location:
- Devpropdef.h
api_type:
- HeaderDef
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: bae16d094d3067ab461aa019a0d8c1a872947220
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63369486"
---
# <a name="definedevpropkey"></a>DEFINE_DEVPROPKEY


DEFINE_DEVPROPKEY マクロでは、Windows Vista および Windows の以降のバージョンでデバイス プロパティのキーを表す DEVPROPKEY 構造が作成、[統一されたデバイス プロパティのモデル](https://msdn.microsoft.com/library/windows/hardware/ff553515)します。

``` syntax
#ifdef INITGUID
#define DEFINE_DEVPROPKEY(name, l, w1, w2, b1, b2, b3, b4, b5, b6, b7, b8, pid) EXTERN_C const DEVPROPKEY DECLSPEC_SELECTANY name = { { l, w1, w2, { b1, b2,  b3,  b4,  b5,  b6,  b7,  b8 } }, pid }
#else
#define DEFINE_DEVPROPKEY(name, l, w1, w2, b1, b2, b3, b4, b5, b6, b7, b8, pid) EXTERN_C const DEVPROPKEY name
#endif // INITGUID
```

## <a name="members"></a>メンバー


<a href="" id="name"></a>*name*  
デバイス プロパティのキーを表す DEVPROPKEY 構造体の名前。

<a href="" id="l"></a>*L*  
値を提供する符号なしの時間の長いに型指定された変数、 **data1** DEVPROPKEY 構造体の fmtid メンバーのメンバー。

<a href="" id="w1"></a>*w1*  
値を指定する符号なしの short 型の変数、 **data2**のメンバー、 **fmtid** DEVPROPKEY 構造体のメンバー。

<a href="" id="w2"></a>*w2*  
値を指定する符号なしの short 型の変数、 **data3**のメンバー、 **fmtid** DEVPROPKEY 構造体のメンバー。

<a href="" id="b1"></a>*B1*  
バイトに型指定された変数の値を提供する、 **data4\[0\]** のメンバー、 **fmtid** DEVPROPKEY 構造体のメンバー。

<a href="" id="b2"></a>*b2*  
バイトに型指定された変数の値を提供する、 **data4\[1\]** のメンバー、 **fmtid** DEVPROPKEY 構造体のメンバー。

<a href="" id="b3"></a>*b3*  
バイトに型指定された変数の値を提供する、 **data4\[2\]** のメンバー、 **fmtid** DEVPROPKEY 構造体のメンバー。

<a href="" id="b4"></a>*B4*  
バイトに型指定された変数の値を提供する、 **data4\[3\]** のメンバー、 **fmtid** DEVPROPKEY 構造体のメンバー。

<a href="" id="b5"></a>*b5*  
バイトに型指定された変数の値を提供する、 **data4\[4\]** のメンバー、 **fmtid** DEVPROPKEY 構造体のメンバー。

<a href="" id="b6"></a>*B6*  
バイトに型指定された変数の値を提供する、 **data4\[5\]** のメンバー、 **fmtid** DEVPROPKEY 構造体のメンバー。

<a href="" id="b7"></a>*b7*  
バイトに型指定された変数の値を提供する、 **data4\[6\]** のメンバー、 **fmtid** DEVPROPKEY 構造体のメンバー。

<a href="" id="b8"></a>*b8*  
バイトに型指定された変数の値を提供する、 **data4\[7\]** のメンバー、 **fmtid** DEVPROPKEY 構造体のメンバー。

<a href="" id="pid"></a>*pid*  
DEVPROPID に型指定された変数の値を提供する、 **pid** DEVPROPKEY 構造体のメンバーを (プロパティの識別子)。 プロパティの識別子は、2 つ以上である必要があります。

<a name="remarks"></a>注釈
-------

DEFINE_DEVPROPKEY 構造がの一部、[統一されたデバイス プロパティのモデル](https://msdn.microsoft.com/library/windows/hardware/ff553515)します。

DEFINE_DEVPROPKEY マクロは、作成に使用できる、 [ **DEVPROPKEY** ](https://msdn.microsoft.com/library/windows/hardware/ff543544)カスタム デバイス プロパティを表す構造体です。

<a name="requirements"></a>要件
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p>Header</p></td>
<td align="left">Devpropdef.h (Devpropdef.h を含む)</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>関連項目


[**DEVPROPKEY**](https://msdn.microsoft.com/library/windows/hardware/ff543544)

 

 






