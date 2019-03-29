---
title: WDDM ドライバーのバージョン番号
description: WDDM ドライバーのバージョン番号
ms.assetid: 14608626-cd01-4756-8329-187153a8b99a
keywords:
- ドライバー モデル WDK Windows Vista では、バージョン番号を表示します。
- Windows Vista ディスプレイ ドライバー モデル、WDK バージョン番号
- バージョン番号 WDK の表示
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 658900f0a2614e096a854bac49d0871ed5bb1bc9
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56581558"
---
# <a name="version-numbers-for-wddm-drivers"></a>WDDM ドライバーのバージョン番号


ディスプレイ ドライバー Windows 表示 Driver Model (WDDM) に準拠していることを確認するまたは[Windows 2000 display driver model (XDDM)](windows-2000-display-driver-model-design-guide.md) Microsoft Windows で Microsoft DirectX の特定のバージョンで実行する を適用する必要がある、ドライバーを適切なバージョン番号です。 任意の DirectX アプリケーションをインストールするときに、ベンダーは、正しくない形式を使用するバージョン番号または不適切なバージョン番号にディスプレイ ドライバーを配布する場合に、エンドユーザーで問題が発生します。

**注**   、 **DriverVer**ディレクティブは、ドライバー パッケージをドライバー ファイル、INF ファイル自体には、INF ファイルなどのバージョン情報を追加する方法を提供します。 使用して、 **DriverVer**ディレクティブ、安全かつ明確を置換できますドライバー パッケージを同じパッケージの将来のバージョン。 このディレクティブの詳細については、次を参照してください。 [ **INF DriverVer ディレクティブ**](https://msdn.microsoft.com/library/windows/hardware/ff547394)します。

 

この表では、DirectX のさまざまなバージョンと互換性のために、WDDM に準拠しているベンダー製のディスプレイ ドライバーの適切なバージョン番号の範囲の例を示します。 \\

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">ターゲット システム</th>
<th align="left">バージョン番号の範囲</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>WDDM と DirectX 9.0 と互換性のあるドライバーを表示します。</p></td>
<td align="left"><p>7.14.01.0000 - 7.14.99.9999</p></td>
</tr>
<tr class="even">
<td align="left"><p>WDDM と DirectX 10.0 と互換性のあるドライバーを表示します。</p></td>
<td align="left"><p>7.15.01.0000 - 7.15.99.9999</p></td>
</tr>
</tbody>
</table>

 

このテーブルに準拠するベンダーから提供されたのディスプレイ ドライバーの適切なバージョン番号の範囲には、 [Windows 2000 のディスプレイ ドライバー モデル](windows-2000-display-driver-model-design-guide.md)DirectX 9.0 と互換性のためです。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">ターゲット システム</th>
<th align="left">バージョン番号の範囲</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>XDDM と DirectX 9.0 と互換性のあるドライバーを表示します。</p></td>
<td align="left"><p>6.14.01.0000 - 6.14.99.9999</p></td>
</tr>
</tbody>
</table>

 

ディスプレイ ドライバーのバージョン管理の詳細については、次を参照してください。[表示ドライバーのバージョン番号](version-numbers-for-display-drivers.md)と[ドライバーのバージョン管理](wddm-2-1-features.md#driver-versioning)します。

 

 





