---
title: 機能のスコア
description: 機能のスコア
ms.assetid: cc7f2cd1-85aa-43be-9c4e-abdba3a4310a
keywords:
- 機能スコアの WDK デバイスのインストール
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 11e3a5daa004035d7a1734ce6406757403887eb7
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56579343"
---
# <a name="feature-score"></a>機能のスコア


ドライバーのランクは 0 x として書式設定*SSGGTHHH*ここで、0 x の値*SS*000000、[署名スコア](signature-score--windows-vista-and-later-.md)、0x00 の値*GG*0000 です特徴のスコアと、値 0x0000*THHH*は、[識別子スコア](identifier-score--windows-vista-and-later-.md)します。

特徴のスコアは、ドライバーをサポートする機能に基づいてランクのドライバーを方法を提供します。 特徴のスコアを定義できますなど、[デバイス セットアップ クラス](device-setup-classes.md)クラスに固有の条件に基づいてドライバーを識別するためです。 特徴のスコアは、ドライバーの作成者をより簡単かつ正確には、明確に定義された条件に基づいているデバイスのさまざまなドライバーによって区別できるように、識別子のスコアを補足します。

Microsoft では、特定のデバイス クラスの機能スコアの使用状況を定義します。 特徴のスコアは必要ありません、ほど多くのデバイス クラスには、指定した機能スコアの使用量はありません。 ここでは、既定の特徴のスコア (0 xff) が必要ですがない場合、ドライバーの INF で定義されている特徴のスコアが割り当てられます。

Microsoft によってデバイス クラスの特徴のスコアが明示的に要求しないときに、ドライバーが必要です。

-   ドライバーの INF の特徴のスコアが定義されていません (0 xff まで Windows が既定の)

    または

-   ドライバーの INF で 0 xff の特徴のスコアを明示的に定義します。

ドライバーの特徴のスコアは設定、 [ **INF FeatureScore ディレクティブ**](inf-featurescore-directive.md)で、 [ **INF DDInstall セクション**](inf-ddinstall-section.md) INF ファイルをデバイスをインストールします。 特徴のスコアはよう設定します。

```cpp
[DDInstallSectionName]
. . .
FeatureScore=featurescore
```

場所*DDInstallSectionName*の名前を指定します、 *DDInstall*セクションと*featurescore* 0x00 と 0 xff までの間の 1 バイトの 16 進数です。 Windows ドライバーに基づく特徴のスコアを計算する、 *featurescore*の値、 **FeatureScore**ディレクティブ。

```cpp
feature score = (featurescore * 0x10000)
```

場合、 [ **INF FeatureScore ディレクティブ**](inf-featurescore-directive.md)が既定の特徴のスコアは、ドライバーは、基本設定の機能に基づいたがないことを示します 0x00FF0000 Windows は、INF ファイルで指定されていません。ドライバー。 小さい機能は、スコア付け、ほどのランク、最適な特徴のスコアが 0x00000000 が。

たとえば、次を設定します、ドライバーの特徴のスコア 0x00FD0000。

```cpp
[DDInstallSectionName]
. . .
FeatureScore=xFD
```

ドライバーのランク付けの詳細については、次を参照してください。[ランク ドライバーをどのように Windows](how-setup-ranks-drivers--windows-vista-and-later-.md)します。

 

 





