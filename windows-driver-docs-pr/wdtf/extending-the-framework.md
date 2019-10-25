---
title: フレームワークの拡張
description: フレームワークの拡張
ms.assetid: 37a0fd70-0c88-414f-b4e3-afd641f1c667
keywords:
- Windows デバイステストフレームワーク WDK、WDTF の拡張
- WDTF WDK、WDTF の拡張
- Windows デバイステストフレームワーク WDK、アクションインターフェイス
- WDTF WDK、アクションインターフェイス
- Windows デバイステストフレームワーク WDK、サンプル
- WDTF WDK、サンプル
- SimpleIO wizard WDK WDTF
- アクションインターフェイス WDK WDTF
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4b7bca0282f495659ac169a470225d88d1463e69
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72823498"
---
# <a name="extending-the-framework"></a>フレームワークの拡張


WDTF は拡張できるように構築されています。 次の図に示すように、拡張性は3つの異なる方法で使用できます。

![wdtf シナリオモデルを示す図](images/wdtf-scenariomodel.gif)

次の一覧では、3つの拡張メソッドについて説明します。

-   **サンプルスクリプトを変更**します。 このメソッドは、前の図では緑で示されています。 WDTF によって提供される[サンプルスクリプト](sample-wdtf-scenarios.md)のいずれかを使用して、シナリオに合わせて変更することができます。 [WDTF シナリオ](creating-wdtf-scenarios.md)はゼロから作成することもできます。

-   SimpleIO の**ような既存の**[**アクションインターフェイス**](https://docs.microsoft.com/windows-hardware/drivers/ddi/index)を**実装**します。 このメソッドは、前の図では黄色で示されています。 既存のアクションインターフェイスを実装して、インターフェイスが機能するターゲットの型を拡張することができます。 デバイスの種類に SimpleIO を実装すると、既存のすべての WDTF ベースのシナリオによって、デバイスの i/o 検証が自動的に開始されます。

    WDTF には、SimpleIO の実装を支援する Microsoft Visual Studio テンプレートが用意されています。 詳細については、「[デバイスの WDTF SimpleIO プラグインを作成する](writing-a-wdtf-simpleio-plug-in-for-your-device.md)」を参照してください。

-   新しい[**アクションインターフェイス**](https://docs.microsoft.com/windows-hardware/drivers/ddi/index)**を作成して実装**します。 このメソッドは、前の図では赤で示されています。 WDTF によって提供される機能が、コンポーネントベースのシナリオを構築するには不十分な場合は、WDTF を使用して新しいコンポーネントを作成できます。

    このメソッドは、 [COM インターフェイスのデザインスキル](com-interface-design-skills.md)を必要とするため、3つのメソッドの中で最も困難です。 COM オートメーションインターフェイスを使用して、機能の単純な抽象化を設計および実装できる必要があります。

 

 




