---
ms.assetid: EB2264A4-BAE8-446B-B9A5-19893936DDCA
title: ドライバー リファレンス ページでのターゲット プラットフォーム
description: Microsoft ドライバー リファレンス ページの下部にある要件ブロックには、ターゲット プラットフォームという名前のエントリが表示されます。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9bf53562619c2fff7f444a36373553cc7f5b6b70
ms.sourcegitcommit: 5598b4c767ab56461b976b49fd75e4e5fb6018d2
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2020
ms.locfileid: "63344037"
---
# <a name="target-platform-on-driver-reference-pages"></a>ドライバー リファレンス ページでのターゲット プラットフォーム

Microsoft ドライバー リファレンス ページの下部にある要件ブロックには、**ターゲット プラットフォーム**という名前のエントリが表示されます。 次の行は、ページが適用される Windows のエディションの一覧です。

次に示すのは、このようなエントリの例です。

![要件ブロックでターゲット プラットフォームがユニバーサルに設定されている](images/TargetPlatform.png)

**[ターゲット プラットフォーム]** に指定された値は、Visual Studio の **[構成プロパティ] &gt; [Driver Settings (ドライバーの設定)] &gt; [全般]** の下にある **[ターゲット プラットフォーム]** プロパティで使用できる値にマップされます。

**ターゲット プラットフォーム**に対して表示される値とその意味を、次に説明します。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">用語</th>
<th align="left">説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><span id="Universal"></span><span id="universal"></span><span id="UNIVERSAL"></span>ユニバーサル</p></td>
<td align="left"><p>ユニバーサル Windows ドライバーのドライバー バイナリは、このデバイス ドライバー インターフェイス (DDI) を呼び出すことができます。</p>
<p>ユニバーサル Windows ドライバーは、次に示す Windows 10 のユニバーサル Windows プラットフォーム (UWP) ベース エディションで動作します。</p>
<ul>
<li>Windows 10 デスクトップ エディション (Home、Pro、Enterprise)</li>
<li>S モードの Windows 10</li>
<li>Windows 10 Mobile</li>
<li>Windows 10 IoT Core</li>
<li>Windows Server 2016</li>
</ul>
<p>詳しくは、「<a href="getting-started-with-universal-drivers.md" data-raw-source="[Getting Started with Universal Windows drivers](getting-started-with-universal-drivers.md)">ユニバーサル Windows ドライバーの概要</a>」をご覧ください。</p></td>
</tr>
<tr class="even">
<td align="left"><p><span id="Desktop"></span><span id="desktop"></span><span id="DESKTOP"></span>デスクトップ</p></td>
<td align="left"><p>Windows 10 デスクトップ エディションまたは Windows Server 2016 のドライバー バイナリは、この DDI を呼び出すことができます。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><span id="Mobile"></span><span id="mobile"></span><span id="MOBILE"></span>モバイル</p></td>
<td align="left"><p>Windows 10 Mobile のドライバー バイナリは、この DDI を呼び出すことができます。</p></td>
</tr>
</tbody>
</table>

 

 

 





