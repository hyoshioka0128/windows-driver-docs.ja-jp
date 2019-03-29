---
title: WIA ユーティリティ クラス
ms.assetid: cc20a088-6470-4648-b7d9-999dbd74baf1
description: ''
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: e731bc730aa1a770a1dd3868fe47e2348196e91b
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56570486"
---
# <a name="wia-utility-classes"></a>WIA ユーティリティ クラス


このトピックでは、WIA ユーティリティ ライブラリの一部である 3 つのヘルパー クラスをについて説明します。

-   [CWiauDbgFn クラス](#cwiaudbgfn-class)
-   [CWiauFormatConverter クラス](#cwiauformatconverter-class)
-   [CWiauPropertyList クラス](#cwiaupropertylist-class)

## <a name="cwiaudbgfn-class"></a>CWiauDbgFn Class


[CWiauDbgFn クラス](https://msdn.microsoft.com/library/windows/hardware/ff540345)関数またはメソッドの開始/終了用のヘルパー クラスがトレースをポイントします。

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
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff540348" data-raw-source="[&lt;strong&gt;CWiauDbgFn::CWiauDbgFn&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff540348)"><strong>CWiauDbgFn::CWiauDbgFn</strong></a></p></td>
<td><p>クラスのコンス トラクターです。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff540356" data-raw-source="[&lt;strong&gt;CWiauDbgFn::~CWiauDbgFn&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff540356)"><strong>CWiauDbgFn::~CWiauDbgFn</strong></a></p></td>
<td><p>クラスのデストラクターです。</p></td>
</tr>
</tbody>
</table>

 

## <a name="cwiauformatconverter-class"></a>CWiauFormatConverter クラス


[CWiauFormatConverter クラス](https://msdn.microsoft.com/library/windows/hardware/ff540363)はイメージが BMP 形式に変換するためのヘルパー クラスです。

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
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff540370" data-raw-source="[&lt;strong&gt;CWiauFormatConverter::CWiauFormatConverter&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff540370)"><strong>CWiauFormatConverter::CWiauFormatConverter</strong></a></p></td>
<td><p>クラスのコンス トラクターです。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff540385" data-raw-source="[&lt;strong&gt;CWiauFormatConverter::~CWiauFormatConverter&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff540385)"><strong>CWiauFormatConverter::~CWiauFormatConverter</strong></a></p></td>
<td><p>クラスのデストラクターです。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff540369" data-raw-source="[&lt;strong&gt;CWiauFormatConverter::ConvertToBmp&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff540369)"><strong>CWiauFormatConverter::ConvertToBmp</strong></a></p></td>
<td><p>イメージを BMP 形式に変換します。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff540374" data-raw-source="[&lt;strong&gt;CWiauFormatConverter::Init&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff540374)"><strong>CWiauFormatConverter::Init</strong></a></p></td>
<td><p>イメージを変換するためのクラスと GDI + を初期化します。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff540379" data-raw-source="[&lt;strong&gt;CWiauFormatConverter::IsFormatSupported&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff540379)"><strong>CWiauFormatConverter::IsFormatSupported</strong></a></p></td>
<td><p>GDI + をサポートしているイメージの形式に変換することを確認します。</p></td>
</tr>
</tbody>
</table>

 

## <a name="cwiaupropertylist-class"></a>CWiauPropertyList クラス


[CWiauPropertyList クラス](https://msdn.microsoft.com/library/windows/hardware/ff540386)を定義して、WIA プロパティ リストの初期化のヘルパー クラスです。

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
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff540389" data-raw-source="[&lt;strong&gt;CWiauPropertyList::CWiauPropertyList&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff540389)"><strong>CWiauPropertyList::CWiauPropertyList</strong></a></p></td>
<td><p>クラスのコンス トラクターです。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff540472" data-raw-source="[&lt;strong&gt;CWiauPropertyList::~CWiauPropertyList&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff540472)"><strong>CWiauPropertyList:: ~ CWiauPropertyList</strong></a></p></td>
<td><p>クラスのデストラクターです。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff540391" data-raw-source="[&lt;strong&gt;CWiauPropertyList::DefineProperty&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff540391)"><strong>CWiauPropertyList::DefineProperty</strong></a></p></td>
<td><p>プロパティ リストのオブジェクトにプロパティの定義を追加します。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff540392" data-raw-source="[&lt;strong&gt;CWiauPropertyList::GetPropId&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff540392)"><strong>CWiauPropertyList::GetPropId</strong></a></p></td>
<td><p>指定したインデックス位置にあるプロパティのプロパティの識別子 (ID) を取得します。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff540396" data-raw-source="[&lt;strong&gt;CWiauPropertyList::Init&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff540396)"><strong>CWiauPropertyList::Init</strong></a></p></td>
<td><p>プロパティ リストのオブジェクトを初期化します。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff540400" data-raw-source="[&lt;strong&gt;CWiauPropertyList::LookupPropId&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff540400)"><strong>CWiauPropertyList::LookupPropId</strong></a></p></td>
<td><p>指定したプロパティ ID を持つプロパティのプロパティのインデックスを取得します。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff540403" data-raw-source="[&lt;strong&gt;CWiauPropertyList::SendToWia&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff540403)"><strong>CWiauPropertyList::SendToWia</strong></a></p></td>
<td><p>プロパティ リスト オブジェクト内に現在含まれているすべてのプロパティを定義する WIA サービスを呼び出します。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff540407" data-raw-source="[&lt;strong&gt;CWiauPropertyList::SetAccessSubType&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff540407)"><strong>CWiauPropertyList::SetAccessSubType</strong></a></p></td>
<td><p>アクセスと、プロパティのサブタイプをリセットします。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff540412" data-raw-source="[&lt;strong&gt;CWiauPropertyList::SetCurrentValue(BYTE*)&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff540412)"><strong>CWiauPropertyList::SetCurrentValue(BYTE*)</strong></a></p></td>
<td><p>型があるプロパティの値を設定<strong>バイト</strong>配列。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff540410" data-raw-source="[&lt;strong&gt;CWiauPropertyList::SetCurrentValue(BSTR)&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff540410)"><strong>CWiauPropertyList::SetCurrentValue(BSTR)</strong></a></p></td>
<td><p>型がプロパティの値を設定<strong>BSTR</strong>します。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff540416" data-raw-source="[&lt;strong&gt;CWiauPropertyList::SetCurrentValue(CLSID)&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff540416)"><strong>CWiauPropertyList::SetCurrentValue(CLSID)</strong></a></p></td>
<td><p>型がプロパティの値を設定<strong>CLSID</strong>します。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff540423" data-raw-source="[&lt;strong&gt;CWiauPropertyList::SetCurrentValue(FLOAT)&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff540423)"><strong>CWiauPropertyList::SetCurrentValue(FLOAT)</strong></a></p></td>
<td><p>型がプロパティの値を設定<strong>FLOAT</strong>します。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff540427" data-raw-source="[&lt;strong&gt;CWiauPropertyList::SetCurrentValue(LONG)&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff540427)"><strong>CWiauPropertyList::SetCurrentValue(LONG)</strong></a></p></td>
<td><p>型がプロパティの値を設定<strong>長い</strong>します。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff540430" data-raw-source="[&lt;strong&gt;CWiauPropertyList::SetCurrentValue(SYSTEMTIME)&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff540430)"><strong>CWiauPropertyList::SetCurrentValue(SYSTEMTIME)</strong></a></p></td>
<td><p>型がプロパティの値を設定<strong>SYSTEMTIME</strong> (Microsoft Windows SDK のドキュメントで説明)。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff540436" data-raw-source="[&lt;strong&gt;CWiauPropertyList::SetValidValues(BSTR, list)&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff540436)"><strong>CWiauPropertyList::SetValidValues (BSTR、リスト)</strong></a></p></td>
<td><p>型と、既定値の一覧の最新かつ有効な値を設定<strong>BSTR</strong>値。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff540439" data-raw-source="[&lt;strong&gt;CWiauPropertyList::SetValidValues(CLSID, list)&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff540439)"><strong>CWiauPropertyList::SetValidValues (CLSID、リスト)</strong></a></p></td>
<td><p>型と、既定値の一覧の最新かつ有効な値を設定<strong>CLSID</strong>値。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff540447" data-raw-source="[&lt;strong&gt;CWiauPropertyList::SetValidValues(flag)&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff540447)"><strong>CWiauPropertyList::SetValidValues(flag)</strong></a></p></td>
<td><p>型だけでなく、既定値は、フラグの設定によって決定されるプロパティの現在、および有効な値を設定します。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff540452" data-raw-source="[&lt;strong&gt;CWiauPropertyList::SetValidValues(FLOAT, list)&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff540452)"><strong>CWiauPropertyList::SetValidValues (FLOAT, リスト)</strong></a></p></td>
<td><p>型と、既定値の一覧の最新かつ有効な値を設定<strong>FLOAT</strong>値。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff540461" data-raw-source="[&lt;strong&gt;CWiauPropertyList::SetValidValues(FLOAT, range)&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff540461)"><strong>CWiauPropertyList::SetValidValues (FLOAT、範囲)</strong></a></p></td>
<td><p>型と、既定値の範囲の現在、および有効な値を設定<strong>FLOAT</strong>値。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff540462" data-raw-source="[&lt;strong&gt;CWiauPropertyList::SetValidValues(LONG, list)&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff540462)"><strong>CWiauPropertyList::SetValidValues (LONG, リスト)</strong></a></p></td>
<td><p>型と、既定値の一覧の最新かつ有効な値を設定<strong>長い</strong>値。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff540468" data-raw-source="[&lt;strong&gt;CWiauPropertyList::SetValidValues(LONG, range)&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff540468)"><strong>CWiauPropertyList::SetValidValues (LONG、範囲)</strong></a></p></td>
<td><p>型と、既定値の範囲の現在、および有効な値を設定<strong>長い</strong>値。</p></td>
</tr>
</tbody>
</table>

 

 

 




