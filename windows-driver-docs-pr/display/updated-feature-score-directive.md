---
title: Windows 8 の機能が更新されたスコア ディレクティブ
description: 更新された機能スコアのディレクティブは、Windows Display Driver Model (WDDM) に続くすべての Windows 8 ドライバーに必要なインストールに関する一般的な設定です。
ms.assetid: E50E132A-DEC8-42F4-AAF8-05F658990CF5
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: f23be96576ac2d2328f7a8e6cf45a7d83e56607e
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56559130"
---
# <a name="updated-feature-score-directive-in-windows-8"></a>Windows 8 の機能が更新されたスコア ディレクティブ


更新された機能スコアのディレクティブは、Windows Display Driver Model (WDDM) に続くすべての Windows 8 ドライバーに必要なインストールに関する一般的な設定です。

次の表では、Windows 8 に適用される値を示します。 キーの変更は、斜体でいます。

**WDDM のバージョンの特徴のスコア**

| ドライバー モデル                     | 特徴のスコア                |
|----------------------------------|------------------------------|
| *Windows 8 WHQL*                 | *E0*                         |
| *Windows 8 のプレリリース版のドライバー*   | *E3*                         |
| Windows 7 WHQL                   | E6                           |
| Windows 7 の受信トレイ                  | EC                           |
| Windows Vista WHQL               | F6                           |
| Windows Vista の受信トレイ              | F8                           |
| *Microsoft Basic ディスプレイ ドライバー* | *FB*                         |
| XDDM サード パーティ                 | FC *(Windows 8 では使用されない)* |
| Windows Vista で XDDM 受信トレイ      | FD *(Windows 8 では使用されない)* |
| VGA                              | FE *(Windows 8 では使用されない)* |
| 既定値またはないスコア              | FF                           |
| 署名されていないドライバー                 | ない特徴スコア = FF        |

 

各オペレーティング システムのリリースでは、新しい機能スコアの値について説明します。 これは Windows 8 向け*E3*ボックスで、プレリリース版のドライバーと*E0* WHQL ドライバー。 特徴のスコアは、複数の利用可能なドライバーが存在する場合にインストールするドライバーを決定する、Windows によって使用されます。 高いランク付けされた特徴のスコアを持つ運転手が選択されます。

Windows 8 では、インボックス ドライバーのすべてのデバイスでは、インボックス ドライバーが Windows 8 でテストされており、既存の Windows 7Windows 7 ドライバーがあるため、すべての既存の Windows 7 ドライバーよりも高いランク付けされた特徴のスコアがあります。 これにより、既存のドライバーが Windows 7 を置き換える、インボックス Windows 8 ドライバー。 独立系ハードウェア ベンダー (IHV) は、次の条件が true の場合、Windows 7 ドライバーを使用した E0 特徴のスコアを使用できます。

-   ドライバーは、Windows 8 向けテストされています。
-   ドライバーは、インボックス ドライバーよりも強化する修正します。
-   ドライバーは、Windows 8 へのアップグレード時に保持されるものです。

 

 





