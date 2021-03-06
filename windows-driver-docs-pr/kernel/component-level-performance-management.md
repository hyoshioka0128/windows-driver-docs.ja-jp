---
title: コンポーネント レベルのパフォーマンス状態の管理
description: Windows 10 以降では、電源管理フレームワーク (PoFx) は、デバイス内の個々 のコンポーネントを個別に調整可能なパフォーマンスの状態の 1 つまたは複数のセットを定義するためのドライバーを使用できます。
ms.assetid: D5341D6D-7C71-43CB-9C70-7E939B32C33F
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 9df895638ec56c6c814fe2586e7a55df24bc5a56
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67377220"
---
# <a name="component-level-performance-state-management"></a>コンポーネント レベルのパフォーマンス状態の管理


Windows 10 以降では、電源管理フレームワーク (PoFx) は、デバイス内の個々 のコンポーネントを個別に調整可能なパフォーマンスの状態の 1 つまたは複数のセットを定義するためのドライバーを使用できます。 このドライバーは、パフォーマンスの状態を使ってコンポーネントのワークロードを調整し、現在のニーズに最適なパフォーマンスを提供します。

## <a name="overview-of-performance-states"></a>パフォーマンス状態の概要


Windows 8 および Windows 8.1 では、PoFx は、コンポーネント レベルの電源を節約するため、電力および特定の F 状態が入力されると、クロックのレール ゲート アイドル状態の状態 (F 状態) を提供します。 このモデルでは、電力を節約しますコンポーネント (F0 以外)、アイドル状態には、電力使用量を最適化したり、コンポーネントがアクティブなときにパフォーマンスのニーズに対して分散の任意のメカニズムは提供されません。 場合でも、コンポーネント (F0) でアクティブでは、要求をサービスするが必要し、しない可能性、デバイスの完全なパフォーマンス。 たとえば、グラフィックス カードがのみ、点滅するカーソルを更新する必要があり、この完全なパフォーマンスを必要はありません。

変数のパフォーマンス状態の現在のニーズに合わせてのに十分なパフォーマンスを提供するデバイスのコンポーネントをスロットルするドライバーを許可することでこの問題に対処します。 Windows 8 および Windows 8.1 では、コンポーネントは、パフォーマンスの状態をサポートしている場合各ドライバーする必要があります、ドライバーの内部に独自のパフォーマンス状態の選択アルゴリズムを実装し、必要な場合、通知、プラットフォーム拡張機能プラグイン (PEP)、独自の方法。 PEP は、チップ (SoC) モジュールにプロセッサまたはシステムの特定の製品ラインに固有の電源管理タスクを実行するソフトウェア コンポーネントです。 ドライバー固有の独自のパフォーマンスの状態ソリューションには、PEP に密結合のデメリットがあり、簡単にデバッグすることはできません。

PoFx 以降 Windows 10 では、パフォーマンスの状態管理の API を提供します。 この API では、2 つの主な目標があります。

-   デバイス ドライバー、PEP のパフォーマンス、適切に対処するために、PEP のパフォーマンス状態の変更を通知する手段を提供します。
-   各ドライバーのカスタム プラグインをしなくても、OS のログと Windows パフォーマンス アナライザー (WPA) では、分析のパフォーマンス状態の変更を通知するドライバーの標準的な方法を提供します。

## <a name="introduction-to-the-pofx-api-for-component-level-performance-states"></a>コンポーネント レベルのパフォーマンス状態の PoFX API の概要


PoFx は、次の種類の各コンポーネントのパフォーマンス状態を定義するデバイスを有効にします。

-   頻度 (Hz で測定)、帯域幅 (1 秒あたりのビット単位) または非透過のインデックス番号の単位で状態の不連続の数。
-   最小値と最大値の間の状態の継続的な配布します。

パフォーマンスの状態は、セットにまとめられているし、コンポーネントごとに登録されます。 セット内のパフォーマンスの状態は 1 ずつ増やす必要があります。 ほとんどのドライバーは、コンポーネントごとのパフォーマンス状態の 1 つのセットを定義する必要があります。 たとえば、ドライバーは、コンポーネントのクロック周波数を制御するためのパフォーマンス状態の 1 つのセットを定義する可能性があります。 ただし、一部のドライバーは、コンポーネントのパフォーマンス状態の複数のディメンションを制御する設定は、複数のパフォーマンス状態を定義する必要があります。 たとえば、ドライバーでは、クロック周波数とバスの帯域幅を制御するためのパフォーマンス状態の 2 つのセットを定義します。

PoFx によるパフォーマンスの状態管理のため、デバイスのコンポーネントを登録するには、ドライバーには、一般的な手順が次に示します。

1.  ドライバーは、PoFx によって管理されるデバイスのコンポーネントを登録します。 詳細については、次を参照してください。[コンポーネント レベルの電源管理](component-level-power-management.md)します。

2.  ドライバーは、呼び出すことによってパフォーマンスの状態のサポートを登録[ **PoFxRegisterComponentPerfStates**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-pofxregistercomponentperfstates)します。 登録の呼び出しの一環として、ドライバー自体が特定のコンポーネントのパフォーマンスの状態を定義するかプラットフォーム拡張機能にプラグインを代わりに定義するには、(PEP) を延期します。

    デバイス ドライバー、または PEP は、コンポーネント、パフォーマンスの状態 (不連続または範囲に基づく) の種類と値の詳細と実際のパフォーマンスの数ごとのパフォーマンス状態のセットの数など、パフォーマンスの状態のナレッジを保持する必要があります。示されます。 PEP がパフォーマンスの状態をサポートしていない場合、ドライバーをまだ PoFx のパフォーマンス状態のサポートについては登録およびログと分析では、Windows パフォーマンス アナライザー (WPA) のパフォーマンス状態の変更の OS に通知。

    正常に完了すると、いずれの場合も[ **PoFxRegisterComponentPerfStates**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-pofxregistercomponentperfstates)、ドライバーは、 [ **PO\_FX\_コンポーネント\_PERF\_情報**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/ns-wdm-_po_fx_component_perf_info)登録済みのパフォーマンス状態のセットを含む構造体。

3.  ドライバーは、コンポーネントは、パフォーマンスの状態を変更する必要がありますを決定したら、それを呼び出す[ **PoFxIssueComponentPerfStateChange** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-pofxissuecomponentperfstatechange)または[ **PoFxIssueComponentPerfStateChangeMultiple**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-pofxissuecomponentperfstatechangemultiple)します。 PoFx 呼び出すドライバーの[ **ComponentPerfStateCallback** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-po_fx_component_perf_state_callback)ルーチン パフォーマンス状態の変更が完了するとします。

4.  ドライバーを活用して、 [ **ComponentPerfStateCallback** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-po_fx_component_perf_state_callback)日常的なかどうか、PEP が成功したか、パフォーマンスの状態の変更を拒否します。 PEP に変更が成功した場合、ドライバーは、その観点からパフォーマンスの状態を変更するために必要な作業を実行します。 PEP には、変更が拒否されている場合、何もしないか、同じまたは別のパフォーマンスが状態を使用して要求を再試行するドライバーを引き起こすことができます。

## <a name="related-topics"></a>関連トピック
[デバイスの電源管理リファレンス](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/index)  



