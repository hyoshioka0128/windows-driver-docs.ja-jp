---
title: Iasphelp Close メソッド
description: Close メソッドは、ASP Web ページをプリンターへのアクセスを終了できます。
MS-HAID:
- webfnc\_62b91ac5-2f01-44d6-9289-ee2136acacc4.xml
- print.iasphelp\_close
MSHAttr:
- PreferredSiteName:MSDN
- PreferredLib:/library/windows/hardware
ms.assetid: 45457eb9-a791-450f-b3fd-f4e7dabc7a70
keywords:
- 印刷デバイスの close メソッド
- Close メソッド、印刷デバイス Iasphelp インターフェイス
- Iasphelp インターフェイス印刷デバイス、Close メソッド
topic_type:
- apiref
api_name:
- Iasphelp.Close
api_type:
- COM
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 03d93d60dc290f9541bd404847dea130bbb07c49
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63362468"
---
# <a name="iasphelpclose-method"></a>Iasphelp::Close メソッド


**閉じます**メソッドにより、ASP Web ページをプリンターへのアクセスを閉じます。

<a name="syntax"></a>構文
------

```cpp
HRESULT Close();
```

<a name="parameters"></a>パラメーター
----------

このメソッドにはパラメーターはありません。

<a name="return-value"></a>戻り値
------------

戻り値は常に S\_ok をクリックします。


## <a name="vbscript-example"></a>VBScript の例

以前の呼び出しで閉じられているプリンターの名前が指定されている必要があります、 [ **Iasphelp::Open** ](iasphelp-open.md)メソッド。

```vb
Dim objPrinter
strPrinter = Session("MS_printer")
Set objPrinter = Server.CreateObject ("OlePrn.AspHelp")
objPrinter.Open strPrinter
...
objPrinter.Close
```

<a name="requirements"></a>要件
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>対象プラットフォーム</p></td>
<td>Desktop</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>関連項目

[**Iasphelp::Open**](iasphelp-open.md)
