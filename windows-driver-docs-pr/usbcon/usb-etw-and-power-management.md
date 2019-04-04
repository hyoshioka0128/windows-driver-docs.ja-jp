---
Description: This topic provides a brief overview about using ETW to examine USB selective suspend state and identifying system energy efficiency problems by using the Windows PowerCfg utility.
title: USB ETW および電源管理
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: e5272a329a7c42a29921e40e2d5196e78b8d2b0f
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56530804"
---
# <a name="usb-etw-and-power-management"></a>USB ETW および電源管理


このトピックでは、簡単な ETW を使用して、USB のセレクティブを確認する方法の概要は中断状態と Windows PowerCfg ユーティリティを使用してシステムのエネルギー効率の問題を識別します。

USB デバイスのドライバーをサポートしている場合[USB セレクティブ サスペンド](usb-selective-suspend.md)デバイスがアイドル状態のときに、USB デバイスを無効にできますが。 デバイスがアイドル状態でなくなったときに、システムは、デバイスのスリープ状態を解除し、通常の操作を再開します。 システムがアイドル状態と、すべての USB デバイスが中断された、プロセッサ アクティビティは不要であり、プロセッサが低電力状態になるためです。 正しく選択的実装を中断大幅な省電力および増加のバッテリ寿命をモバイル システム向けに発生することができます。

USB の ETW を使用して、USB デバイスを確認し、選択的に正常に移動するかどうかを検証するには、そのドライバーが中断します。 システムの製造元、IT プロフェッショナルは、またはハードウェア開発者であるかどうかは、あなたは USB デバイスを検査することをお勧めおよびドライバーを正しくサポートするオプションを選択することを確認するが、デバイスをエンドユーザーに提供することを中断します。

システムのエネルギー効率性の問題を特定するために、Windows 7、Windows PowerCfg ユーティリティを拡張します。 PowerCfg は、電源ポリシーの列挙型と構成可能にする Windows に含まれているコマンド ライン ユーティリティです。 PowerCfg エネルギー効率の問題を判断するための機能強化を使用して実行された、 **-エネルギー**パラメーター。 これらの拡張機能では、PowerCfg エネルギー効率の一般的な問題のシステムを検査し、検出された問題を含む HTML レポートの生成を有効にします。

PowerCfg では、さまざまなエネルギー効率が USB デバイス、過剰なプロセッサ使用率、増加のタイマー精度、非効率な電源ポリシーの設定、およびバッテリ容量低下して選択的の非効率的な使用を含む、問題を中断を検出します。 PowerCfg では、さまざまなレベルのサーバーの問題 (エラー)、軽微な問題 (警告) などの問題を識別します。

詳細については、Windows 電源管理と、PowerCfg ツールは、[Powercfg のコマンドライン オプション](https://technet.microsoft.com/library/cc748940(WS.10).aspx)と[システムのエネルギー効率の評価に PowerCfg を使用して](https://msdn.microsoft.com/library/windows/hardware/gg463250.aspx)を参照してください。

## <a name="related-topics"></a>関連トピック
[Windows のイベント トレースは USB](usb-event-tracing-for-windows.md)  



