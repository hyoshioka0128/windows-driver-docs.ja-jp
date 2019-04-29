---
title: Iasphelp get\_双方向メソッド
description: 双方向のプロパティは、プリンターが両面印刷をサポートしているかを判断する ASP Web ページを使用できます。
MS-HAID:
- webfnc\_346f6357-9ca9-4b97-93a3-50ec9f28c118.xml
- print.iasphelp\_duplex
MSHAttr:
- PreferredSiteName:MSDN
- PreferredLib:/library/windows/hardware
ms.assetid: e837f8f2-68a5-4f9a-a253-dfcf33ea7047
keywords:
- 印刷デバイスの get_Duplex メソッド
- get_Duplex メソッド、印刷デバイス Iasphelp インターフェイス
- Iasphelp インターフェイス、印刷デバイス get_Duplex メソッド
topic_type:
- apiref
api_name:
- Iasphelp.get_Duplex
api_type:
- COM
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3eb48ac5aa4134c8b24cda828434a17c5c19e5f2
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63386625"
---
# <a name="iasphelpgetduplex-method"></a>Iasphelp::get\_双方向メソッド

**双方向**プロパティは、プリンターが両面印刷をサポートしているかを判断する ASP Web ページを使用できます。

<a name="syntax"></a>構文
------

```cpp
HRESULT get_Duplex(
  [out] BOOL *pVal
);
```

<a name="parameters"></a>パラメーター
----------

*pVal* \[out\]  
受信場所へのポインターの呼び出し元が指定**TRUE**プリンターが両面印刷をサポートしている場合または**FALSE**そうでない場合。

<a name="return-value"></a>戻り値
------------

Win32 エラー コードを返すこともできます。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>リターン コード</th>
<th>説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><strong>S_OK</strong></td>
<td><p>操作に成功しました。</p></td>
</tr>
<tr class="even">
<td><strong>E_HANDLE</strong></td>
<td><p><strong>Iasphelp::Open</strong>メソッドが呼び出されていません。</p></td>
</tr>
<tr class="odd">
<td><strong>E_OUTOFMEMORY</strong></td>
<td><p>メモリ不足。</p></td>
</tr>
</tbody>
</table>

## <a name="vbscript-example"></a>VBScript の例

[ **Iasphelp::Open** ](iasphelp-open.md)メソッドは、前に呼び出す必要があります、 **Iasphelp::Duplex**プロパティのクエリを実行できます。

```vb
Dim objPrinter, DoesDuplex
strPrinter = Session("MS_printer")
Set objPrinter = Server.CreateObject ("OlePrn.AspHelp")
objPrinter.Open strPrinter
DoesDuplex = objPrinter.Duplex
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
