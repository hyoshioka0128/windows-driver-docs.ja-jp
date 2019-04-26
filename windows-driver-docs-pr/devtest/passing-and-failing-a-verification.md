---
title: 検証の成功と失敗
description: 検証の成功と失敗
ms.assetid: 2639358b-eb6a-49b7-b23a-877a452917dc
keywords:
- 静的ドライバー検証ツールの WDK、検証結果
- StaticDV WDK、検証結果
- SDV の WDK、検証結果
- WDK Static Driver Verifier の結果
- 渡された検証 WDK Static Driver Verifier
- WDK Static Driver Verifier を確認できませんでした。
- 結果が不確定検証 WDK Static Driver Verifier
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: a840d3ddf31d7fa1ee33a997ce09e196eb6d9d3a
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63356345"
---
# <a name="passing-and-failing-a-verification"></a>検証の成功と失敗


ルールの SDV の検証では、次の 3 つの基本的な結果があります。

-   ドライバー*渡します*検証します。

-   ドライバー*失敗*検証します。

-   結果は*結果が不確定*します。

これらの結果に基づいて何らかの結論を描画する前にする必要があります、各結果を理解し、それに伴う多くの要件に注意してください。 ドライバーの最終的なまたは完全な評価結果を判断する必要があります。

### <a name="span-idverificationresultsspanspan-idverificationresultsspanverification-results"></a><span id="verification_results"></span><span id="VERIFICATION_RESULTS"></span>検証結果

ドライバー*渡します*SDV 検証ときに、ドライバーのすべての関連する実行パスの調査後に次のようにコードを SDV[検証エンジン](verification-engine.md)ドライバーが選択されたルールに違反したことを証明することはできません検証します。

ドライバー*失敗*SDV 検証エンジン ドライバーがルールを 1 回以上違反することを証明するときに検証します。 違反と呼ばれる、*の参加を解除*します。 SDV のレポートのかどうか、ドライバーは、ルールを複数回違反、*複数欠陥*します。

検証が*結果が不確定*タイムアウトのため完了前に終了した場合 (、**タイムアウト**結果) またはメモリが不足している (、 **Spaceout**結果)、または SDV成功か失敗した結論に到達できませんでした (、**不明な**結果)。 また、SDV をそのタスクの完了を妨げる内部ツールのエラーが発生した可能性があります。 (結果の詳細については、次を参照してください[静的ドライバー検証結果を解釈する](interpreting-static-driver-verifier-results.md)。)。

ときに、ルールは適用されません、ドライバーをなど、ドライバーを行わなかった場合、ルールを確認するデバイス ドライバー インターフェイスの使用、SDV は、規則があることを報告**該当なし**します。

 

 





