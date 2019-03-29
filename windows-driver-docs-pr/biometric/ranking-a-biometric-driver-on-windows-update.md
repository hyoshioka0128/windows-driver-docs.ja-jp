---
title: Windows Update における生体認証ドライバーのランク付け
description: Windows Update における生体認証ドライバーのランク付け
ms.assetid: fc8634ab-0ecd-4390-9834-825f60fe68ce
keywords:
- 生体認証ドライバー WDK、Windows Update で順位付け
- 生体認証ドライバー WDK 生体認証を順位付け
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 76f287e954c65e1d1205b0db3a80ed425816a64c
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56574746"
---
# <a name="ranking-a-biometric-driver-on-windows-update"></a>Windows Update における生体認証ドライバーのランク付け


両方のレガシ生体認証を提供するベンダーと WBDI ドライバーは、Windows Update からインストールされているドライバーを制御するのにドライバーの特徴のスコアを使用できます。

Windows 生体認証フレームワークで正しく動作するため、ドライバーがサポートしている排他アクセスが認識をサポートしているレガシ エンジンと WBDI は、1 つのドライバーを記述することを選択したベンダーがあります。 排他アクセスを無効にすると、ドライバーは、従来のドライバーとして機能します。 レジストリでの排他値を設定する方法を確認するを参照してください。[生体認証ドライバーをインストールする](installing-a-biometric-driver.md)します。

さらに、レガシ モードで動作している生体認証ドライバーには、GUID が割り当てる必要がありますいない\_DEVINTERFACE\_生体認証の\_リーダー デバイスのインターフェイス。 このデバイスのインターフェイスの割り当ては、ドライバーを認識する Windows 生体認証サービスです。

特徴のスコアが適切に設定されている場合、WBDI ドライバーのみがない生体認証ドライバー既にインプレース システムでインストールされています。

従来のスタックを有効にする、顧客が決定したら、顧客は WBDI ドライバー経由でより高いランクのレガシ ドライバーをインストールできます。

### <a name="span-idhowfeaturescoreworksspanspan-idhowfeaturescoreworksspanhow-feature-score-works"></a><span id="how_feature_score_works"></span><span id="HOW_FEATURE_SCORE_WORKS"></span>どの機能のスコアのしくみ

特徴のスコアは、全体的なドライバーのランクの 3 番目と 4 番目の桁で表されます。 たとえば、 *GG*特徴のスコア次のドライバーのランクからには。

```cpp
0x00GG0000 
```

小さい番号の機能では、一致が高いことを示します。 既定の特徴のスコアは、0 xff は、ドライバーの機能に基づく基本設定がないことを示します。

Microsoft は、従来の生体認証ドライバー 0xa0 の特徴のスコアをお勧めします。 後でオーバーライドする必要がある場合、特徴のスコアを 0x00 を設定しない必要があります。

ドライバーの特徴のスコアは、INF FeatureScore ディレクティブで設定されて、 [ **INF DDInstall セクション**](https://msdn.microsoft.com/library/windows/hardware/ff547344)デバイス。

たとえば、次のコードでは、0x20 をドライバーの特徴のスコアを設定します。

```cpp
[DDInstallSectionName]
. . .
FeatureScore=x20
```

ドライバーの特徴のスコアを設定する方法の詳細については、次を参照してください。[特徴のスコア (Windows Vista)](https://go.microsoft.com/fwlink/p/?linkid=132806)します。

 

 





