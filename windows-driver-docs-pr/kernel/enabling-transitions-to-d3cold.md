---
title: D3cold への遷移の有効化
description: すべてのバージョンの Windows では、コンピューターのスリープ中にデバイスを D3cold にすることができます (システムの低電力状態 S1 ~ S4)。
ms.assetid: C2C6166D-8269-4FCE-81A8-B350626052D4
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: a60efd60e9295eb69d16bbef9adc17ca87f340df
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72836766"
---
# <a name="enabling-transitions-to-d3cold"></a>D3cold への遷移の有効化


すべてのバージョンの Windows では、コンピューターのスリープ中にデバイスを D3cold にすることができます (システムの低電力状態 S1 ~ S4)。 コンピューターが S0 を終了する前に、関数ドライバー、バスドライバー、およびフィルタードライバーが連携して、デバイスを D3hot に移動します。 コンピューターが低電力の Sx 状態になると、この移行は、デバイスを D3hot から D3cold に移動する副作用になります。

Windows 8 以降では、コンピューターが S0 のままになっている間に、デバイスは D3cold を開始して終了することができます。 デバイスの電源ポリシー所有者 (PPO) であるドライバーは、D3cold への移行を有効または無効にすることができます。 ドライバーは、デバイスが必要に応じて D3cold から復帰し、D0 への移行後に通常の操作を再開しない限り、デバイスが D3cold に入ることを許可しないでください。

デバイスは D3 に入ったときに、最初に D3 の D3hot の下位部分に入ります。 D3hot から、デバイスは D0 または D3cold のいずれかを入力できます。 Wake イベントまたは i/o 要求に応答して、デバイスは D3hot から D0 に入ります。 それ以外の場合は、デバイスが D3hot に残っているか、D3hot から D3cold に移動する可能性があります。 これらの遷移の詳細については、デバイスの電源状態の[図](device-power-states.md#power-state-diagram)「[デバイスの電源](device-power-states.md)状態」を参照してください。

ドライバーは、デバイスの D3hot から D3cold への移行を開始しません。 この移行は、このデバイスと共通の電源を共有する他のすべてのデバイスが D3hot にあり、D3cold に入る準備が整ったときに発生します。 これらのデバイスの最後に D3hot が入力されると、基になるバスドライバーとシステムファームウェアによって電源が削除され、デバイスが D3cold に移行します。

デバイスの PPO ドライバーは、デバイスの D3hot から D3cold への移行を有効にするかどうかをオペレーティングシステムに伝えます。 ドライバーは、デバイスをインストールする INF ファイルにこの情報を提供できます。また、ドライバーは実行時に[*SetD3ColdSupport*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-set_d3cold_support)ルーチンを呼び出して、デバイスの D3cold への移行を動的に有効または無効にすることができます。 詳細については、「 [USING GUID\_D3COLD\_SUPPORT\_Interface Driver interface](using-guid-d3cold-support-interface.md)」を参照してください。

デバイスで D3cold を入力できるようにすることで、ドライバーは次の動作を保証します。

-   コンピューターが S0 のままになっている場合、デバイスは D3hot から D3cold への移行を許容できます。
-   デバイスは、D3cold から D0 に戻ると正常に動作します。

いずれかの要件を満たしていないデバイスは、D3cold を入力した後に、コンピューターが再起動されるか、またはスリープ状態になるまで使用できません。 デバイスが、入力された省電力の Dx 状態からウェイクアップイベントを通知できる必要がある場合、D3cold へのエントリを有効にすることはできません。ただし、デバイスのスリープ解除信号が D3cold で動作することがドライバーによって特定される場合を除きます。

デバイスを D3cold に配置することは、必ずしもデバイスの電源のすべてのソースが削除されていることを意味するわけではありません。これは、バス経由でデバイスへの通信を許可する電力の供給元だけが失われることを意味します。 デバイスは、スリープ状態のイベントをプロセッサに通知するために十分な電力を描画できる可能性があります。 たとえば、メインの電源が取り外されているイーサネットネットワークインターフェイスカード (NIC) は、イーサネットケーブルから電力を引くことができます。

D3cold は、デバイスとの通信にバスを使用できない状態であるため、ドライバーはデバイスを D3cold に直接入れることができません。 代わりに、ドライバーはまず[**PoRequestPowerIrp**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-porequestpowerirp)ルーチンを呼び出して、D3 の電源 IRP を要求します ( [**IRP\_\_に\_設定**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-set-power)され、ターゲット状態 = **PowerDeviceD3**) は、デバイスを D0 から D3hot に移動します。 D3hot を入力した後、デバイスが D3hot から D3cold に移動する場合と、ない場合があります。 バスが取り外された場合にのみ、デバイスは D3cold に入ります。これは、親バスドライバーがバスをオフにした場合、またはシステムファームウェアによってハードウェアプラットフォームのセクションに電源がオフになった場合に発生します。

 

 




