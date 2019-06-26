---
title: プリンター グラフィックス DLL をビルドする
description: プリンター グラフィックス DLL をビルドする
ms.assetid: bec1e9cc-a846-43e5-bc9e-e43a151ef6c4
keywords:
- プリンター グラフィックスの構築、DLL の WDK
- グラフィックスの DLL の WDK プリンター、ビルド
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2f413bb9767bc47dae5cc205686fed6b5fb43c26
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67384191"
---
# <a name="building-a-printer-graphics-dll"></a>プリンター グラフィックス DLL をビルドする





プリンター グラフィックス DLL をビルドする場合は、Dll は、ユーザー モードでの実行およびカーネル モードでの実行用の次の違いに注意する必要があります。

**注**   Windows Vista では、ユーザー モードでプリンター グラフィックス Dll は実行できるのみです。 詳細については、次を参照してください。[選択ユーザー モードまたはカーネル モード](choosing-user-mode-or-kernel-mode.md)します。

 

### <a name="rules-for-building-a-printer-graphics-dll"></a>プリンター グラフィックス DLL を構築するための規則

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>ユーザー モードのグラフィックス DLL</th>
<th>カーネル モードのグラフィックス DLL</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>TARGETTYPE を設定するソース ファイルで DYNLINK を = です。</p></td>
<td><p>TARGETTYPE を設定するソース ファイルで GDI_DRIVER を = です。</p></td>
</tr>
<tr class="even">
<td><p>Winddi.h が含まれる前に、プリプロセッサ マクロ USERMODE_DRIVER をソース ファイルで定義する必要があります。</p></td>
<td><p>プリプロセッサ マクロ USERMODE_DRIVER を定義する必要があります。</p></td>
</tr>
<tr class="odd">
<td><p>オブジェクトのモジュールは、インポート ライブラリ umpdddi.lib gdi32.lib とリンクする必要があります。</p></td>
<td><p>オブジェクトのモジュールは、win32k.lib インポート ライブラリとリンクする必要があります。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvquerydriverinfo" data-raw-source="[&lt;strong&gt;DrvQueryDriverInfo&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvquerydriverinfo)"> <strong>DrvQueryDriverInfo</strong> </a>関数が返す必要があります<strong>TRUE</strong> DRVQUERY_USERMODE の。</p></td>
<td><p><a href="https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvquerydriverinfo" data-raw-source="[&lt;strong&gt;DrvQueryDriverInfo&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvquerydriverinfo)"> <strong>DrvQueryDriverInfo</strong> </a>関数が返す必要があります<strong>FALSE</strong> DRVQUERY_USERMODE の。 (または、関数は省略できます。)</p></td>
</tr>
</tbody>
</table>

 

 

 




