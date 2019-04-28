---
title: Iasphelp get\_PendingJobCount メソッド
description: PendingJobCount プロパティは、保留中の印刷ジョブの数を決定する ASP Web ページを使用できます。
MS-HAID:
- webfnc\_fd1cbaac-f195-4a38-8788-990eb9b3fd6c.xml
- print.iasphelp\_pendingjobcount
MSHAttr:
- PreferredSiteName:MSDN
- PreferredLib:/library/windows/hardware
ms.assetid: e0d00abd-0b2a-403c-a7b2-f1f2587b977f
keywords:
- 印刷デバイスの get_PendingJobCount メソッド
- get_PendingJobCount メソッド、印刷デバイス Iasphelp インターフェイス
- Iasphelp インターフェイス、印刷デバイス get_PendingJobCount メソッド
topic_type:
- apiref
api_name:
- Iasphelp.get_PendingJobCount
api_type:
- COM
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7c7f5efc765e7422e0700169211963424b0ca8e9
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63361861"
---
# <a name="iasphelpgetpendingjobcount-method"></a>Iasphelp::get\_PendingJobCount メソッド

**PendingJobCount**プロパティは、保留中の印刷ジョブの数を決定する ASP Web ページを使用できます。

<a name="syntax"></a>構文
------

```cpp
HRESULT get_PendingJobCount(
  [out] long *pVal
);
```

<a name="parameters"></a>パラメーター
----------

*pVal* \[out\]  
保留中の印刷ジョブの数を受け取るメモリ位置への呼び出し元が指定のポインター。

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
<td><strong>S_OK</strong></td>
<td><p>操作に成功しました。</p></td>
</tr>
<tr class="even">
<td><strong>E_HANDLE</strong></td>
<td><p><a href="iasphelp-open.md" data-raw-source="[&lt;strong&gt;Iasphelp::Open&lt;/strong&gt;](iasphelp-open.md)"> <strong>Iasphelp::Open</strong> </a>メソッドが呼び出されていません。</p></td>
</tr>
<tr class="odd">
<td><strong>E_OUTOFMEMORY</strong></td>
<td><p>メモリ不足。</p></td>
</tr>
</tbody>
</table>

## <a name="vbscript-example"></a>VBScript の例

このプロパティのクエリを実行する前に呼び出す、 [ **Iasphelp::CalcJobETA** ](iasphelp-calcjobeta.md)プロパティの値を初期化します。

```vb
Dim objPrinter
strPrinter = Session("MS_printer")
Set objPrinter = Server.CreateObject ("OlePrn.AspHelp")
objPrinter.Open strPrinter
objPrinter.CalcJobETA
PendingJobs = objPrinter.PendingJobCount
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
