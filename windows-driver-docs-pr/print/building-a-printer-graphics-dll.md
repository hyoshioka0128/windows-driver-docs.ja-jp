---
title: プリンター グラフィックス DLL の構築
description: プリンター グラフィックス DLL の構築
ms.assetid: bec1e9cc-a846-43e5-bc9e-e43a151ef6c4
keywords:
- プリンター グラフィックスの構築、DLL の WDK
- グラフィックスの DLL の WDK プリンター、ビルド
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2e203066f09f027d734a131089edb42948f218eb
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56550044"
---
# <a name="building-a-printer-graphics-dll"></a>プリンター グラフィックス DLL の構築





プリンター グラフィックス DLL をビルドする場合は、Dll は、ユーザー モードでの実行およびカーネル モードでの実行用の次の違いに注意する必要があります。

**注**   Windows Vista では、ユーザー モードでプリンター グラフィックス Dll は実行できるのみです。 詳細については、[選択ユーザー モードまたはカーネル モード](choosing-user-mode-or-kernel-mode.md)を参照してください。

 

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
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff556261" data-raw-source="[&lt;strong&gt;DrvQueryDriverInfo&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff556261)"> <strong>DrvQueryDriverInfo</strong> </a>関数が返す必要があります<strong>TRUE</strong> DRVQUERY_USERMODE の。</p></td>
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff556261" data-raw-source="[&lt;strong&gt;DrvQueryDriverInfo&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff556261)"> <strong>DrvQueryDriverInfo</strong> </a>関数が返す必要があります<strong>FALSE</strong> DRVQUERY_USERMODE の。 (または、関数は省略できます。)</p></td>
</tr>
</tbody>
</table>

 

 

 




