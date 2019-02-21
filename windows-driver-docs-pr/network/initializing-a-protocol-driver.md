---
title: プロトコル ドライバーの初期化
description: プロトコル ドライバーの初期化
ms.assetid: 1479d59b-7c8b-495b-86c7-72f1b7e334e4
keywords:
- プロトコルのドライバー WDK ネットワーク、初期化しています
- NDIS ドライバー WDK のプロトコルの初期化
- プロトコル ドライバーの初期化
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d043809b5a93e4e6feb8a08dce74b6f8c3fdf3e3
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56530115"
---
# <a name="initializing-a-protocol-driver"></a>プロトコル ドライバーの初期化




システム呼び出しプロトコル ドライバーの[DriverEntry](https://msdn.microsoft.com/library/windows/hardware/ff544113)ルーチン、ドライバーが読み込まれた後です。 プロトコル ドライバーは、システム サービスとして読み込みます。 前にいつでも読み込むことができますが、中、または後、ミニポート ドライバーを読み込みます。

プロトコル ドライバーがドライバーのリソースを割り当てるし、登録*ProtocolXxx*関数**DriverEntry**します。 これには、いる CoNDIS クライアントとスタンドアロンのコール マネージャーが含まれます。 登録するその*ProtocolXxx* NDIS と関数は、プロトコル ドライバーの呼び出し、 [NdisRegisterProtocolDriver](https://msdn.microsoft.com/library/windows/hardware/ff564520)関数。

[DriverEntry](https://msdn.microsoft.com/library/windows/hardware/ff544113) NDIS プロトコル ドライバーとしてドライバーが正常に登録されている場合に STATUS_SUCCESS、またはその同等の NDIS_STATUS_SUCCESS を返します。 場合**DriverEntry**伝達することによって返されたエラー状態で初期化が失敗した、 **NdisXxx**関数またはカーネル モードのサポート ルーチンでは、によってドライバーいないは読み込まれません。 **DriverEntry**実行する必要があります。 つまり、同期的には、STATUS_PENDING またはその同等 NDIS_STATUS_PENDING を返すことはできません。

[DriverEntry](https://msdn.microsoft.com/library/windows/hardware/ff544113) NDIS プロトコル ドライバーの関数を呼び出す必要があります、 [NdisRegisterProtocolDriver](https://msdn.microsoft.com/library/windows/hardware/ff564520)関数。 ドライバーの登録に*ProtocolXxx* NDIS ライブラリ、エントリ ポイントのプロトコルのドライバーを初期化します、 [ **NDIS_PROTOCOL_DRIVER_CHARACTERISTICS** ](https://msdn.microsoft.com/library/windows/hardware/ff566825)構造と渡されます**NdisRegisterProtocolDriver**します。

その ProtocolXxx 機能のいずれかに即時の呼び出しの NdisRegisterProtocolDriver を呼び出してドライバーを準備する必要があります。

NDIS プロトコル ドライバーは、次を提供*ProtocolXxx*関数で、従来のドライバーを提供する関数のバージョンが更新されました。

[*ProtocolSetOptions*](https://msdn.microsoft.com/library/windows/hardware/ff570269)

[*ProtocolBindAdapterEx*](https://msdn.microsoft.com/library/windows/hardware/ff570220)

[*ProtocolUnbindAdapterEx*](https://msdn.microsoft.com/library/windows/hardware/ff570278)

[*ProtocolOpenAdapterCompleteEx*](https://msdn.microsoft.com/library/windows/hardware/ff570265)

[*ProtocolCloseAdapterCompleteEx*](https://msdn.microsoft.com/library/windows/hardware/ff570236)

[*ProtocolNetPnPEvent*](https://msdn.microsoft.com/library/windows/hardware/ff570263)

[*ProtocolUninstall*](https://msdn.microsoft.com/library/windows/hardware/ff570279)

NDIS プロトコル ドライバーは、次を提供*ProtocolXxx*関数の送受信操作。

[**ProtocolReceiveNetBufferLists**](https://msdn.microsoft.com/library/windows/hardware/ff570267)

[**ProtocolSendNetBufferListsComplete**](https://msdn.microsoft.com/library/windows/hardware/ff570268)

NDIS プロトコル ドライバーのすべての種類を完全に機能に登録する必要があります[ *ProtocolBindAdapterEx* ](https://msdn.microsoft.com/library/windows/hardware/ff570220)と[ *ProtocolUnbindAdapterEx* ](https://msdn.microsoft.com/library/windows/hardware/ff570278)プラグ アンド プレイ (PnP) をサポートする関数。 一般に、 [DriverEntry](https://msdn.microsoft.com/library/windows/hardware/ff544113)関数を呼び出す必要があります[NdisRegisterProtocolDriver](https://msdn.microsoft.com/library/windows/hardware/ff564520)直後に、前に STATUS_SUCCESS または NDIS_STATUS_SUCCESS のステータス値を持つコントロールを返します。

その NDIS 定義だけでなく、標準のカーネル モード ドライバー ルーチンのセットをエクスポートする任意のプロトコル ドライバー *ProtocolXxx*関数に渡される特定のドライバー オブジェクト内でこれらのドライバー ライブラリ ルーチンのエントリ ポイントを設定する必要がありますその[DriverEntry](https://msdn.microsoft.com/library/windows/hardware/ff544113)関数。 このようなプロトコル ドライバーの機能の詳細についての**DriverEntry**関数を参照してください[DriverEntry ルーチンを記述](../kernel/writing-a-driverentry-routine.md)します。

場合、ドライバーは、ネットワーク I/O 操作の失敗が、実行するために必要なリソースを割り当てられません[DriverEntry](https://msdn.microsoft.com/library/windows/hardware/ff544113)すべてのリソースを解放する必要があります、既に status _ 以外のステータスを持つコントロールを返す前に割り当てる成功または NDIS_STATUS_SUCCESS。

呼び出しに成功した後にエラーが発生した場合[NdisRegisterProtocolDriver](https://msdn.microsoft.com/library/windows/hardware/ff564520)、ドライバーを呼び出す必要があります、 [NdisDeregisterProtocolDriver](https://msdn.microsoft.com/library/windows/hardware/ff561743)する前に関数**DriverEntry**返します。

省略可能なサービスを構成するプロトコル ドライバーには、NDIS 呼び出しは、 *ProtocolSetOptions*プロトコル ドライバーの呼び出しのコンテキスト内で関数**NdisRegisterProtocolDriver**します。 省略可能なサービスの詳細については、次を参照してください。[省略可能なプロトコル ドライバー サービスを構成する](configuring-optional-protocol-driver-services.md)します。

いる CoNDIS クライアント ドライバーを呼び出す必要があります、 [NdisSetOptionalHandlers](https://msdn.microsoft.com/library/windows/hardware/ff564550)関数を[ *ProtocolSetOptions* ](https://msdn.microsoft.com/library/windows/hardware/ff570269)関数。 ドライバーの初期化、 [ **NDIS_CO_CLIENT_OPTIONAL_HANDLERS** ](https://msdn.microsoft.com/library/windows/hardware/ff564884)を構造化し、これで、 *OptionalHandlers*パラメーターの**NdisSetOptionalHandlers**します。

スタンドアロンのコール マネージャーを呼び出す必要がありますもいる CoNDIS、 [NdisSetOptionalHandlers](https://msdn.microsoft.com/library/windows/hardware/ff564550)関数を[ *ProtocolSetOptions* ](https://msdn.microsoft.com/library/windows/hardware/ff570269)関数。 ドライバーの初期化、 [ **NDIS_CO_CALL_MANAGER_OPTIONAL_HANDLERS** ](https://msdn.microsoft.com/library/windows/hardware/ff564883)を構造化し、これで、 *OptionalHandlers*パラメーターの**NdisSetOptionalHandlers**します。

MCMs はプロトコル ドライバーではありません。 そのため、呼び出す必要がありますが、 [NdisSetOptionalHandlers](https://msdn.microsoft.com/library/windows/hardware/ff564550)関数を[MiniportSetOptions](https://msdn.microsoft.com/library/windows/hardware/ff559443)関数。 MCM を初期化します、 [ **NDIS_CO_CALL_MANAGER_OPTIONAL_HANDLERS** ](https://msdn.microsoft.com/library/windows/hardware/ff564883)を構造化し、これで、 *OptionalHandlers*パラメーターの**NdisSetOptionalHandlers**します。

プロトコル ドライバーに呼び出し NDIS を使用して登録を解除する[NdisDeregisterProtocolDriver](https://msdn.microsoft.com/library/windows/hardware/ff561743)からその[アンロード](https://msdn.microsoft.com/library/windows/hardware/ff564886)ルーチン。

プロトコル ドライバーの登録プロトコル ドライバーをアンインストールする前にクリーンアップ操作を実行することができます、 [ *ProtocolUninstall* ](https://msdn.microsoft.com/library/windows/hardware/ff570279)関数。 *ProtocolUninstall*関数は省略可能です。 たとえば、中間のドライバーの下端プロトコルが必要があります、 *ProtocolUninstall*関数。 中間ドライバーではそのプロトコル エッジのリソースを解放できます*ProtocolUninstall* NDIS 呼び出される前にその[ *MiniportDriverUnload* ](https://msdn.microsoft.com/library/windows/hardware/ff559378)関数。

 

 





