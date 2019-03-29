---
title: Iasphelp get\_LongPaperName メソッド
description: LongPaperName プロパティは、用紙の短い名前を用紙の長い名前に変換する ASP Web ページを使用できます。
MS-HAID:
- webfnc\_17250b54-29f4-41c5-bdf2-b72e0823d8e4.xml
- print.iasphelp\_longpapername
MSHAttr:
- PreferredSiteName:MSDN
- PreferredLib:/library/windows/hardware
ms.assetid: 14e6d6db-c429-4d80-840b-c4e0102c9380
keywords:
- 印刷デバイスの get_LongPaperName メソッド
- get_LongPaperName メソッド、印刷デバイス Iasphelp インターフェイス
- Iasphelp インターフェイス、印刷デバイス get_LongPaperName メソッド
topic_type:
- apiref
api_name:
- Iasphelp.get_LongPaperName
api_type:
- COM
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: cda3f8b569ca82bcdef8892db983e07b7b0feb78
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56580101"
---
# <a name="iasphelpgetlongpapername-method"></a>Iasphelp::get\_LongPaperName メソッド

**LongPaperName**プロパティは、用紙の短い名前を用紙の長い名前に変換する ASP Web ページを使用できます。

<a name="syntax"></a>構文
------

```cpp
HRESULT get_LongPaperName(
  [in]  BSTR bstrShortName,
  [out] BSTR *pVal
);
```

<a name="parameters"></a>パラメーター
----------

*bstrShortName* \[in\]  
用紙の短い名前を含む文字列への呼び出し元が指定のポインター。

*pVal* \[out\]  
用紙の名前を含む文字列へのポインターを受信する呼び出し元が指定の場所。

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
<td><strong>E_POINTER</strong></td>
<td><p>有効なメモリの場所に少なくとも 1 つのパラメーターが指していません。</p></td>
</tr>
<tr class="odd">
<td><strong>E_OUTOFMEMORY</strong></td>
<td><p>メモリ不足です。</p></td>
</tr>
</tbody>
</table>

## <a name="vbscript-example"></a>VBScript の例

```vb
Dim objPrinter, LongName
Set objPrinter = Server.CreateObject ("OlePrn.AspHelp")
LongName = objPrinter.LongPaperName("iso-a0")
```

<a name="requirements"></a>必要条件
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
