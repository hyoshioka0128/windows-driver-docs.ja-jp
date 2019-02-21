---
title: Iasphelp CalcJobETA メソッド
description: CalcJobETA メソッドでは、印刷ジョブが完了する時間を計算する ASP Web ページを使用します。
MS-HAID:
- webfnc\_65577773-9d44-429e-a2fe-eb1a1475b7f6.xml
- print.iasphelp\_calcjobeta
MSHAttr:
- PreferredSiteName:MSDN
- PreferredLib:/library/windows/hardware
ms.assetid: cdf4d590-c236-4ed7-a071-fd0ddbb78590
keywords:
- 印刷デバイスの CalcJobETA メソッド
- CalcJobETA メソッド、印刷デバイス Iasphelp インターフェイス
- Iasphelp インターフェイス、印刷デバイス CalcJobETA メソッド
topic_type:
- apiref
api_name:
- Iasphelp.CalcJobETA
api_type:
- COM
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: de81d764a826b987923bbdb0c980725ec8f45d3c
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56559614"
---
# <a name="iasphelpcalcjobeta-method"></a>Iasphelp::CalcJobETA メソッド

**CalcJobETA**メソッドは、印刷ジョブが完了する時間を計算する ASP Web ページを使用できます。

<a name="syntax"></a>構文
------

```cpp
HRESULT CalcJobETA();
```

<a name="parameters"></a>パラメーター
----------

このメソッドにはパラメーターはありません。

<a name="return-value"></a>戻り値
------------

次の表では、このメソッドの戻り値を示します。

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
<td><p>メソッドが成功しました。</p></td>
</tr>
<tr class="even">
<td><strong>E_HANDLE</strong></td>
<td><p><strong>Iasphelp::Open</strong>メソッドが呼び出されていません。</p></td>
</tr>
<tr class="odd">
<td><strong>E_OUTOFMEMORY</strong></td>
<td><p>メモリ不足です。</p></td>
</tr>
</tbody>
</table>

 

## <a name="vbscript-example"></a>VBScript の例

**CalcJobETA**メソッドは、その後 Iasphelp プロパティを使用して取得できる印刷ジョブの情報を計算します。 呼び出す**CalcJobETA**次のプロパティのいずれかを取得する前に。

[**Iasphelp::JobCompletionMinute**](iasphelp-jobcompletionminute.md)

[**Iasphelp::PendingJobCount**](iasphelp-pendingjobcount.md)

[**Iasphelp::AvgJobSize**](iasphelp-avgjobsize.md)

[**Iasphelp::AvgJobSizeUnit**](iasphelp-avgjobsizeunit.md)

前に**CalcJobETA**が呼び出されると、これらのプロパティのいずれかの値が 0 です。 場合**CalcJobETA**決定するプリンターの速度が現在のプリンターで使用できる、JobCompletionMinute 後続の呼び出しは、-1 の値を取得します。

[ **Iasphelp::Open** ](iasphelp-open.md)メソッドは、前に呼び出す必要があります、 **CalcJobETA**メソッドを呼び出すことができます。

```vb
Dim objPrinter
strPrinter = Session("MS_printer")
Set objPrinter = Server.CreateObject ("OlePrn.AspHelp")
objPrinter.Open strPrinter
objPrinter.CalcJobETA
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

[**Iasphelp::JobCompletionMinute**](iasphelp-jobcompletionminute.md)

[**Iasphelp::PendingJobCount**](iasphelp-pendingjobcount.md)

[**Iasphelp::AvgJobSize**](iasphelp-avgjobsize.md)

[**Iasphelp::AvgJobSizeUnit**](iasphelp-avgjobsizeunit.md)

[**Iasphelp::Open**](iasphelp-open.md)
