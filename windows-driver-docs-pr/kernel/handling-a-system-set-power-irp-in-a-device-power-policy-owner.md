---
title: デバイス電源ポリシー所有者のシステム電源設定 IRP の処理
description: デバイス電源ポリシー所有者のシステム電源設定 IRP の処理
ms.assetid: f6206455-142b-4f3f-ae5a-d8e79386bce3
keywords:
- セット power Irp WDK の電源管理
- デバイスの電源ポリシー所有者 WDK カーネル
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: a8e8cb45d24f56a788d75a8c91cca222847fae21
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63359830"
---
# <a name="handling-a-system-set-power-irp-in-a-device-power-policy-owner"></a>デバイス電源ポリシー所有者のシステム電源設定 IRP の処理





システムへの応答セット power の IRP、[電源ポリシー所有者](managing-device-power-policy.md)デバイス スタックは、適切なデバイスの電源状態にそのデバイス スタックを配置する責任を負います。

デバイスの電源ポリシー所有者は受信すると、一般的な規則として、 [ **IRP\_MN\_設定\_POWER** ](https://msdn.microsoft.com/library/windows/hardware/ff551744)のシステム電源の状態をシステムを渡すことによって応答する必要がありますデバイス スタック IRP を出力を設定します。 デバイスの電源ポリシー所有者は、デバイス スタックを送信することによって応答も**IRP\_MN\_設定\_POWER**で対応するデバイスの電源状態の[ *IoCompletion* ](https://msdn.microsoft.com/library/windows/hardware/ff548354)ルーチン。 スタック内のすべてのドライバーは、デバイスを完了した後にセット power IRP では、デバイスの電源ポリシーの所有者が完了すると、システム IRP の出力を設定します。

ただし、システム再開パフォーマンスを向上させるには、デバイス電源所有者子デバイスがないデバイスの必要がありますを使用して、別のアプローチに戻るにシステムにかかる時間を短縮する[作業状態 S0](system-working-state-s0.md)から、 [スリープ状態](system-sleeping-states.md)します。 システムへの応答でこの例では、作業状態 S0、システムが返すセット power IRP デバイス電源ポリシー所有者は、次の一連の操作を実行する必要があります。

1.  受信した後、 **IRP\_MN\_設定\_POWER** IRP がドライバーの S0 システム電源の状態の[DispatchPower ルーチン](dispatchpower-routines.md)、設定、 *IoCompletion* IRP を渡します IRP が下位のスタックのルーチンです。

2.  *IoCompletion*手順 (1) での日常的なセットを要求、 **IRP\_MN\_設定\_POWER**対応するデバイスの電源状態の IRP し、すぐにシステムの完了 IRP の出力を設定します。 デバイスのセットの電源のドライバーを待ちませんする必要があります、システムが完了する前に完了する Irp セット power IRP。 *IoCompletion*下位レベルのすべてのドライバーは、システムで完了した後、ルーチンが実行されるセット power IRP とセット power IRP が渡される、システム、ドライバーの機能のデバイス オブジェクト (FDO) に戻します。

3.  必要なデバイスに固有の初期化を実行します。

4.  デバイスの完了手順 (2) で送信されたセット power IRP します。

5.  デバイスで起動したときにキューに配置された I/O 要求を処理する[デバイスがスリープ状態](device-sleeping-states.md)します。

カーネルの電源マネージャは、限られた IRP ディスパッチ キューを備え、システムの稼働状態 S0 を戻り値のシステムのすべてのデバイスをすばやく通知する必要があります。 システムを完了していないドライバー セット power IRP 可能な限り早く防止他のデバイス、システム セット power IRP は、システム電源の状態遷移中に、システムの全体的なパフォーマンスに悪影響を与えることができます。

システムの処理の詳細についてはセット power Irp では、以下でご覧ください。

[適切なデバイスの電源状態を判断します。](determining-the-correct-device-power-state.md)

[システムのセット Power IRP への応答でデバイスのセット Power IRP を送信します。](sending-a-device-set-power-irp-in-response-to-a-system-set-power-irp.md)

 

 




