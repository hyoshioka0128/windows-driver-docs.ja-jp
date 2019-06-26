---
title: ネットワーク アダプターのデバイス電源状態
description: ネットワーク アダプターのデバイス電源状態
ms.assetid: 969aadc9-e797-4a07-9714-8c2c5a6357da
keywords:
- Nic の WDK ネットワーク、電源の状態
- ネットワーク インターフェイス カードの WDK ネットワーク、電源の状態
- デバイスの電源状態が WDK ネットワーク
- WDK ネットワークの状態を電源します。
- WDK の NDIS ミニポートの電源管理、デバイスの電源の状態します。
- WDK のネットワークの状態遷移の電源
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 800da6faa1c0f9a20b9c878613119c7c1e105ff3
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67381388"
---
# <a name="device-power-states-for-network-adapters"></a>ネットワーク アダプターのデバイス電源状態





ネットワーク アダプターのデバイスの電源状態では、ネットワーク アダプターのレベルの電力消費量とコンピューティングのアクティビティについて説明します。

これには 4 つのデバイスの電源状態があります。D0、D1、d2 に切り替わり、および D3 します。 D0 は、highest-powered 状態です。 D1、d2 に切り替わり、および D3 は、スリープ状態です。 D3 は D3hot と D3cold に分割されます。

状態の数が電力消費量に関連する反比例: それ以上の状態を使用して、電力を節約します。 電源は、D3 状態のネットワーク アダプターからは完全に解消される可能性があります。

デバイスの状態の詳細な説明は、次のトピックを参照してください。

* [デバイスの電源の状態](https://docs.microsoft.com/windows-hardware/drivers/kernel/device-power-states)
* [デバイスの動作状態 D0](https://docs.microsoft.com/windows-hardware/drivers/kernel/device-working-state-d0)
* [デバイスの低電力状態](https://docs.microsoft.com/windows-hardware/drivers/kernel/device-sleeping-states)
* [デバイスの電源状態の必要なサポート](https://docs.microsoft.com/windows-hardware/drivers/kernel/required-support-for-device-power-states)

**注**  NDIS プロセスの電源管理の Irp では、NDIS ドライバーがないです。

 

ネットワーク アダプターのデバイスの電源の状態は次のとおりです。

### <a href="" id="d0"></a>デバイスの動作状態 D0

この電源状態の説明は、すべてのデバイスで[デバイスの操作状態 D0](https://docs.microsoft.com/windows-hardware/drivers/kernel/device-working-state-d0)します。 ネットワーク アダプターおよびミニポート ドライバー。

<a href="" id="power-consumption"></a>電力消費量  
ネットワーク アダプターでは、完全に供給し、配信の完全な機能とパフォーマンスが。

<a href="" id="device-context"></a>デバイス コンテキスト  
ハードウェア デバイス コンテキストは、ネットワーク アダプターのミニポート ドライバーまたはその両方によって管理されます。

<a href="" id="miniport-driver-and-network-adapter-behavior"></a>ミニポート ドライバーとネットワーク アダプターの動作  
ネットワーク アダプターが接続されているネットワークの要件に完全に準拠します。 低電力要件により、ミニポート ドライバーとネットワーク アダプターの操作を制限することがありません。

<a href="" id="restore-time"></a>復元時間  
適用できません。

### <a href="" id="d1"></a>デバイスの電源状態 D1

この電源状態の説明は、すべてのデバイスで[デバイス低電力状態](https://docs.microsoft.com/windows-hardware/drivers/kernel/device-sleeping-states)します。 ネットワーク アダプターおよびミニポート ドライバー。

<a href="" id="power-consumption"></a>電力消費量  
この状態は、highest-powered スリープ状態です。 電力消費は、状態とより大きいまたは D2 の状態と等しい D0 でよりも短くなっています。

<a href="" id="device-context"></a>デバイス コンテキスト  
ミニポート ドライバーでは、失われる可能性がある任意のハードウェア デバイス コンテキストを保持する必要があります。 D0 状態に戻ると、デバイス、ミニポート ドライバーはこのようなコンテキストを復元する必要があります。

<a href="" id="miniport-driver-and-network-adapter-behavior"></a>ミニポート ドライバーとネットワーク アダプターの動作  
ミニポート ドライバーでは、プロトコル ドライバーから送信要求を受信しません。 NDIS かスリープ状態へのネットワーク アダプターの遷移のバインドのプロトコル ドライバーに通知または、NDIS がプロトコル ドライバーからの転送要求を無効にプロトコル ドライバーが古いドライバーは、電源管理に対応している場合。 ただし、ミニポート ドライバーは、この省電力状態にあるときに、送信要求を受け取ることはケースを処理できる必要があります。 この場合、ミニポート ドライバーでは、すべての転送要求は失敗します。

ミニポート ドライバーは示しませんのパケットをこの状態になっているネットワーク アダプターが表示される可能性があります。

ネットワーク アダプターでは、割り込みを生成しません。 ただし、ミニポート ドライバーできる必要があります、割り込みを処理するため、バスの共有の割り込みを生成できませんできます。

<a href="" id="restore-time"></a>復元時間  
ネットワーク アダプターを D0 状態に復元する特定は、ネットワーク アダプターが D2 の状態を必要とするよりも小さい。

### <a href="" id="d2"></a>デバイスの電源状態 D2

この電源状態の説明は、すべてのデバイスで[デバイス低電力状態](https://docs.microsoft.com/windows-hardware/drivers/kernel/device-sleeping-states)します。 ネットワーク アダプターおよびミニポート ドライバー。

<a href="" id="power-consumption"></a>電力消費量  
中間のスリープ状態です。 電力消費は、状態とより大きいまたは D3 状態と等しい D1 でよりも短くなっています。

<a href="" id="device-context"></a>デバイス コンテキスト  
D1 の場合と同じです。

<a href="" id="miniport-driver-and-network-adapter-behavior"></a>ミニポート ドライバーとネットワーク アダプターの動作  
D1 の場合と同じです。

<a href="" id="restore-time"></a>復元時間  
ネットワーク アダプターを D0 状態に復元する特定は、ネットワーク アダプターが D1 状態を必要とするよりも大きいと、ネットワーク アダプターが D3 の状態を必要とするよりも小さいです。

### <a href="" id="d3"></a>デバイスの電源状態 D3

この電源状態の説明は、すべてのデバイスで[デバイス低電力状態](https://docs.microsoft.com/windows-hardware/drivers/kernel/device-sleeping-states)します。 ネットワーク アダプターおよびミニポート ドライバー。

<a href="" id="power-consumption"></a>電力消費量  
電力量が少なくとスリープの状態。 電力量がゼロ以外 (D3hot) あります。 または、正確に 0 (D3cold) がある可能性があります。 D3hot と D3cold の詳細については、次を参照してください。[デバイス低電力状態](https://docs.microsoft.com/windows-hardware/drivers/kernel/device-sleeping-states)します。

<a href="" id="device-context"></a>デバイス コンテキスト  
D1 の場合と同じです。

<a href="" id="miniport-driver-and-network-adapter-behavior"></a>ミニポート ドライバーとネットワーク アダプターの動作  
D1 の場合と同じです。

<a href="" id="restore-time"></a>復元時間  
ネットワーク アダプターを D0 状態に復元にかかる時間は、ネットワーク アダプターが D2 の状態を必要とするを超えています。

ミニポート ドライバーをミニポート ドライバーの管理下にあるすべて無効にする必要があります、ネットワーク アダプターは、スリープ状態に移行する、前に: タイマーをキャンセルする必要があります、やなど割り込みを無効にする必要があります。 バス ドライバーでは、ネットワーク アダプターを D3 状態に設定した後、ミニポート ドライバーは、ネットワーク アダプターのハードウェアにアクセスできません。

### <a name="transitions-allowed-between-device-power-states"></a>デバイスの電源状態の間の遷移

デバイスの電源状態の間で許可されている唯一の遷移はから highest-powered 状態 (D0) に (D1, D2, D3) に、スリープ状態またはスリープ状態から highest-powered 状態です。 NDIS は、別の 1 つのスリープ状態から直接ネットワーク アダプターを移行しないコマンドします。

 

 





