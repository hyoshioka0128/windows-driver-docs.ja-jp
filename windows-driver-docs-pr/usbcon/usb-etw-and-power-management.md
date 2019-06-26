---
Description: このトピックでは、簡単な ETW を使用して、USB のセレクティブを確認する方法の概要は中断状態と Windows PowerCfg ユーティリティを使用してシステムのエネルギー効率の問題を識別します。
title: USB ETW と電源管理
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7344397f386329b57b44b134df13a776a40d2f7f
ms.sourcegitcommit: f663c383886d87ea762e419963ff427500cc5042
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67391766"
---
# <a name="usb-etw-and-power-management"></a>USB ETW と電源管理


このトピックでは、簡単な ETW を使用して、USB のセレクティブを確認する方法の概要は中断状態と Windows PowerCfg ユーティリティを使用してシステムのエネルギー効率の問題を識別します。

USB デバイスのドライバーをサポートしている場合[USB セレクティブ サスペンド](usb-selective-suspend.md)デバイスがアイドル状態のときに、USB デバイスを無効にできますが。 デバイスがアイドル状態でなくなったときに、システムは、デバイスのスリープ状態を解除し、通常の操作を再開します。 システムがアイドル状態と、すべての USB デバイスが中断された、プロセッサ アクティビティは不要であり、プロセッサが低電力状態になるためです。 正しく選択的実装を中断大幅な省電力および増加のバッテリ寿命をモバイル システム向けに発生することができます。

USB の ETW を使用して、USB デバイスを確認し、選択的に正常に移動するかどうかを検証するには、そのドライバーが中断します。 システムの製造元、IT プロフェッショナルは、またはハードウェア開発者であるかどうかは、あなたは USB デバイスを検査することをお勧めおよびドライバーを正しくサポートするオプションを選択することを確認するが、デバイスをエンドユーザーに提供することを中断します。

システムのエネルギー効率性の問題を特定するために、Windows 7、Windows PowerCfg ユーティリティを拡張します。 PowerCfg は、電源ポリシーの列挙型と構成可能にする Windows に含まれているコマンド ライン ユーティリティです。 PowerCfg エネルギー効率の問題を判断するための機能強化を使用して実行された、 **-エネルギー**パラメーター。 これらの拡張機能では、PowerCfg エネルギー効率の一般的な問題のシステムを検査し、検出された問題を含む HTML レポートの生成を有効にします。

PowerCfg では、さまざまなエネルギー効率が USB デバイス、過剰なプロセッサ使用率、増加のタイマー精度、非効率な電源ポリシーの設定、およびバッテリ容量低下して選択的の非効率的な使用を含む、問題を中断を検出します。 PowerCfg では、さまざまなレベルのサーバーの問題 (エラー)、軽微な問題 (警告) などの問題を識別します。

詳細については、Windows 電源管理と、PowerCfg ツールは、次を参照してください。 [Powercfg のコマンドライン オプション](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-vista/cc748940(v=ws.10))と[システムのエネルギー効率の評価に PowerCfg を使用して](https://docs.microsoft.com/previous-versions/windows/hardware/download/dn550976(v=vs.85))します。

## <a name="related-topics"></a>関連トピック
[Windows のイベント トレースは USB](usb-event-tracing-for-windows.md)  



