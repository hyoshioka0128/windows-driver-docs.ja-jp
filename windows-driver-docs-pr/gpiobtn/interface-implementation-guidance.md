---
title: インターフェイスの実装のガイダンス
description: このセクションでは、インターフェイスの実装のガイダンスを提供します。
ms.assetid: E97A880F-0422-432C-8567-444CA6FD2980
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 37285e04fe0e09a4353a392b92e1fdff569774eb
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56529811"
---
# <a name="interface-implementation-guidance"></a>インターフェイスの実装のガイダンス


このセクションでは、インターフェイスの実装のガイダンスを提供します。

## <a name="span-idinthissectionspanin-this-section"></a><span id="in_this_section"></span>このセクションでは


<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">トピック</th>
<th align="left">説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><a href="available-interfaces-and-related-apis.md" data-raw-source="[Available interfaces and related APIs](available-interfaces-and-related-apis.md)">使用可能なインターフェイスと関連 Api</a></p></td>
<td align="left"><p>次の 3 つの GPIO インターフェイスがあります。 デバイスごとに 1 つ。 各インターフェイスは、GUID によって参照されます。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="indicator-implementation.md" data-raw-source="[Indicator implementation](indicator-implementation.md)">インジケーターの実装</a></p></td>
<td align="left"><p>このトピックでは、インジケーターの実装について説明します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="button-implementation.md" data-raw-source="[Button implementation](button-implementation.md)">ボタンの実装</a></p></td>
<td align="left"><p>ボタンと状態インジケーターの両方の物理 GPIO リソースを使用することをお勧めします。</p></td>
</tr>
</tbody>
</table>

 

## <a name="span-idsystemstatespanspan-idsystemstatespanspan-idsystemstatespansystem-state"></a><span id="System_state"></span><span id="system_state"></span><span id="SYSTEM_STATE"></span>システムの状態


負荷の受信トレイのドライバーでサポートされているすべてのボタンの既定の状態は、上の位置には。

インターフェイスを使用して最初の兆候は、ダウン状態に、(インデックス) を使用して、指定したボタンを切り替えます。

ラップトップ/スレート モードのインジケーターの既定の状態では、スレートです。

ドッキングのモードのインジケーターの既定の状態はドッキング解除時です。

インターフェイスを使用して最初の兆候は、その他の状態をインジケーターを切り替えます。

状態を照会するには次のように GetSystemMetric API を使用できます。

``` syntax
int WINAPI GetSystemMetrics(
  _In_  int nIndex
);
```

インジケーターの使用可能なパラメーター:

-   SM\_SYSTEMDOCKED ドッキング状態にします。 値はドッキングされていないモードのサイトおよび 0 以外それ以外の場合。
-   SM\_CONVERTIBLESLATEMODE スレート モードにします。 呼び出しを返します 0 スレート モードのサイトおよび 0 以外。

## <a name="span-idnotificationsspanspan-idnotificationsspanspan-idnotificationsspannotifications"></a><span id="Notifications"></span><span id="notifications"></span><span id="NOTIFICATIONS"></span>通知


ときにいずれかのシステム メトリック SM\_CONVERTIBLESLATEMODE または SM\_SYSTEMDOCKED 変更では、WM を使用してブロードキャスト メッセージがシステムによって送信された\_SETTINGCHANGE します。

WM の LPARAM\_SETTINGCHANGE メッセージには、どのシステムを示します。 メトリックが"ConvertibleSlateMode"または"SystemDockMode"のいずれかの文字列を使用して変更します。

 

 




