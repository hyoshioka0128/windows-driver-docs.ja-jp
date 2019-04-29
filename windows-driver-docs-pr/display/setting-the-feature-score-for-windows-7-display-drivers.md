---
title: Windows 7 ディスプレイ ドライバーの機能スコアの設定
description: Windows 7 ディスプレイ ドライバーの機能スコアの設定
ms.assetid: 7b2cf25d-a88d-48e1-8d62-8c245c289566
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9148246fd84492b9a12f0ffe2e2d4e47f93ca185
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63390441"
---
# <a name="setting-the-feature-score-for-windows-7-display-drivers"></a>Windows 7 ディスプレイ ドライバーの機能スコアの設定


このセクションでは、Windows 7 以降および Windows Server 2008 R2 以降のバージョンの Windows オペレーティング システムにのみ適用されます。

**FeatureScore**ディレクティブは、Windows Vista およびそれ以降のオペレーティング システムをインストールして実行するすべてのドライバーに必要です。 Windows Vista の適用機能スコアの設定が記載されて[ドライバーの特徴のスコアを設定](setting-the-driver-feature-score.md)します。 次の表では、Windows 7 以降を適用するスコアの設定、機能を示します。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">機能
<div>
 
</div>
score</th>
<th align="left">ドライバー モデルと配布方法</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>E6</p></td>
<td align="left"><p>Windows Display Driver Model (WDDM) に書き込まれるベンダーから提供されたドライバー モデルの Windows 7 の機能用に最適化された、Windows Hardware Quality Labs (WHQL) によってが修飾されている Windows 7 ドライバー パッケージでパッケージ化されに含まれる、Windows<a href="https://go.microsoft.com/fwlink/p/?linkid=138031" data-raw-source="[Compatibility Center](https://go.microsoft.com/fwlink/p/?linkid=138031)">互換性センター</a>テスト済み製品一覧</p></td>
</tr>
<tr class="even">
<td align="left"><p>E6</p></td>
<td align="left"><p>ベンダーから提供されたドライバーは、WDDM に書き込まれるモデルの Windows 7 の機能用に最適化され、の統合された Windows 7 および Windows Vista ドライバー パッケージ、Windows ハードウェア認定キットを使用して、認定されているパッケージに付属</p></td>
</tr>
<tr class="odd">
<td align="left"><p>EC</p></td>
<td align="left"><p>WDDM に書き込まれるインボックス ドライバー モデルの Windows 7 の機能用に最適化された、Windows 7 のドライバー パッケージに同梱されています。</p></td>
</tr>
<tr class="even">
<td align="left"><p>F4</p></td>
<td align="left"><p>統合された Windows 7 および Windows Vista ドライバー パッケージ、Windows ハードウェア認定キットを使用してパッケージの認定と WDDM に書き込まれるベンダーから提供されたドライバー</p></td>
</tr>
<tr class="odd">
<td align="left"><p>F4</p></td>
<td align="left"><p>Windows 7 のドライバー パッケージと WDDM に書き込まれるインボックス ドライバー</p></td>
</tr>
<tr class="even">
<td align="left"><p>F6</p></td>
<td align="left"><p>ベンダーから提供されたドライバーが WHQL で修飾し、Windows に含まれる Windows Vista ドライバー パッケージに WDDM に書き込まれる<a href="https://go.microsoft.com/fwlink/p/?linkid=138031" data-raw-source="[Vista Compatibility Center](https://go.microsoft.com/fwlink/p/?linkid=138031)">Vista 互換性センター</a>テスト済み製品一覧</p></td>
</tr>
<tr class="odd">
<td align="left"><p>F8</p></td>
<td align="left"><p>Windows Vista のドライバー パッケージと WDDM に書き込まれるインボックス ドライバー</p></td>
</tr>
<tr class="even">
<td align="left"><p>FC</p></td>
<td align="left"><p>書き込まれるベンダーから提供されたドライバー、 <a href="windows-2000-display-driver-model-design-guide.md" data-raw-source="[Windows 2000 display driver model](windows-2000-display-driver-model-design-guide.md)">Windows 2000 のディスプレイ ドライバー モデル</a></p></td>
</tr>
<tr class="odd">
<td align="left"><p>FD</p></td>
<td align="left"><p>ボックス内に書き込まれる Windows Vista のドライバー、 <a href="windows-2000-display-driver-model-design-guide.md" data-raw-source="[Windows 2000 display driver model](windows-2000-display-driver-model-design-guide.md)">Windows 2000 のディスプレイ ドライバー モデル</a></p></td>
</tr>
<tr class="even">
<td align="left"><p>FE</p></td>
<td align="left"><p>ビデオのグラフィックスの配列 (VGA) ドライバー</p></td>
</tr>
</tbody>
</table>

 

Wddm ドライバー、グラフィックス ハードウェアのベンダーを配置する必要があります、 **FeatureScore**下ディレクティブ、 [ **DDInstall セクション**](https://msdn.microsoft.com/library/windows/hardware/ff547344)の INF ファイルと使用**FeatureScore**ドライバーに、特徴のスコアを適用します。

[Windows 2000 Display Driver Model](windows-2000-display-driver-model-design-guide.md)ドライバー、Microsoft で、Windows 2000 Display Driver Model ドライバーのまたは、INF ドライバーのインストールの実行時に、クラスのインストーラーで適切な特徴のスコアが適用されます。 ベンダーが使用する必要があります、 **FeatureScore**ディレクティブには、Windows 2000 Display Driver Model ドライバーの特徴のスコアを挿入します。

未署名のドライバは、FF に相当する特徴のスコアを受け取ります。 この値は、既定値は、スコアがないことを示します。

 

 





