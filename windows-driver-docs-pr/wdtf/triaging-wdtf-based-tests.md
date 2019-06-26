---
title: WDTF ベース テストのトリアージ
description: WDTF ベースのテストで起こっているかを理解するために、WDTF オブジェクトのログ記録と WPP ソフトウェア トレースの組み込みのサポートを使用することができます。
ms.assetid: C2F7AA74-7A74-4EA4-AD2D-8143252380C8
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 31ec77d4107ae7b568bd1d799a82c60b1c03ca2f
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67369458"
---
# <a name="triaging-wdtf-based-tests"></a>WDTF ベース テストのトリアージ


WDTF ベースのテストで行われる内容についての理解を深めるために、[WDTF オブジェクト ログ](logging-and-tracing.md)および [WPP ソフトウェア トレース](https://docs.microsoft.com/windows-hardware/drivers/devtest/wpp-software-tracing)の組み込みのサポートを使用できます。

Automatcially WDTF オブジェクト記述を簡略化できます共通のログ ファイルにログ メッセージがテスト作成と役立つことができます WDTF オブジェクトのログ記録の原因は、テストの問題を診断します。 デバイスの基本的なテストと WDK に含まれているその他のテストは、WDTF ベースのテストの例を示します。 これらのテストについては、次を参照してください。[を選択し、デバイスの基本的なテストを構成する方法](https://docs.microsoft.com/windows-hardware/drivers)します。

サポートを提供する WDTF [WPP ソフトウェア トレース](https://docs.microsoft.com/windows-hardware/drivers/devtest/wpp-software-tracing)します。 WDTF のすべてのオブジェクトは、実行中にトレース情報を生成します。 など、WDK のツールを使用して、トレース情報を読み取れる[traceview で](https://docs.microsoft.com/windows-hardware/drivers/devtest/using-traceview)します。

## <a name="in-this-section"></a>このセクションの内容


-   [WDTF オブジェクトのログ記録](logging-and-tracing.md)
-   [有効化と WDTF トレースの表示](viewing-wdtf-traces.md)
-   [WDTF ベースのテストを実行している問題を診断します。](diagnosing-problems-running-wdtf-based-tests.md)

 

 




