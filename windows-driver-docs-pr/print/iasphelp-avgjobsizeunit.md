---
title: Iasphelp get\_AvgJobSizeUnit メソッド
description: AvgJobSizeUnit プロパティは、ジョブの平均サイズの単位を決定する ASP Web ページを使用できます。
MS-HAID:
- webfnc\_b7542526-ad13-46d7-a1c1-e02d7832dfb6.xml
- print.iasphelp\_avgjobsizeunit
MSHAttr:
- PreferredSiteName:MSDN
- PreferredLib:/library/windows/hardware
ms.assetid: f5a701ff-270f-45f5-8c6e-ecf1b8afab20
keywords:
- 印刷デバイスの get_AvgJobSizeUnit メソッド
- get_AvgJobSizeUnit メソッド、印刷デバイス Iasphelp インターフェイス
- Iasphelp インターフェイス、印刷デバイス get_AvgJobSizeUnit メソッド
topic_type:
- apiref
api_name:
- Iasphelp.get_AvgJobSizeUnit
api_type:
- COM
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 63320ba94707ed0990adf15b59af555a901ab844
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56558294"
---
# <a name="iasphelpgetavgjobsizeunit-method"></a>Iasphelp::get\_AvgJobSizeUnit メソッド


**AvgJobSizeUnit**プロパティは、ジョブの平均サイズの単位を決定する ASP Web ページを使用できます。

<a name="syntax"></a>構文
------

```cpp
HRESULT get_AvgJobSizeUnit(
  [out] long *pVal
);
```

<a name="parameters"></a>パラメーター
----------

*pVal* \[out\]  
次の表に、値のいずれかを受信するメモリ位置への呼び出し元が指定のポインター。 値は、ジョブの平均サイズに関連付けられているユニットを示します。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>Value</th>
<th>意味</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>1</p></td>
<td><p>ジョブの平均サイズの単位は、ジョブごとのページには。</p></td>
</tr>
<tr class="even">
<td><p>2</p></td>
<td><p>ジョブの平均サイズの単位は、ジョブあたりのバイト数でです。</p></td>
</tr>
</tbody>
</table>

 

<a name="return-value"></a>戻り値
------------

このメソッドは、秒を返します。\_成功した場合には、[ok] です。

## <a name="vbscript-example"></a>VBScript の例

クエリ、 **Iasphelp::AvgJobSizeUnit**の単位を決定するプロパティ、 [ **Iasphelp::AvgJobSize** ](iasphelp-avgjobsize.md)プロパティの値が表されます。

このプロパティのクエリを実行する前に呼び出す、 [ **Iasphelp::CalcJobETA** ](iasphelp-calcjobeta.md)プロパティの値を初期化します。

```vb
Dim objPrinter, strPrinter, JobUnits
strPrinter = Session("MS_printer")
Set objPrinter = Server.CreateObject ("OlePrn.AspHelp")
objPrinter.Open strPrinter
objPrinter.CalcJobETA
JobUnits = objPrinter.AvgJobSizeUnit
' If JobUnits = 1 then job size is in units of pages
' If JobUnits = 2 then job size is in units of bytes
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

[**Iasphelp::AvgJobSize**](iasphelp-avgjobsize.md)

[**Iasphelp::CalcJobETA**](iasphelp-calcjobeta.md)
