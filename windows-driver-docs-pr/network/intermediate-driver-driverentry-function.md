---
title: 中間ドライバー DriverEntry 関数
description: 中間ドライバー DriverEntry 関数
ms.assetid: 85b4d5c0-8ec9-41a9-a34e-578a85d411e3
keywords:
- 中間ドライバー WDK ネットワー キング、エントリ ポイント
- NDIS 中間ドライバー WDK、エントリ ポイント
- WDK のネットワー キングのエントリ ポイントします。
- ネットワーク DriverEntry WDK
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8c3a12d890cc5047628c698c30d2f2701def0c62
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67385085"
---
# <a name="intermediate-driver-driverentry-function"></a>中間ドライバー DriverEntry 関数





中間のドライバーの必要な初期のエントリ ポイントを明示的に指定する必要があります[ **DriverEntry** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_initialize)ローダーが識別して正しくできるようにします。 他のすべてのドライバーがエクスポートされた関数は、ため、このセクションで説明されている*MiniportXxx*と*ProtocolXxx*、NDIS アドレスとして渡されるために、任意のベンダーが指定した名前を持つことができます。

中間のドライバーでは、 **DriverEntry**には、少なくとも必要があります。

1.  呼び出す[ **NdisMRegisterMiniportDriver** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndismregisterminiportdriver)で返されるハンドルを保存し、 *NdisMiniportDriverHandle*パラメーター。

2.  呼び出す[ **NdisRegisterProtocolDriver** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndisregisterprotocoldriver)ドライバーの登録を*ProtocolXxx*場合と、ドライバー、その後バインド自体、基になる NDIS ドライバーに機能します。

3.  呼び出す[ **NdisIMAssociateMiniport** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndisimassociateminiport) NDIS ドライバーのミニポートの上端と下端のプロトコル間の関連付けに通知します。

中間のドライバーを登録する必要があります、 [ *MiniportDriverUnload* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-miniport_unload)ハンドラーをアンロードします。 システムが中間のドライバーをアンロードこのアンロード ハンドラーが呼び出されます。 場合[ **DriverEntry** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_initialize)失敗した場合、このアンロード ハンドラーは呼び出されません。 代わりに、ドライバーが読み込まれます。 アンロード ハンドラーの詳細については、次を参照してください。[中間のドライバーをアンロード](unloading-an-intermediate-driver.md)します。

アンロード ハンドラーを呼び出す必要があります[ **NdisDeregisterProtocolDriver** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndisderegisterprotocoldriver)中間ドライバーのプロトコルの一部の登録を解除します。 アンロード ハンドラーでは、ドライバーのプロトコルの部分で使用されるリソースを再割り当てなど、必要なクリーンアップ操作も実行する必要があります。

アンロード、ハンドラーが異なることに注意してください、 [ *MiniportHaltEx* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-miniport_halt)関数: アンロード ハンドラーが、多くのグローバル スコープとのスコープ、 *MiniportHaltEx*関数特定のミニポート アダプターに制限されています。 中間ドライバーは、状態情報をクリーンアップし、それにバインドされている基になる各ミニポート ドライバーが停止したときにリソースを再割り当てする必要があります。 仮想ミニポートの停止操作を処理する方法の詳細については、次を参照してください。[仮想ミニポートを停止する](halting-a-virtual-miniport.md)します。

[*ProtocolUninstall* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-protocol_uninstall)省略可能なアンロード ハンドラーします。 この関数のエントリ ポイントを登録、 *ProtocolCharacteristics*構造に渡す[ **NdisRegisterProtocolDriver**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndisregisterprotocoldriver)します。 NDIS 呼び出し*ProtocolUninstall*中間のドライバーをアンインストールするユーザーの要求に応答します。 NDIS 呼び出し[ *ProtocolUnbindAdapterEx* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-protocol_unbind_adapter_ex) 、バインドされたアダプターごとに 1 回呼び出して NDIS および*ProtocolUninstall*します。 システムが実際にドライバーをアンロードする前に、このハンドラーが呼び出されます。 このタイミングは、すべてのデバイス オブジェクト、またはアンロード ハンドラーに登録されている呼び出し元からそれ以外の場合、システムを妨げる可能性のあるその他のリソースを解放する機会を提供します。 **NdisMRegisterMiniportDriver**とドライバーをアンロードします。

**DriverEntry**状態変数、構造、およびメモリ領域などの中間ドライバーによって割り当てられるグローバルに共有のリソースを保護するスピン ロックを初期化することができます。 ドライバーの使用で進行状況やキューのドライバーに割り当てられた接続を追跡し、追跡するために、これらのリソースを送信します。

場合**DriverEntry**が失敗すると、ドライバーを実行する必要があるすべてのリソースを割り当てるネットワーク I/O 操作は、これは、以前に割り当てられたリソースを解放し、該当するエラー状態を返すか。

さらに、次のトピックでは、中間ドライバーを登録する方法について説明します。

[NDIS 中間ドライバーとして登録します。](registering-as-an-ndis-intermediate-driver.md)

[ミニポート ドライバーとして中間のドライバーを登録します。](registering-an-intermediate-driver-as-a-miniport-driver.md)

[プロトコル ドライバーとして中間のドライバーを登録します。](registering-an-intermediate-driver-as-a-protocol.md)

 

 





