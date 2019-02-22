---
title: Iasphelp get\_AvgJobSize メソッド
description: AvgJobSize プロパティは、一連の印刷ジョブのジョブの平均サイズを決定する ASP Web ページを使用できます。
MS-HAID:
- webfnc\_de863905-eb8f-430a-a70b-7cb404dd3717.xml
- print.iasphelp\_avgjobsize
MSHAttr:
- PreferredSiteName:MSDN
- PreferredLib:/library/windows/hardware
ms.assetid: 3373376f-c904-47dd-8502-c2c26caed3be
keywords:
- 印刷デバイスの get_AvgJobSize メソッド
- get_AvgJobSize メソッド、印刷デバイス Iasphelp インターフェイス
- Iasphelp インターフェイス、印刷デバイス get_AvgJobSize メソッド
topic_type:
- apiref
api_name:
- Iasphelp.get_AvgJobSize
api_type:
- COM
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 47fac5c86d5b2602ef173eb9582ea8e9b4b73a69
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56558409"
---
# <a name="iasphelpgetavgjobsize-method"></a>Iasphelp::get\_AvgJobSize メソッド


**AvgJobSize**プロパティは、一連の印刷ジョブのジョブの平均サイズを決定する ASP Web ページを使用できます。

<a name="syntax"></a>構文
------

```cpp
HRESULT get_AvgJobSize(
  [out] long *pVal
);
```

<a name="parameters"></a>パラメーター
----------

*pVal* \[out\]  
ジョブの平均サイズを受け取るメモリ位置への呼び出し元が指定のポインター。 このパラメーターの詳細については、次の「解説」を参照してください。

<a name="return-value"></a>戻り値
------------

このメソッドは、秒を返します。\_成功した場合には、[ok] です。

## <a name="vbscript-example"></a>VBScript の例

ジョブの平均サイズは、ジョブごとのページ数またはジョブごとのバイト数として表現できます。 使用して、 [ **Iasphelp::AvgJobSizeUnit** ](iasphelp-avgjobsizeunit.md)する単位の対象を決定するプロパティ、 **Iasphelp::AvgJobSize**プロパティ。

このプロパティのクエリを実行する前に呼び出す、 [ **Iasphelp::CalcJobETA** ](iasphelp-calcjobeta.md)プロパティの値を初期化します。

```vb
Dim objPrinter, strPrinter, JobSizeAvg
strPrinter = Session("MS_printer")
Set objPrinter = Server.CreateObject ("OlePrn.AspHelp")
objPrinter.Open strPrinter
objPrinter.CalcJobETA
JobSizeAvg = objPrinter.AvgJobSize
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

[**Iasphelp::AvgJobSizeUnit**](iasphelp-avgjobsizeunit.md)

[**Iasphelp::CalcJobETA**](iasphelp-calcjobeta.md)
