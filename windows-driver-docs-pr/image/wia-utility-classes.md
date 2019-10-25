---
title: WIA ユーティリティ クラス
ms.assetid: cc20a088-6470-4648-b7d9-999dbd74baf1
description: ''
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: feacee820d973a043176b1a3f4749a89aeed471c
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72840662"
---
# <a name="wia-utility-classes"></a>WIA ユーティリティ クラス


このトピックでは、WIA ユーティリティライブラリの一部である3つのヘルパークラスについて説明します。

-   [Cwi/Dbgfn クラス](#cwiaudbgfn-class)
-   [Cwi/Formatconverter クラス](#cwiauformatconverter-class)
-   [Cwi/Propertylist クラス](#cwiaupropertylist-class)

## <a name="cwiaudbgfn-class"></a>Cwi/Dbgfn クラス


[Cwiaudbgfn クラス](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff540345(v=vs.85))は、関数またはメソッドのエントリ/終了ポイントのトレース用のヘルパークラスです。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>メソッド</th>
<th>説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wiautil/nf-wiautil-cwiaudbgfn-cwiaudbgfn" data-raw-source="[&lt;strong&gt;CWiauDbgFn::CWiauDbgFn&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wiautil/nf-wiautil-cwiaudbgfn-cwiaudbgfn)"><strong>Cwi/Dbgfn:: Cwi/Dbgfn</strong></a></p></td>
<td><p>クラスコンストラクター。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wiautil/nf-wiautil-cwiaudbgfn-~cwiaudbgfn" data-raw-source="[&lt;strong&gt;CWiauDbgFn::~CWiauDbgFn&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wiautil/nf-wiautil-cwiaudbgfn-~cwiaudbgfn)"><strong>Cwi/Dbgfn:: ~ Cwi/Dbgfn</strong></a></p></td>
<td><p>クラスデストラクター。</p></td>
</tr>
</tbody>
</table>

 

## <a name="cwiauformatconverter-class"></a>Cwi/Formatconverter クラス


[Cwi/Formatconverter クラス](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff540363(v=vs.85))は、イメージを BMP 形式に変換するためのヘルパークラスです。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>メソッド</th>
<th>説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wiautil/nf-wiautil-cwiauformatconverter-cwiauformatconverter" data-raw-source="[&lt;strong&gt;CWiauFormatConverter::CWiauFormatConverter&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wiautil/nf-wiautil-cwiauformatconverter-cwiauformatconverter)"><strong>Cwi/Formatconverter:: Cwi/Formatconverter</strong></a></p></td>
<td><p>クラスコンストラクター。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wiautil/nf-wiautil-cwiauformatconverter-~cwiauformatconverter" data-raw-source="[&lt;strong&gt;CWiauFormatConverter::~CWiauFormatConverter&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wiautil/nf-wiautil-cwiauformatconverter-~cwiauformatconverter)"><strong>Cwi/Formatconverter:: ~ Cwi/Formatconverter</strong></a></p></td>
<td><p>クラスデストラクター。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wiautil/nf-wiautil-cwiauformatconverter-converttobmp" data-raw-source="[&lt;strong&gt;CWiauFormatConverter::ConvertToBmp&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wiautil/nf-wiautil-cwiauformatconverter-converttobmp)"><strong>Cwi/Formatconverter:: ConvertToBmp</strong></a></p></td>
<td><p>イメージを BMP 形式に変換します。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wiautil/nf-wiautil-cwiauformatconverter-init" data-raw-source="[&lt;strong&gt;CWiauFormatConverter::Init&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wiautil/nf-wiautil-cwiauformatconverter-init)"><strong>Cwi/Formatconverter:: Init</strong></a></p></td>
<td><p>イメージを変換するために、クラスと GDI + を初期化します。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wiautil/nf-wiautil-cwiauformatconverter-isformatsupported" data-raw-source="[&lt;strong&gt;CWiauFormatConverter::IsFormatSupported&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wiautil/nf-wiautil-cwiauformatconverter-isformatsupported)"><strong>Cwi/Formatconverter:: IsFormatSupported</strong></a></p></td>
<td><p>GDI + が変換対象のイメージ形式をサポートしていることを確認します。</p></td>
</tr>
</tbody>
</table>

 

## <a name="cwiaupropertylist-class"></a>Cwi/Propertylist クラス


[Cwi/Propertylist クラス](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff540386(v=vs.85))は、WIA プロパティリストを定義および初期化するためのヘルパークラスです。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>メソッド</th>
<th>説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wiautil/nf-wiautil-cwiaupropertylist-cwiaupropertylist" data-raw-source="[&lt;strong&gt;CWiauPropertyList::CWiauPropertyList&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wiautil/nf-wiautil-cwiaupropertylist-cwiaupropertylist)"><strong>Cwi/Propertylist:: Cwi/Propertylist</strong></a></p></td>
<td><p>クラスコンストラクター。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wiautil/nf-wiautil-cwiaupropertylist-~cwiaupropertylist" data-raw-source="[&lt;strong&gt;CWiauPropertyList::~CWiauPropertyList&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wiautil/nf-wiautil-cwiaupropertylist-~cwiaupropertylist)"><strong>Cwi/Propertylist:: ~ Cwi/Propertylist</strong></a></p></td>
<td><p>クラスデストラクター。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wiautil/nf-wiautil-cwiaupropertylist-defineproperty" data-raw-source="[&lt;strong&gt;CWiauPropertyList::DefineProperty&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wiautil/nf-wiautil-cwiaupropertylist-defineproperty)"><strong>CWiauPropertyList::D efineProperty</strong></a></p></td>
<td><p>プロパティリストオブジェクトにプロパティ定義を追加します。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wiautil/nf-wiautil-cwiaupropertylist-getpropid" data-raw-source="[&lt;strong&gt;CWiauPropertyList::GetPropId&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wiautil/nf-wiautil-cwiaupropertylist-getpropid)"><strong>Cwi/Propertylist:: GetPropId</strong></a></p></td>
<td><p>指定したインデックス位置にあるプロパティのプロパティ識別子 (ID) を取得します。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wiautil/nf-wiautil-cwiaupropertylist-init" data-raw-source="[&lt;strong&gt;CWiauPropertyList::Init&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wiautil/nf-wiautil-cwiaupropertylist-init)"><strong>Cwi/Propertylist:: Init</strong></a></p></td>
<td><p>プロパティリストオブジェクトを初期化します。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wiautil/nf-wiautil-cwiaupropertylist-lookuppropid" data-raw-source="[&lt;strong&gt;CWiauPropertyList::LookupPropId&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wiautil/nf-wiautil-cwiaupropertylist-lookuppropid)"><strong>Cwi/Propertylist:: LookupPropId</strong></a></p></td>
<td><p>指定したプロパティ ID を持つプロパティのプロパティインデックスを取得します。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wiautil/nf-wiautil-cwiaupropertylist-sendtowia" data-raw-source="[&lt;strong&gt;CWiauPropertyList::SendToWia&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wiautil/nf-wiautil-cwiaupropertylist-sendtowia)"><strong>Cwi/Propertylist:: SendToWia</strong></a></p></td>
<td><p>WIA サービスを呼び出して、プロパティリストオブジェクトに現在格納されているすべてのプロパティを定義します。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wiautil/nf-wiautil-cwiaupropertylist-setaccesssubtype(int_ulong_ulong)" data-raw-source="[&lt;strong&gt;CWiauPropertyList::SetAccessSubType&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wiautil/nf-wiautil-cwiaupropertylist-setaccesssubtype(int_ulong_ulong))"><strong>Cwi/Propertylist:: SetAccessSubType</strong></a></p></td>
<td><p>プロパティのアクセスおよびサブタイプをリセットします。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff540412(v=vs.85)" data-raw-source="[&lt;strong&gt;CWiauPropertyList::SetCurrentValue(BYTE*)&lt;/strong&gt;](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff540412(v=vs.85))"><strong>Cwisystem.windows.dependencyobject.setcurrentvalue Propertylist:: (BYTE *)</strong></a></p></td>
<td><p>型が<strong>バイト</strong>配列であるプロパティの値を設定します。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff540410(v=vs.85)" data-raw-source="[&lt;strong&gt;CWiauPropertyList::SetCurrentValue(BSTR)&lt;/strong&gt;](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff540410(v=vs.85))"><strong>Cwisystem.windows.dependencyobject.setcurrentvalue Propertylist:: (BSTR)</strong></a></p></td>
<td><p>型が<strong>BSTR</strong>であるプロパティの値を設定します。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff540416(v=vs.85)" data-raw-source="[&lt;strong&gt;CWiauPropertyList::SetCurrentValue(CLSID)&lt;/strong&gt;](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff540416(v=vs.85))"><strong>Cwisystem.windows.dependencyobject.setcurrentvalue Propertylist:: (CLSID)</strong></a></p></td>
<td><p>型が<strong>CLSID</strong>であるプロパティの値を設定します。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff540423(v=vs.85)" data-raw-source="[&lt;strong&gt;CWiauPropertyList::SetCurrentValue(FLOAT)&lt;/strong&gt;](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff540423(v=vs.85))"><strong>Cwisystem.windows.dependencyobject.setcurrentvalue Propertylist:: (FLOAT)</strong></a></p></td>
<td><p>型が<strong>FLOAT</strong>であるプロパティの値を設定します。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff540427(v=vs.85)" data-raw-source="[&lt;strong&gt;CWiauPropertyList::SetCurrentValue(LONG)&lt;/strong&gt;](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff540427(v=vs.85))"><strong>Cwisystem.windows.dependencyobject.setcurrentvalue Propertylist:: (LONG)</strong></a></p></td>
<td><p>型が<strong>LONG</strong>であるプロパティの値を設定します。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff540430(v=vs.85)" data-raw-source="[&lt;strong&gt;CWiauPropertyList::SetCurrentValue(SYSTEMTIME)&lt;/strong&gt;](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff540430(v=vs.85))"><strong>Cwisystem.windows.dependencyobject.setcurrentvalue Propertylist:: (SYSTEMTIME)</strong></a></p></td>
<td><p>種類が<strong>SYSTEMTIME</strong>であるプロパティの値を設定します (Microsoft Windows SDK のドキュメントを参照)。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff540436(v=vs.85)" data-raw-source="[&lt;strong&gt;CWiauPropertyList::SetValidValues(BSTR, list)&lt;/strong&gt;](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff540436(v=vs.85))"><strong>Cwi/Propertylist:: SetValidValues (BSTR、list)</strong></a></p></td>
<td><p>型と、 <strong>BSTR</strong>値のリストの既定値、現在の値、および有効な値を設定します。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff540439(v=vs.85)" data-raw-source="[&lt;strong&gt;CWiauPropertyList::SetValidValues(CLSID, list)&lt;/strong&gt;](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff540439(v=vs.85))"><strong>Cwi/Propertylist:: SetValidValues (CLSID, list)</strong></a></p></td>
<td><p><strong>CLSID</strong>値の一覧の既定値、現在の値、および有効な値を設定します。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff540447(v=vs.85)" data-raw-source="[&lt;strong&gt;CWiauPropertyList::SetValidValues(flag)&lt;/strong&gt;](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff540447(v=vs.85))"><strong>Cwi/Propertylist:: SetValidValues (フラグ)</strong></a></p></td>
<td><p>フラグの設定によって値が決定されるプロパティの、型、および既定値、現在の値、および有効な値を設定します。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff540452(v=vs.85)" data-raw-source="[&lt;strong&gt;CWiauPropertyList::SetValidValues(FLOAT, list)&lt;/strong&gt;](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff540452(v=vs.85))"><strong>Cwi/Propertylist:: SetValidValues (FLOAT、list)</strong></a></p></td>
<td><p><strong>FLOAT</strong>値のリストの既定値、現在の値、および有効値を設定します。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff540461(v=vs.85)" data-raw-source="[&lt;strong&gt;CWiauPropertyList::SetValidValues(FLOAT, range)&lt;/strong&gt;](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff540461(v=vs.85))"><strong>Cwi/Propertylist:: SetValidValues (FLOAT, range)</strong></a></p></td>
<td><p>型と、 <strong>FLOAT</strong>値の範囲の既定値、現在の値、および有効値を設定します。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff540462(v=vs.85)" data-raw-source="[&lt;strong&gt;CWiauPropertyList::SetValidValues(LONG, list)&lt;/strong&gt;](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff540462(v=vs.85))"><strong>Cwi/Propertylist:: SetValidValues (LONG、list)</strong></a></p></td>
<td><p>型、および<strong>LONG</strong>型の値のリストの既定値、現在の値、および有効な値を設定します。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff540468(v=vs.85)" data-raw-source="[&lt;strong&gt;CWiauPropertyList::SetValidValues(LONG, range)&lt;/strong&gt;](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff540468(v=vs.85))"><strong>Cwi/Propertylist:: SetValidValues (LONG, range)</strong></a></p></td>
<td><p>型と、 <strong>LONG</strong>値の範囲の既定値、現在の値、有効な値を設定します。</p></td>
</tr>
</tbody>
</table>

 

 

 




