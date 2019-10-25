---
title: 中間ドライバー DriverEntry 関数
description: 中間ドライバー DriverEntry 関数
ms.assetid: 85b4d5c0-8ec9-41a9-a34e-578a85d411e3
keywords:
- 中間ドライバー WDK ネットワーク、エントリポイント
- NDIS 中間ドライバー WDK、エントリポイント
- エントリポイント WDK ネットワーク
- DriverEntry WDK ネットワーク
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: adaf4daed294e73215691d9b37ef0c5a7b1eef57
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72844185"
---
# <a name="intermediate-driver-driverentry-function"></a>中間ドライバー DriverEntry 関数





中間ドライバーの最初の必須エントリポイントは、ローダーが適切に識別できるように、明示的に[**driverentry**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_initialize)という名前にする必要があります。 このセクションで説明さ*れている*他のすべてのエクスポートされたドライバー関数は、NDIS にアドレスとして渡されるため、ベンダーが指定した*名前を持つ*ことができます。

中間ドライバーでは、 **Driverentry**に少なくとも次の値を指定する必要があります。

1.  [**NdisMRegisterMiniportDriver**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismregisterminiportdriver)を呼び出し、 *NdisMiniportDriverHandle*パラメーターに返されたハンドルを保存します。

2.  ドライバーがその後、基になる NDIS ドライバーにバインドする場合は、 [**NdisRegisterProtocolDriver**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisregisterprotocoldriver)を呼び出してドライバーの*protocolxxx*関数を登録します。

3.  [**NdisIMAssociateMiniport**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisimassociateminiport)を呼び出して、ドライバーのミニポートの上端とプロトコルの下端との関連付けについて NDIS に通知します。

中間ドライバーは、 [*Miniportdriverunload*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_unload)アンロードハンドラーを登録する必要があります。 このアンロードハンドラーは、システムによって中間ドライバーがアンロードされるときに呼び出されます。 [**Driverentry**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_initialize)が失敗した場合、このアンロードハンドラーは呼び出されません。代わりに、ドライバーは単にアンロードされます。 Unload ハンドラーの詳細については、「[中間ドライバーのアンロード](unloading-an-intermediate-driver.md)」を参照してください。

Unload ハンドラーは、中間ドライバーのプロトコル部分を登録解除するために[**NdisDeregisterProtocolDriver**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisderegisterprotocoldriver)を呼び出す必要があります。 また、アンロードハンドラーは、ドライバーのプロトコル部分で使用されるリソースの再割り当てなど、必要なクリーンアップ操作も実行する必要があります。

Unload ハンドラーは、 [*Miniporthaltex*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_halt)関数とは異なることに注意してください。 unload ハンドラーはよりグローバルなスコープを持ち、 *Miniporthaltex*関数のスコープは特定のミニポートアダプターに制限されています。 中間ドライバーは、バインドされている基になるミニポートドライバーが停止されると、状態情報をクリーンアップし、リソースを再割り当てする必要があります。 仮想ミニポートの停止操作の処理の詳細については、「[仮想ミニポートの停止](halting-a-virtual-miniport.md)」を参照してください。

[*Protocoluninstall*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-protocol_uninstall)は省略可能なアンロードハンドラーです。 [**NdisRegisterProtocolDriver**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisregisterprotocoldriver)に渡す*protocolcharacteristics*構造体に、この関数のエントリポイントを登録します。 NDIS は、中間ドライバーをアンインストールするユーザーの要求に応じて*Protocoluninstall*を呼び出します。 NDIS は、バインドされたアダプターごとに[*Protocolunbindadapterex*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-protocol_unbind_adapter_ex)を呼び出し、Ndis は*protocoluninstall*を呼び出します。 このハンドラーは、システムによって実際にドライバーがアンロードされる前に呼び出されます。 このタイミングで、 **NdisMRegisterMiniportDriver**に登録されているアンロードハンドラーがシステムによって呼び出され、ドライバーがアンロードされるのを防ぐ、デバイスオブジェクトやその他のリソースが解放される可能性があります。

**Driverentry**では、スピンロックを初期化して、中間ドライバーが割り当てたグローバル共有リソース (状態変数、構造体、メモリ領域など) を保護することができます。 ドライバーは、これらのリソースを使用して接続を追跡し、進行中の送信またはドライバーによって割り当てられたキューを追跡します。

**Driverentry**が、ネットワーク i/o 操作を実行するために必要なリソースの割り当てに失敗した場合、以前に割り当てられたリソースを解放し、適切なエラー状態を返します。

次のトピックでは、中間ドライバーを登録する方法について詳しく説明します。

[NDIS 中間ドライバーとして登録する](registering-as-an-ndis-intermediate-driver.md)

[ミニポートドライバーとしての中間ドライバーの登録](registering-an-intermediate-driver-as-a-miniport-driver.md)

[プロトコルドライバーとしての中間ドライバーの登録](registering-an-intermediate-driver-as-a-protocol.md)

 

 





