---
title: トリアージ WDTF ベースのテスト
description: WDTF ベースのテストで起こっているかを理解するために、WDTF オブジェクトのログ記録と WPP ソフトウェア トレースの組み込みのサポートを使用することができます。
ms.assetid: C2F7AA74-7A74-4EA4-AD2D-8143252380C8
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c026384159c004d68b28952d973f61f039cd1bb0
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56556506"
---
# <a name="triaging-wdtf-based-tests"></a>トリアージ WDTF ベースのテスト


組み込みサポートを使用する、WDTF ベースのテストで起こっているかを理解するために、 [WDTF オブジェクトのログ記録](logging-and-tracing.md)と[WPP ソフトウェア トレース](https://msdn.microsoft.com/library/windows/hardware/ff556204)します。

Automatcially WDTF オブジェクト記述を簡略化できます共通のログ ファイルにログ メッセージがテスト作成と役立つことができます WDTF オブジェクトのログ記録の原因は、テストの問題を診断します。 デバイスの基本的なテストと WDK に含まれているその他のテストは、WDTF ベースのテストの例を示します。 これらのテストについては、次を参照してください。[を選択し、デバイスの基本的なテストを構成する方法](https://msdn.microsoft.com/windows-drivers/develop/how_to_select_and_configure_the_device_fundamental_tests)します。

サポートを提供する WDTF [WPP ソフトウェア トレース](https://msdn.microsoft.com/library/windows/hardware/ff556204)します。 WDTF のすべてのオブジェクトは、実行中にトレース情報を生成します。 など、WDK のツールを使用して、トレース情報を読み取れる[traceview で](https://msdn.microsoft.com/library/windows/hardware/ff556063)します。

## <a name="in-this-section"></a>このセクションの内容


-   [WDTF オブジェクトのログ記録](logging-and-tracing.md)
-   [有効化と WDTF トレースの表示](viewing-wdtf-traces.md)
-   [WDTF ベースのテストを実行している問題を診断します。](diagnosing-problems-running-wdtf-based-tests.md)

 

 




