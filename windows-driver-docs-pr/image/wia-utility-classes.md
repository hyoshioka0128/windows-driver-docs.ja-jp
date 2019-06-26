---
title: WIA ユーティリティ クラス
ms.assetid: cc20a088-6470-4648-b7d9-999dbd74baf1
description: ''
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: fe433e5f5a2d40a1379dd2b0b110491c40b49371
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67387337"
---
# <a name="wia-utility-classes"></a>WIA ユーティリティ クラス


このトピックでは、WIA ユーティリティ ライブラリの一部である 3 つのヘルパー クラスをについて説明します。

-   [CWiauDbgFn クラス](#cwiaudbgfn-class)
-   [CWiauFormatConverter クラス](#cwiauformatconverter-class)
-   [CWiauPropertyList クラス](#cwiaupropertylist-class)

## <a name="cwiaudbgfn-class"></a>CWiauDbgFn Class


[CWiauDbgFn クラス](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff540345(v=vs.85))関数またはメソッドの開始/終了用のヘルパー クラスがトレースをポイントします。

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
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wiautil/nf-wiautil-cwiaudbgfn-cwiaudbgfn" data-raw-source="[&lt;strong&gt;CWiauDbgFn::CWiauDbgFn&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wiautil/nf-wiautil-cwiaudbgfn-cwiaudbgfn)"><strong>CWiauDbgFn::CWiauDbgFn</strong></a></p></td>
<td><p>クラスのコンス トラクターです。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wiautil/nf-wiautil-cwiaudbgfn-~cwiaudbgfn" data-raw-source="[&lt;strong&gt;CWiauDbgFn::~CWiauDbgFn&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wiautil/nf-wiautil-cwiaudbgfn-~cwiaudbgfn)"><strong>CWiauDbgFn::~CWiauDbgFn</strong></a></p></td>
<td><p>クラスのデストラクターです。</p></td>
</tr>
</tbody>
</table>

 

## <a name="cwiauformatconverter-class"></a>CWiauFormatConverter クラス


[CWiauFormatConverter クラス](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff540363(v=vs.85))はイメージが BMP 形式に変換するためのヘルパー クラスです。

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
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wiautil/nf-wiautil-cwiauformatconverter-cwiauformatconverter" data-raw-source="[&lt;strong&gt;CWiauFormatConverter::CWiauFormatConverter&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wiautil/nf-wiautil-cwiauformatconverter-cwiauformatconverter)"><strong>CWiauFormatConverter::CWiauFormatConverter</strong></a></p></td>
<td><p>クラスのコンス トラクターです。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wiautil/nf-wiautil-cwiauformatconverter-~cwiauformatconverter" data-raw-source="[&lt;strong&gt;CWiauFormatConverter::~CWiauFormatConverter&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wiautil/nf-wiautil-cwiauformatconverter-~cwiauformatconverter)"><strong>CWiauFormatConverter::~CWiauFormatConverter</strong></a></p></td>
<td><p>クラスのデストラクターです。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wiautil/nf-wiautil-cwiauformatconverter-converttobmp" data-raw-source="[&lt;strong&gt;CWiauFormatConverter::ConvertToBmp&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wiautil/nf-wiautil-cwiauformatconverter-converttobmp)"><strong>CWiauFormatConverter::ConvertToBmp</strong></a></p></td>
<td><p>イメージを BMP 形式に変換します。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wiautil/nf-wiautil-cwiauformatconverter-init" data-raw-source="[&lt;strong&gt;CWiauFormatConverter::Init&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wiautil/nf-wiautil-cwiauformatconverter-init)"><strong>CWiauFormatConverter::Init</strong></a></p></td>
<td><p>イメージを変換するためのクラスと GDI + を初期化します。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wiautil/nf-wiautil-cwiauformatconverter-isformatsupported" data-raw-source="[&lt;strong&gt;CWiauFormatConverter::IsFormatSupported&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wiautil/nf-wiautil-cwiauformatconverter-isformatsupported)"><strong>CWiauFormatConverter::IsFormatSupported</strong></a></p></td>
<td><p>GDI + をサポートしているイメージの形式に変換することを確認します。</p></td>
</tr>
</tbody>
</table>

 

## <a name="cwiaupropertylist-class"></a>CWiauPropertyList クラス


[CWiauPropertyList クラス](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff540386(v=vs.85))を定義して、WIA プロパティ リストの初期化のヘルパー クラスです。

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
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wiautil/nf-wiautil-cwiaupropertylist-cwiaupropertylist" data-raw-source="[&lt;strong&gt;CWiauPropertyList::CWiauPropertyList&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wiautil/nf-wiautil-cwiaupropertylist-cwiaupropertylist)"><strong>CWiauPropertyList::CWiauPropertyList</strong></a></p></td>
<td><p>クラスのコンス トラクターです。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wiautil/nf-wiautil-cwiaupropertylist-~cwiaupropertylist" data-raw-source="[&lt;strong&gt;CWiauPropertyList::~CWiauPropertyList&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wiautil/nf-wiautil-cwiaupropertylist-~cwiaupropertylist)"><strong>CWiauPropertyList:: ~ CWiauPropertyList</strong></a></p></td>
<td><p>クラスのデストラクターです。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wiautil/nf-wiautil-cwiaupropertylist-defineproperty" data-raw-source="[&lt;strong&gt;CWiauPropertyList::DefineProperty&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wiautil/nf-wiautil-cwiaupropertylist-defineproperty)"><strong>CWiauPropertyList::DefineProperty</strong></a></p></td>
<td><p>プロパティ リストのオブジェクトにプロパティの定義を追加します。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wiautil/nf-wiautil-cwiaupropertylist-getpropid" data-raw-source="[&lt;strong&gt;CWiauPropertyList::GetPropId&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wiautil/nf-wiautil-cwiaupropertylist-getpropid)"><strong>CWiauPropertyList::GetPropId</strong></a></p></td>
<td><p>指定したインデックス位置にあるプロパティのプロパティの識別子 (ID) を取得します。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wiautil/nf-wiautil-cwiaupropertylist-init" data-raw-source="[&lt;strong&gt;CWiauPropertyList::Init&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wiautil/nf-wiautil-cwiaupropertylist-init)"><strong>CWiauPropertyList::Init</strong></a></p></td>
<td><p>プロパティ リストのオブジェクトを初期化します。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wiautil/nf-wiautil-cwiaupropertylist-lookuppropid" data-raw-source="[&lt;strong&gt;CWiauPropertyList::LookupPropId&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wiautil/nf-wiautil-cwiaupropertylist-lookuppropid)"><strong>CWiauPropertyList::LookupPropId</strong></a></p></td>
<td><p>指定したプロパティ ID を持つプロパティのプロパティのインデックスを取得します。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wiautil/nf-wiautil-cwiaupropertylist-sendtowia" data-raw-source="[&lt;strong&gt;CWiauPropertyList::SendToWia&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wiautil/nf-wiautil-cwiaupropertylist-sendtowia)"><strong>CWiauPropertyList::SendToWia</strong></a></p></td>
<td><p>プロパティ リスト オブジェクト内に現在含まれているすべてのプロパティを定義する WIA サービスを呼び出します。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wiautil/nf-wiautil-cwiaupropertylist-setaccesssubtype(int_ulong_ulong)" data-raw-source="[&lt;strong&gt;CWiauPropertyList::SetAccessSubType&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wiautil/nf-wiautil-cwiaupropertylist-setaccesssubtype(int_ulong_ulong))"><strong>CWiauPropertyList::SetAccessSubType</strong></a></p></td>
<td><p>アクセスと、プロパティのサブタイプをリセットします。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff540412(v=vs.85)" data-raw-source="[&lt;strong&gt;CWiauPropertyList::SetCurrentValue(BYTE*)&lt;/strong&gt;](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff540412(v=vs.85))"><strong>CWiauPropertyList::SetCurrentValue(BYTE*)</strong></a></p></td>
<td><p>型があるプロパティの値を設定<strong>バイト</strong>配列。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff540410(v=vs.85)" data-raw-source="[&lt;strong&gt;CWiauPropertyList::SetCurrentValue(BSTR)&lt;/strong&gt;](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff540410(v=vs.85))"><strong>CWiauPropertyList::SetCurrentValue(BSTR)</strong></a></p></td>
<td><p>型がプロパティの値を設定<strong>BSTR</strong>します。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff540416(v=vs.85)" data-raw-source="[&lt;strong&gt;CWiauPropertyList::SetCurrentValue(CLSID)&lt;/strong&gt;](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff540416(v=vs.85))"><strong>CWiauPropertyList::SetCurrentValue(CLSID)</strong></a></p></td>
<td><p>型がプロパティの値を設定<strong>CLSID</strong>します。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff540423(v=vs.85)" data-raw-source="[&lt;strong&gt;CWiauPropertyList::SetCurrentValue(FLOAT)&lt;/strong&gt;](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff540423(v=vs.85))"><strong>CWiauPropertyList::SetCurrentValue(FLOAT)</strong></a></p></td>
<td><p>型がプロパティの値を設定<strong>FLOAT</strong>します。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff540427(v=vs.85)" data-raw-source="[&lt;strong&gt;CWiauPropertyList::SetCurrentValue(LONG)&lt;/strong&gt;](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff540427(v=vs.85))"><strong>CWiauPropertyList::SetCurrentValue(LONG)</strong></a></p></td>
<td><p>型がプロパティの値を設定<strong>長い</strong>します。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff540430(v=vs.85)" data-raw-source="[&lt;strong&gt;CWiauPropertyList::SetCurrentValue(SYSTEMTIME)&lt;/strong&gt;](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff540430(v=vs.85))"><strong>CWiauPropertyList::SetCurrentValue(SYSTEMTIME)</strong></a></p></td>
<td><p>型がプロパティの値を設定<strong>SYSTEMTIME</strong> (Microsoft Windows SDK のドキュメントで説明)。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff540436(v=vs.85)" data-raw-source="[&lt;strong&gt;CWiauPropertyList::SetValidValues(BSTR, list)&lt;/strong&gt;](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff540436(v=vs.85))"><strong>CWiauPropertyList::SetValidValues (BSTR、リスト)</strong></a></p></td>
<td><p>型と、既定値の一覧の最新かつ有効な値を設定<strong>BSTR</strong>値。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff540439(v=vs.85)" data-raw-source="[&lt;strong&gt;CWiauPropertyList::SetValidValues(CLSID, list)&lt;/strong&gt;](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff540439(v=vs.85))"><strong>CWiauPropertyList::SetValidValues (CLSID、リスト)</strong></a></p></td>
<td><p>型と、既定値の一覧の最新かつ有効な値を設定<strong>CLSID</strong>値。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff540447(v=vs.85)" data-raw-source="[&lt;strong&gt;CWiauPropertyList::SetValidValues(flag)&lt;/strong&gt;](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff540447(v=vs.85))"><strong>CWiauPropertyList::SetValidValues(flag)</strong></a></p></td>
<td><p>型だけでなく、既定値は、フラグの設定によって決定されるプロパティの現在、および有効な値を設定します。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff540452(v=vs.85)" data-raw-source="[&lt;strong&gt;CWiauPropertyList::SetValidValues(FLOAT, list)&lt;/strong&gt;](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff540452(v=vs.85))"><strong>CWiauPropertyList::SetValidValues (FLOAT, リスト)</strong></a></p></td>
<td><p>型と、既定値の一覧の最新かつ有効な値を設定<strong>FLOAT</strong>値。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff540461(v=vs.85)" data-raw-source="[&lt;strong&gt;CWiauPropertyList::SetValidValues(FLOAT, range)&lt;/strong&gt;](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff540461(v=vs.85))"><strong>CWiauPropertyList::SetValidValues (FLOAT、範囲)</strong></a></p></td>
<td><p>型と、既定値の範囲の現在、および有効な値を設定<strong>FLOAT</strong>値。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff540462(v=vs.85)" data-raw-source="[&lt;strong&gt;CWiauPropertyList::SetValidValues(LONG, list)&lt;/strong&gt;](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff540462(v=vs.85))"><strong>CWiauPropertyList::SetValidValues (LONG, リスト)</strong></a></p></td>
<td><p>型と、既定値の一覧の最新かつ有効な値を設定<strong>長い</strong>値。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff540468(v=vs.85)" data-raw-source="[&lt;strong&gt;CWiauPropertyList::SetValidValues(LONG, range)&lt;/strong&gt;](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff540468(v=vs.85))"><strong>CWiauPropertyList::SetValidValues (LONG、範囲)</strong></a></p></td>
<td><p>型と、既定値の範囲の現在、および有効な値を設定<strong>長い</strong>値。</p></td>
</tr>
</tbody>
</table>

 

 

 




