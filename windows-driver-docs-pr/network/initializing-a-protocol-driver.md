---
title: プロトコル ドライバーの初期化
description: プロトコル ドライバーの初期化
ms.assetid: 1479d59b-7c8b-495b-86c7-72f1b7e334e4
keywords:
- プロトコルドライバー WDK ネットワーク、初期化
- NDIS プロトコルドライバー WDK、初期化
- プロトコルドライバーの初期化
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ca80f51784b974f715d08a619b1c2d4536cc5af7
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72824502"
---
# <a name="initializing-a-protocol-driver"></a>プロトコル ドライバーの初期化




ドライバーが読み込まれた後、システムはプロトコルドライバーの[Driverentry](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_initialize)ルーチンを呼び出します。 プロトコルドライバーは、システムサービスとして読み込まれます。 これらは、ミニポートドライバーの読み込みの前、後、または後でいつでも読み込むことができます。

プロトコルドライバーはドライバーリソースを割り当て、 **Driverentry**に*protocolxxx*関数を登録します。 これには、CoNDIS クライアントとスタンドアロンの呼び出しマネージャーが含まれます。 プロトコルドライバーは、その*Protocolxxx*関数を NDIS に登録するために、 [NdisRegisterProtocolDriver](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisregisterprotocoldriver)関数を呼び出します。

ドライバーが NDIS プロトコルドライバーとして正常に登録されている場合、 [Driverentry](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_initialize)は STATUS_SUCCESS、またはそれと同等の NDIS_STATUS_SUCCESS を返します。 **NdisXxx**関数またはカーネルモードのサポートルーチンによって返されたエラー状態を伝達することによって、 **driverentry**が初期化に失敗した場合、ドライバーは読み込まれたままになりません。 **Driverentry**は同期的に実行する必要があります。つまり、STATUS_PENDING またはそれと同等の NDIS_STATUS_PENDING を返すことはできません。

NDIS プロトコルドライバーの[Driverentry](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_initialize)関数は、 [NdisRegisterProtocolDriver](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisregisterprotocoldriver)関数を呼び出す必要があります。 ドライバーの*Protocolxxx*エントリポイントを NDIS ライブラリに登録するために、プロトコルドライバーは[**NDIS_PROTOCOL_DRIVER_CHARACTERISTICS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_protocol_driver_characteristics)構造体を初期化し、 **NdisRegisterProtocolDriver**に渡します。

NdisRegisterProtocolDriver を呼び出すドライバーは、その ProtocolXxx 関数をすぐに呼び出すために準備する必要があります。

NDIS プロトコルドライバーには、次の*Protocolxxx*関数が用意されています。これらは、レガシドライバーが提供する関数の更新バージョンです。

[*ProtocolSetOptions*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-set_options)

[*ProtocolBindAdapterEx*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-protocol_bind_adapter_ex)

[*ProtocolUnbindAdapterEx*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-protocol_unbind_adapter_ex)

[*ProtocolOpenAdapterCompleteEx*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-protocol_open_adapter_complete_ex)

[*ProtocolCloseAdapterCompleteEx*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-protocol_close_adapter_complete_ex)

[*ProtocolNetPnPEvent*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-protocol_net_pnp_event)

[*ProtocolUninstall*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-protocol_uninstall)

NDIS プロトコルドライバーは、送信および受信操作に次の*Protocolxxx*関数を提供します。

[**ProtocolReceiveNetBufferLists**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-protocol_receive_net_buffer_lists)

[**ProtocolSendNetBufferListsComplete**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-protocol_send_net_buffer_lists_complete)

すべての種類の NDIS プロトコルドライバーは、完全に機能する[*protocolbindadapterex*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-protocol_bind_adapter_ex)および[*protocolunbindadapterex*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-protocol_unbind_adapter_ex)関数を登録して、プラグアンドプレイ (PnP) をサポートする必要があります。 一般に、 [Driverentry](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_initialize)関数は、状態値が STATUS_SUCCESS または NDIS_STATUS_SUCCESS のコントロールを返す直前に[NdisRegisterProtocolDriver](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisregisterprotocoldriver)を呼び出す必要があります。

NDIS によって定義された*Protocolxxx*関数に加えて、一連の標準カーネルモードドライバールーチンをエクスポートするプロトコルドライバーは、その[driverentry](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_initialize)関数に渡される特定のドライバーオブジェクト内のドライバールーチンのエントリポイントを設定する必要があります。 このようなプロトコルドライバーの**driverentry**関数の機能の詳細については、「 [Driverentry ルーチンを記述する](../kernel/writing-a-driverentry-routine.md)」を参照してください。

ドライバーがネットワーク i/o 操作を実行するために必要なリソースを割り当てることができなかった場合、 [Driverentry](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_initialize)は、既に割り当てられているすべてのリソースを解放してから、STATUS_SUCCESS または NDIS_STATUS_SUCCESS 以外の状態のコントロールを返します。

[NdisRegisterProtocolDriver](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisregisterprotocoldriver)への呼び出しが成功した後でエラーが発生した場合、ドライバーは**driverentry**を返す前に[NdisDeregisterProtocolDriver](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisderegisterprotocoldriver)関数を呼び出す必要があります。

プロトコルドライバーでオプションのサービスを構成できるようにするために、NDIS は、 **NdisRegisterProtocolDriver**へのプロトコルドライバーの呼び出しのコンテキスト内で*ProtocolSetOptions*関数を呼び出します。 オプションのサービスの詳細については、「[オプションのプロトコルドライバーサービスの構成](configuring-optional-protocol-driver-services.md)」を参照してください。

CoNDIS client ドライバーは、 [*ProtocolSetOptions*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-set_options)関数から[NdisSetOptionalHandlers](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndissetoptionalhandlers)関数を呼び出す必要があります。 このドライバーは[**NDIS_CO_CLIENT_OPTIONAL_HANDLERS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_co_client_optional_handlers)構造体を初期化し、 **NdisSetOptionalHandlers**のパラメーター化された*ハンドラー*パラメーターに渡します。

CoNDIS スタンドアロンの呼び出しマネージャーも、 [*ProtocolSetOptions*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-set_options)関数から[NdisSetOptionalHandlers](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndissetoptionalhandlers)関数を呼び出す必要があります。 このドライバーは[**NDIS_CO_CALL_MANAGER_OPTIONAL_HANDLERS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_co_call_manager_optional_handlers)構造体を初期化し、 **NdisSetOptionalHandlers**のパラメーター化された*ハンドラー*パラメーターに渡します。

MCMs はプロトコルドライバーではありません。 したがって、 [MiniportSetOptions](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-set_options)関数から[NdisSetOptionalHandlers](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndissetoptionalhandlers)関数を呼び出す必要があります。 MCM は[**NDIS_CO_CALL_MANAGER_OPTIONAL_HANDLERS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_co_call_manager_optional_handlers)構造体を初期化し、 **NdisSetOptionalHandlers**のパラメーター化された*ハンドラー*パラメーターに渡します。

NDIS から登録を解除するために、プロトコルドライバーはその[アンロード](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_unload)ルーチンから[NdisDeregisterProtocolDriver](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisderegisterprotocoldriver)を呼び出します。

プロトコルドライバーをアンインストールする前にクリーンアップ操作を実行するために、プロトコルドライバーは[*Protocoluninstall*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-protocol_uninstall)関数を登録できます。 *Protocoluninstall*関数は省略可能です。 たとえば、中間ドライバーの低エッジプロトコルには*Protocoluninstall*関数が必要になる場合があります。 中間ドライバーは、NDIS が[*Miniportdriverunload*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_unload)関数を呼び出す前に、 *protocoluninstall*でそのプロトコルエッジリソースを解放できます。

 

 





