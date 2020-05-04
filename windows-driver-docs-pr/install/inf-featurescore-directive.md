---
title: INF FeatureScore ディレクティブ
description: Features Core ディレクティブは、ドライバーがサポートする機能に基づいて、ドライバーの追加の順位付け条件を提供します。
ms.assetid: 78e1c2cf-b3e9-43ea-b435-979360cc3e28
keywords:
- INF の主要なディレクティブデバイスとドライバーのインストール
topic_type:
- apiref
api_name:
- INF FeatureScore Directive
api_type:
- NA
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 631a9b80dae40aa5cf9fba4ae5379b1c488c6582
ms.sourcegitcommit: a55489992dbf0a7e9d09f237e13514799711647a
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/28/2020
ms.locfileid: "82223162"
---
# <a name="inf-featurescore-directive"></a>INF FeatureScore ディレクティブ


Features **core**ディレクティブは、ドライバーがサポートする機能に基づいて、ドライバーの追加の順位付け条件を提供します。 たとえば、クラス固有の条件に基づくドライバーを区別する[デバイスセットアップクラス](device-setup-classes.md)に対して、機能スコアが定義されている場合があります。

```inf
[DDInstall]
  
FeatureScore=featurescore
```

Windows Vista 以降のバージョンの Windows**では、このディレクティブは**サポートされています。

**警告**  - **[ \[ddinstall\] ** ] セクションで直接指定されている場合にのみ、[領域の**コア**] ディレクティブが処理されます。

 

## <a name="entries"></a>エントリ


<a href="" id="featurescore"></a>*特長コア*  
この値は、ドライバーの機能の内容に基づいた順位付けスコアを指定します。 このエントリは、0x00 から0xFF までの1バイトの16進数です。

特徴の*コア*値が小さいほど、特徴スコアランクが向上します。ここで、0x00 は最適な特徴スコアランクです。 機能**コア**ディレクティブが指定されていない場合、Windows では、ドライバーに対して既定の特徴スコアランク0xff を使用します。

<a name="remarks"></a>解説
-------

Windows が同じデバイスに対して複数のドライバーを検出した場合は、まず、どのドライバーがインストールに最適なドライバーであるかを判断する必要があります。 これを実現するために、Windows は、次のようないくつかの要素またはスコアに基づいて、各ドライバーに全体的なランクを割り当てます。

-   ドライバーが署名されているかどうかに基づくドライバー署名スコア ([*署名スコア*](signature-score--windows-vista-and-later-.md))。
-   ドライバーの機能スコア ([*機能スコア*](feature-score--windows-vista-and-later-.md))。ドライバーの機能のランクとデバイスの別のドライバーとの比較に基づいています。
-   ハードウェア識別子スコア ([*識別子スコア*](identifier-score--windows-vista-and-later-.md))。デバイスのバスドライバーによって報告されたプラグアンドプレイ (PnP) デバイス識別文字列が、inf ファイルの [inf[***モデル***](inf-models-section.md)] セクションの[デバイス id 文字列](device-identification-strings.md)と一致するかどうかに基づいて決まります。

機能スコアは、ドライバーがサポートする機能に基づいてドライバーに順位を付ける方法を提供します。 たとえば、クラス固有の条件に基づいてドライバーを区別する[デバイスセットアップクラス](device-setup-classes.md)に対して、機能スコアが定義されている場合があります。

特徴スコアは識別子スコアを補足します。これにより、ドライバーの作成者は、明確に定義された条件に基づいて、デバイスのさまざまなドライバーをより簡単かつ正確に識別できるようになります。

ドライバーの順位付けの詳細については、「Windows がドライバーをランク付けする[方法 (Windows Vista 以降)](how-setup-ranks-drivers--windows-vista-and-later-.md)」を参照してください。

## <a name="see-also"></a>関連項目


[機能スコア](feature-score--windows-vista-and-later-.md)

[識別子スコア](identifier-score--windows-vista-and-later-.md)

[***モデル***](inf-models-section.md)

[署名スコア](signature-score--windows-vista-and-later-.md)

 

 






