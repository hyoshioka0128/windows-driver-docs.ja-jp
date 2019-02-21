---
title: Iasphelp get\_Status メソッド
description: Status プロパティは、プリンターの状態を確認する ASP Web ページを使用します。
MS-HAID:
- webfnc\_30feffa7-1aa0-4b66-9d0a-1f66025272c3.xml
- print.iasphelp\_status
MSHAttr:
- PreferredSiteName:MSDN
- PreferredLib:/library/windows/hardware
ms.assetid: cff9dd7d-722b-4917-84ca-d6b17e8e64a4
keywords:
- get_Status メソッド印刷デバイス
- get_Status メソッド、印刷デバイス Iasphelp インターフェイス
- Iasphelp インターフェイス、印刷デバイス get_Status メソッド
topic_type:
- apiref
api_name:
- Iasphelp.get_Status
api_type:
- COM
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 69bd9d6bbf5284ec1676acafc7677186caf2b19b
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56560269"
---
# <a name="iasphelpgetstatus-method"></a>Iasphelp::get\_Status メソッド

**状態**プロパティは、プリンターの状態を確認する ASP Web ページを使用できます。

<a name="syntax"></a>構文
------

```cpp
HRESULT get_Status(
  [out] long *pVal
);
```

<a name="parameters"></a>パラメーター
----------

*pVal* \[out\]  
プリンターの状態フラグを受信する場所への呼び出し元が指定のポインター。 詳細については、次の「解説」を参照してください。

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
<td><strong>S_OK を返します</strong></td>
<td><p>操作に成功しました。</p></td>
</tr>
<tr class="even">
<td><strong>E_HANDLE</strong></td>
<td><p><a href="iasphelp-open.md" data-raw-source="[&lt;strong&gt;Iasphelp::Open&lt;/strong&gt;](iasphelp-open.md)"> <strong>Iasphelp::Open</strong> </a>メソッドが呼び出されていません。</p></td>
</tr>
<tr class="odd">
<td><strong>E_OUTOFMEMORY</strong></td>
<td><p>メモリ不足です。</p></td>
</tr>
</tbody>
</table>

## <a name="vbscript-example"></a>VBScript の例

プロパティの値は 0 または 1 つまたは複数のプリンターのビットごとの OR のいずれかであるプリンターのステータス コード\_状態\_*XXX*フラグ ヘッダーで定義されているファイルの Winspool.h、 **の状態**プリンターのメンバー\_情報\_2 構造体。 この構造体の詳細については、Windows SDK のドキュメントを参照してください。

[ **Iasphelp::Open** ](iasphelp-open.md)メソッドは、前に呼び出す必要があります、 **Iasphelp::Status**プロパティのクエリを実行できます。

```vb
Dim objPrinter, PtrStatus
strPrinter = Session("MS_printer")
Set objPrinter = Server.CreateObject ("OlePrn.AspHelp")
objPrinter.Open strPrinter
PtrStatus = objPrinter.Status
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
