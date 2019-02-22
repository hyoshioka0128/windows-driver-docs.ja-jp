---
title: Static Driver Verifier のトラブルシューティングに関する推奨事項
description: Static Driver Verifier のトラブルシューティングに関する推奨事項
ms.assetid: 14c39437-12ca-4938-93bb-79bbcb192de2
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 67beefeaa8b9314da081fec011400c2d76402d23
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56550564"
---
# <a name="recommendations-for-troubleshooting-static-driver-verifier"></a>Static Driver Verifier のトラブルシューティングに関する推奨事項


Static Driver Verifier (SDV) で、ドライバーのソース コードとタイムアウト、停止、または Spaceout SDV レポートを実行すると、次の操作を試してください。

-   次の推奨事項には、SDV の構成設定に変更が必要です。 静的ドライバー Verfier で直接構成設定を設定することができます、**構成**] タブで、[リソース、または、[静的ドライバー検証ツールのオプション ファイル](static-driver-verifier-options-file.md)、Sdv defaults.xml します。 既定のオプションのファイルはドライバー モデルに固有でありで見つかる、\\ツール\\sdv\\データ\\モデル\\モデルが WDM、WDF、NDIS、または Storport、ディレクトリ。
    1.  コンピューターがマルチコア プロセッサの場合は、1 を確認中に使用されるスレッドの数を減らします。 リソース グループに、**構成** タブで、ドロップダウン リストから 1 を選択します。 SDV の既定のファイルでは、SDV の値を変更します。\_SlamConfig\_NumberOfTheads を 1 にします。
    2.  SDV は、タイムアウトを報告する場合は、タイムアウト制限を増やします。 この値は、SDV は、ルールの検証が費やした時間の量を制限します。 既定値は、50 分 (3000 秒) です。 リソース グループに、**構成** タブで、変更することで設定を調整することができます、**最長時間**(分)。 オプション ファイルでは、SDV を変更できます\_SlamConfig\_タイムアウト値。 最小値は 10(Sec) で、最大値は 86400(Sec) です。 SDV の値をダブルクリックするなど、\_SlamConfig\_6000 にタイムアウトします。
-   問題の解決のこれらの方法でも解決しない場合、すべてをまとめてに適用することをお試しください。

**注**これらの手法の実行を実際の期間は長くなりますもが簡単に有用な結果をそのジョブの完了の SDV の (渡すまたは参加解除) します。
