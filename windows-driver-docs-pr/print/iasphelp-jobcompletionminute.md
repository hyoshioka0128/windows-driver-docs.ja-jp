---
title: Iasphelp get\_JobCompletionMinute メソッド
description: JobCompletionMinute プロパティは、現在保留になっている印刷ジョブが完了する時期を決定する ASP Web ページを使用できます。
MS-HAID:
- webfnc\_63bca3eb-0ead-4430-8e82-9014d58c133b.xml
- print.iasphelp\_jobcompletionminute
MSHAttr:
- PreferredSiteName:MSDN
- PreferredLib:/library/windows/hardware
ms.assetid: e3dba870-84b4-4959-8ed4-102ac82be14b
keywords:
- 印刷デバイスの get_JobCompletionMinute メソッド
- get_JobCompletionMinute メソッド、印刷デバイス Iasphelp インターフェイス
- Iasphelp インターフェイス、印刷デバイス get_JobCompletionMinute メソッド
topic_type:
- apiref
api_name:
- Iasphelp.get_JobCompletionMinute
api_type:
- COM
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c50ccdeb1454a184cfaac36460a0f9fb6bfed3ee
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56559083"
---
# <a name="iasphelpgetjobcompletionminute-method"></a>Iasphelp::get\_JobCompletionMinute メソッド

**JobCompletionMinute**プロパティは現在保留中の印刷ジョブの完了すると判断する ASP Web ページを使用できます。

<a name="syntax"></a>構文
------

```cpp
HRESULT get_JobCompletionMinute(
  [out] long *pVal
);
```

<a name="parameters"></a>パラメーター
----------

*pVal* \[out\]  
現在完了待ちになっているすべての印刷ジョブ (分)、必要な時間を受信するメモリ位置への呼び出し元が指定のポインター。

<a name="return-value"></a>戻り値
------------

このプロパティは、次の表に、値のいずれかを返します。

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

このプロパティのクエリを実行する前に呼び出す、 [ **Iasphelp::CalcJobETA** ](iasphelp-calcjobeta.md)プロパティの値を初期化します。 保留中の印刷ジョブの数を確認するのには、クエリ、 [ **Iasphelp::PendingJobCount** ](iasphelp-pendingjobcount.md)プロパティ。

```vb
Dim objPrinter, EndMinute
strPrinter = Session("MS_printer")
Set objPrinter = Server.CreateObject ("OlePrn.AspHelp")
objPrinter.Open strPrinter
objPrinter.CalcJobETA
EndMinute = objPrinter.JobCompletionMinute
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

[**Iasphelp::CalcJobETA**](iasphelp-calcjobeta.md)

[**Iasphelp::PendingJobCount**](iasphelp-pendingjobcount.md)
