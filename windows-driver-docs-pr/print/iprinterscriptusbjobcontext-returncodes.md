---
title: IPrinterScriptUsbJobContext 開始メソッド
description: IHV は、JavaScript 関数の定義のリターン コード値を提供できるオブジェクトを返します。
MSHAttr:
- PreferredSiteName:MSDN
- PreferredLib:/library/windows/hardware
ms.assetid: 0FD3A103-970E-4EB8-9867-7EC21273269C
keywords:
- 印刷デバイスの開始メソッド
- 開始メソッド、印刷デバイス IPrinterScriptUsbJobContext インターフェイス
- IPrinterScriptUsbJobContext インターフェイス印刷デバイス、開始メソッド
topic_type:
- apiref
api_name:
- IPrinterScriptUsbJobContext.ReturnCodes
api_type:
- COM
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9db76f31b4e7088d889b5fc07ef0d29109a1f047
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56539042"
---
# <a name="iprinterscriptusbjobcontextreturncodes-method"></a>IPrinterScriptUsbJobContext::ReturnCodes メソッド

IHV は、JavaScript 関数の定義のリターン コード値を提供できるオブジェクトを返します。

<a name="syntax"></a>構文
------

```cpp
HRESULT ReturnCodes(
  [out, retval] IPrinterScriptUsbJobContextReturnCodes **ppReturnCodes
);
```

<a name="parameters"></a>パラメーター
----------

*ppReturnCodes* \[out, retval\]  
IHV JavaScript 関数のリターン コード値。 リターン コード値がによって表される、 [ **IPrinterScriptUsbJobContextReturnCodes** ](iprinterscriptusbjobcontextreturncodes.md)インターフェイス。

<a name="return-value"></a>戻り値
------------

このメソッドが戻る、 **HRESULT**値。

<a name="remarks"></a>注釈
-------

IHV は、現在の印刷ジョブに関連付けられたプロパティ バッグを実装するインターフェイスを開発する必要があります。 IHV JavaScript 関数は、プロパティまたは処理されている現在の印刷ジョブに固有のデータを格納するのに、このプロパティ バッグを使用できます。 このプロパティ バッグには、現在のジョブだけの期間が存在します。

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

[**IPrinterScriptUsbJobContextReturnCodes**](iprinterscriptusbjobcontextreturncodes.md)
