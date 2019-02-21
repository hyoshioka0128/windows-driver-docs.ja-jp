---
title: IPrinterScriptUsbJobContext JobPropertyBag メソッド
description: 現在の印刷ジョブに関連付けられたプロパティ バッグを返します。
MSHAttr:
- PreferredSiteName:MSDN
- PreferredLib:/library/windows/hardware
ms.assetid: 6309CCD2-D53A-4B21-970E-AF19D1DACEE3
keywords:
- 印刷デバイスの JobPropertyBag メソッド
- JobPropertyBag メソッド、印刷デバイス IPrinterScriptUsbJobContext インターフェイス
- IPrinterScriptUsbJobContext インターフェイス、印刷デバイス JobPropertyBag メソッド
topic_type:
- apiref
api_name:
- IPrinterScriptUsbJobContext.JobPropertyBag
api_type:
- COM
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9f31afd0131ee0b0c89d83c0608108fbeacd8e8e
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56557655"
---
# <a name="iprinterscriptusbjobcontextjobpropertybag-method"></a>IPrinterScriptUsbJobContext::JobPropertyBag メソッド

現在の印刷ジョブに関連付けられたプロパティ バッグを返します。

<a name="syntax"></a>構文
------

```cpp
HRESULT JobPropertyBag(
  [out, retval] IPrinterScriptablePropertyBag **ppPropertyBag
);
```

<a name="parameters"></a>パラメーター
----------

*ppPropertyBag* \[out, retval\]  
現在の印刷ジョブに関連付けられたプロパティ バッグ。

<a name="return-value"></a>戻り値
------------

このメソッドが戻る、 **HRESULT**値。

<a name="remarks"></a>注釈
-------

**JobPropertyBag**は読み取り専用のメソッドです。 IHV JavaScript 関数は、このプロパティ バッグを使用して、プロパティまたは処理されている現在の印刷ジョブに固有のデータを格納できます。 このプロパティ バッグには、現在のジョブだけの期間が存在します。

<a name="requirements"></a>要件
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>サポートされている最小のクライアント</p></td>
<td><p>Windows 8.1</p></td>
</tr>
<tr class="even">
<td><p>サポートされている最小のサーバー</p></td>
<td><p>Windows Server 2012 R2</p></td>
</tr>
<tr class="odd">
<td><p>対象プラットフォーム</p></td>
<td>Desktop</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>関連項目

[**IPrinterScriptUsbJobContext**](iprinterscriptusbjobcontext.md)
