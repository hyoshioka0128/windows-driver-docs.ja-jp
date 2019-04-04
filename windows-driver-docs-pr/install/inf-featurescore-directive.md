---
title: INF FeatureScore ディレクティブ
description: FeatureScore ディレクティブは、ドライバーをドライバーがサポートする機能に基づいて、追加の順位付け条件を提供します。
ms.assetid: 78e1c2cf-b3e9-43ea-b435-979360cc3e28
keywords:
- INF FeatureScore ディレクティブ デバイスとドライバーのインストール
topic_type:
- apiref
api_name:
- INF FeatureScore Directive
api_type:
- NA
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1263574f3266e452e0970eb90e095d1a453a2737
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56548765"
---
# <a name="inf-featurescore-directive"></a>INF FeatureScore ディレクティブ


**FeatureScore**ディレクティブのドライバーをドライバーがサポートする機能に基づいて、追加の順位付け条件を提供します。 特徴のスコアを定義できますなど、[デバイス セットアップ クラス](device-setup-classes.md)クラスに固有の条件に基づくドライバーを識別するためです。

```ini
[DDInstall]
  
FeatureScore=featurescore
```

**FeatureScore**ディレクティブは、Windows Vista および以降のバージョンの Windows でサポートされます。

**警告**  、 **FeatureScore**ディレクティブが処理されるで直接指定した場合のみ、 **\[DDInstall\]** セクション。

 

## <a name="entries"></a>エントリ


<a href="" id="featurescore"></a>*featurescore*  
この値は、その機能の内容に基づいて、ドライバーのランク付けのスコアを指定します。 このエントリは、0x00 と 0 xff までの間の 1 バイトの 16 進数です。

低い*featurescore*値より優れた機能を 0x00 が最適な特徴のスコア順位、スコアのランクを指定します。 場合、 **FeatureScore**ディレクティブが指定されていない、Windows は、ドライバーの 0 xff の既定機能スコアのランクを使用します。

<a name="remarks"></a>注釈
-------

Windows では、同じデバイスに対して複数のドライバーを検出する場合は、最初をインストールする最適なドライバーをドライバーを確認しする必要があります。 これを実現するには、Windows は、全体的なランク付けがいくつかの要因、または、次のように、スコアに基づいて各ドライバーを割り当てます。

-   ドライバーの署名のスコア付け ([*署名スコア*](signature-score--windows-vista-and-later-.md) ) かどうかに、ドライバーが署名されているかどうかに基づいて、します。
-   ドライバーの特徴のスコア ([*特徴スコア*](feature-score--windows-vista-and-later-.md)) ドライバーの機能のデバイス用の別のドライバーと比較したランクに基づいて、します。
-   ハードウェア識別子のスコア付け ([*識別子スコア*](identifier-score--windows-vista-and-later-.md))、に基づいてどの程度プラグ アンド プレイ (PnP) デバイスの識別文字列はドライバーによって報告された、バスとが一致するデバイスを[デバイスの識別文字列](device-identification-strings.md)、INF で[***モデル***](inf-models-section.md) INF ファイルのセクション。

特徴のスコアは、ドライバーをサポートする機能に基づいてランクのドライバーを方法を提供します。 特徴のスコアを定義できますなど、[デバイス セットアップ クラス](device-setup-classes.md)クラスに固有の条件に基づいてドライバーを識別するためです。

特徴のスコアは、ドライバー作成者より簡単かつ正確には明確に定義された条件に基づいているデバイスのさまざまなドライバーを区別することができます識別子スコアを補足します。

ドライバーが順位付けされる方法の詳細については、[どの Windows ランクのドライバー (Windows Vista 以降)](how-setup-ranks-drivers--windows-vista-and-later-.md)を参照してください。

## <a name="see-also"></a>関連項目


[特徴のスコア](feature-score--windows-vista-and-later-.md)

[識別子のスコア](identifier-score--windows-vista-and-later-.md)

[***モデル***](inf-models-section.md)

[署名のスコア](signature-score--windows-vista-and-later-.md)

 

 






