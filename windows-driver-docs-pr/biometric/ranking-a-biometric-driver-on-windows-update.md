---
title: Windows Update における生体認証ドライバーのランク付け
description: Windows Update における生体認証ドライバーのランク付け
ms.assetid: fc8634ab-0ecd-4390-9834-825f60fe68ce
keywords:
- 生体認証ドライバー WDK、Windows Update で順位付け
- 生体認証ドライバー WDK 生体認証を順位付け
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0fc9a56c5201890283c9bef44f27eb3531a925a5
ms.sourcegitcommit: 1a5d7884cec9dd8d2b85242bee78b56a1cf8e4c9
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/01/2019
ms.locfileid: "58761853"
---
# <a name="ranking-a-biometric-driver-on-windows-update"></a>Windows Update における生体認証ドライバーのランク付け

両方のレガシ生体認証を提供するベンダーと WBDI ドライバーは、Windows Update からインストールされているドライバーを制御するのにドライバーの特徴のスコアを使用できます。

Windows 生体認証フレームワークで正しく動作するため、ドライバーがサポートしている排他アクセスが認識をサポートしているレガシ エンジンと WBDI は、1 つのドライバーを記述することを選択したベンダーがあります。 排他アクセスを無効にすると、ドライバーは、従来のドライバーとして機能します。 レジストリでの排他値を設定する方法を確認するを参照してください。[生体認証ドライバーをインストールする](installing-a-biometric-driver.md)します。

さらに、レガシ モードで動作している生体認証ドライバーには、GUID が割り当てる必要がありますいない\_DEVINTERFACE\_生体認証の\_リーダー デバイスのインターフェイス。 このデバイスのインターフェイスの割り当ては、ドライバーを認識する Windows 生体認証サービスです。

特徴のスコアが適切に設定されている場合、WBDI ドライバーのみがない生体認証ドライバー既にインプレース システムでインストールされています。

従来のスタックを有効にする、顧客が決定したら、顧客は WBDI ドライバー経由でより高いランクのレガシ ドライバーをインストールできます。

## <a name="how-feature-score-works"></a>どの機能のスコアのしくみ

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

ドライバーの特徴のスコアを設定する方法の詳細については、[特徴スコア](https://docs.microsoft.com/windows-hardware/drivers/install/feature-score--windows-vista-and-later-)を参照してください。
