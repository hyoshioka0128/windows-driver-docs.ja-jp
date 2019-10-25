---
title: コンポーネント レベルのパフォーマンス状態の管理
description: Windows 10 以降、電源管理フレームワーク (PoFx) を使用すると、ドライバーは、デバイス内の個々のコンポーネントに対して個別に調整可能なパフォーマンス状態を1つ以上定義できます。
ms.assetid: D5341D6D-7C71-43CB-9C70-7E939B32C33F
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 01b7a194aee6e8c97cfd4462dc5ddaa762b3b42a
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72837065"
---
# <a name="component-level-performance-state-management"></a>コンポーネント レベルのパフォーマンス状態の管理


Windows 10 以降、電源管理フレームワーク (PoFx) を使用すると、ドライバーは、デバイス内の個々のコンポーネントに対して個別に調整可能なパフォーマンス状態を1つ以上定義できます。 このドライバーは、パフォーマンスの状態を使ってコンポーネントのワークロードを調整し、現在のニーズに最適なパフォーマンスを提供します。

## <a name="overview-of-performance-states"></a>パフォーマンスの状態の概要


Windows 8 と Windows 8.1 では、PoFx は、特定の F 状態が入力されたときに、電源とクロックレールによって、コンポーネントレベルの電力節約のアイドル状態 (F 状態) を提供します。 このモデルは、コンポーネントがアイドル状態 (非 F0) のときに電力を節約しますが、コンポーネントがアクティブなときに電力使用量を最適化したり、パフォーマンスのニーズに合わせたりするためのメカニズムを備えていません。 コンポーネントがアクティブ (F0) であり、要求を処理している場合でも、デバイスの完全なパフォーマンスを必要としない可能性があります。 たとえば、グラフィックスカードでは、点滅するカーソルだけを更新する必要があり、完全なパフォーマンスは必要ない場合があります。

可変パフォーマンス状態: 現在のニーズに十分なパフォーマンスを提供するようにドライバーがデバイスコンポーネントを調整できるようにすることで、この問題に対処します。 Windows 8 および Windows 8.1 では、コンポーネントがパフォーマンス状態をサポートしている場合、各ドライバーは、ドライバー内部の独自のパフォーマンス状態選択アルゴリズムを実装する必要があります。また、必要に応じて、プラットフォーム拡張機能プラグイン (PEP) に独自のものを通知する必要があります。ながら. PEP は、チップ (SoC) モジュール上の特定の製品ラインプロセッサまたはシステムに固有の電源管理タスクを実行するソフトウェアコンポーネントです。 ドライバー固有の独自のパフォーマンス状態ソリューションには、PEP と密結合されるという欠点があり、簡単にデバッグすることはできません。

Windows 10 以降では、PoFx はパフォーマンス状態管理のための API を提供します。 この API には、主に次の2つの目標があります。

-   デバイスドライバーは、パフォーマンスの状態の変化について PEP に通知する標準的な方法を提供し、PEP が適切なアクションを実行できるようにします。
-   ドライバーは、ドライバーごとにカスタムプラグインを用意することなく、Windows Performance Analyzer (WPA) でのログ記録と分析のために、パフォーマンスの状態の変化を OS に通知するための標準的な方法を提供します。

## <a name="introduction-to-the-pofx-api-for-component-level-performance-states"></a>コンポーネントレベルのパフォーマンス状態に関する PoFX API の概要


PoFx を使用すると、デバイスは、各コンポーネントに対して次の種類のパフォーマンス状態を定義できます。

-   周波数の単位 (Hz 単位)、帯域幅 (ビット/秒単位)、または不透明なインデックス番号の個別の状態の数。
-   最小値と最大値の間の状態の連続分布。

パフォーマンスの状態は、セットごとにまとめられ、コンポーネントごとに登録されます。 セット内のパフォーマンスの状態は、単調に増加する必要があります。 ほとんどのドライバーでは、コンポーネントごとにパフォーマンス状態の1つのセットを定義することが想定されています。 たとえば、1つのドライバーで1つのパフォーマンス状態を定義して、コンポーネントのクロック周波数を制御できます。 ただし、一部のドライバーでは、コンポーネントのパフォーマンス状態の複数の次元を制御するために複数のパフォーマンス状態セットを定義する必要がある場合があります。 たとえば、ドライバーでは、クロック周波数とバス帯域幅を制御するために、2つのパフォーマンス状態のセットを定義できます。

PoFx によるパフォーマンス状態管理のためにデバイスコンポーネントを登録するには、次の一般的な手順に従います。

1.  ドライバーは、PoFx によって管理されるようにデバイスコンポーネントを登録します。 詳細については、「[コンポーネントレベルの電源管理](component-level-power-management.md)」を参照してください。

2.  このドライバーは、 [**Pofxregistercomponentperfstates**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-pofxregistercomponentperfstates)を呼び出すことによって、パフォーマンス状態のサポートを登録します。 登録呼び出しの一部として、ドライバーは、特定のコンポーネントのパフォーマンス状態を定義するか、プラットフォーム拡張機能プラグイン (PEP) に従って代わりに定義することができます。

    デバイスドライバーまたは PEP は、パフォーマンス状態の情報を保持する必要があります。これには、コンポーネントごとのパフォーマンス状態セットの数、パフォーマンス状態の種類 (不連続または範囲ベース)、および実際のパフォーマンスの値と数の詳細が含まれます。米. PEP でパフォーマンス状態がサポートされていない場合でも、ドライバーは PoFx によるパフォーマンス状態のサポートに登録し、Windows Performance Analyzer (WPA) でログと分析のためにパフォーマンスの状態の変化を OS に通知する場合があります。

    どちらの場合でも、 [**Pofxregistercomponentperfstates**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-pofxregistercomponentperfstates)が正常に完了すると、ドライバーには、登録されているパフォーマンス状態セットを含む、 [ **\_FX\_コンポーネント\_PERF\_INFO**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_po_fx_component_perf_info)構造体が含まれます。

3.  ドライバーは、コンポーネントのパフォーマンス状態を変更する必要があると判断した場合、 [**PoFxIssueComponentPerfStateChange**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-pofxissuecomponentperfstatechange)または[**PoFxIssueComponentPerfStateChangeMultiple**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-pofxissuecomponentperfstatechangemultiple)を呼び出します。 パフォーマンス状態の変更が完了すると、PoFx はドライバーによって提供される[**ComponentPerfStateCallback**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-po_fx_component_perf_state_callback)ルーチンを呼び出します。

4.  このドライバーは、PEP がパフォーマンス状態の変化を成功したか拒否したかにかかわらず、 [**ComponentPerfStateCallback**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-po_fx_component_perf_state_callback)ルーチンによって通知されます。 PEP によって変更が成功した場合、ドライバーは、パフォーマンスの状態をパースペクティブから変更するために必要なすべての作業を実行します。 PEP で変更が拒否された場合、ドライバーは何も実行しないか、同じまたは代替のパフォーマンス状態でもう一度要求を再試行することができます。

## <a name="related-topics"></a>関連トピック
[デバイスの電源管理のリファレンス](https://docs.microsoft.com/windows-hardware/drivers/ddi/index)  



