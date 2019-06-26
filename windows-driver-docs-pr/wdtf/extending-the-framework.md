---
title: フレームワークの拡張
description: フレームワークの拡張
ms.assetid: 37a0fd70-0c88-414f-b4e3-afd641f1c667
keywords:
- Windows デバイスのテスト フレームワーク WDK、WDTF を拡張します。
- WDTF WDK、WDTF を拡張します。
- Windows デバイスのテスト フレームワーク WDK、アクションのインターフェイス
- WDTF WDK、アクションのインターフェイス
- Windows デバイスのテスト フレームワーク WDK サンプル
- WDTF WDK サンプル
- SimpleIO ウィザード WDK WDTF
- アクションは、WDK WDTF をインターフェイスします。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6e5e724f617b7f06d1aca970555ebda34460198a
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67366487"
---
# <a name="extending-the-framework"></a>フレームワークの拡張


WDTF は拡張性が構築されています。 性は、次の図に示すように 3 つの異なる方法で可能性があります。

![wdtf シナリオのモデルを示す図](images/wdtf-scenariomodel.gif)

難易度の順序で、次の 3 つの機能拡張メソッドは次のとおりです。

-   **サンプル スクリプトを変更する**します。 このメソッドは、上記の図の緑色に表示されます。 WDTF 標準のいずれかを実行することができます[サンプル スクリプト](sample-wdtf-scenarios.md)シナリオに合わせて変更しています。 できます[WDTF シナリオを作成](creating-wdtf-scenarios.md)最初から。

-   **既存の実装** [**アクション インターフェイス**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/index)**と同様に、** SimpleIO します。 このメソッドは、黄色が上記の図に表示されます。 インターフェイスが機能する対象の種類を拡張する既存のアクション インターフェイスを実装できます。 デバイスの種類に、SimpleIO を実装する場合、デバイスの I/O の検証を実行する WDTF ベースの既存のシナリオのすべてを自動的に開始されます。

    WDTF は、SimpleIO の実装で支援するために Microsoft Visual Studio テンプレートを提供します。 詳細については、次を参照してください。 [WDTF SimpleIO がデバイスのプラグインを記述](writing-a-wdtf-simpleio-plug-in-for-your-device.md)します。

-   **作成 (および実装し)、新しい** [**アクション インターフェイス**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/index)します。 このメソッドは、上記の図で赤色で表示されます。 WDTF を提供する機能が、コンポーネント ベースのシナリオを構築するのに十分でない場合は、新しいコンポーネントを作成する WDTF を使用できます。

    必要があるために、このメソッドは 3 つのメソッドの中で最も難しい[COM インターフェイスの設計スキル](com-interface-design-skills.md)します。 設計と COM オートメーション インターフェイスを使用して、機能の単純な抽象化を実装する必要があります。

 

 




