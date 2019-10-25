---
title: ミニポート ドライバーの初期化
description: ミニポート ドライバーの初期化
ms.assetid: cda2437c-b292-4d21-b200-89c7b55cd46c
keywords:
- ミニポートドライバー WDK ネットワーク、初期化
- ミニポートドライバーの初期化
- NDIS ミニポートドライバー WDK、初期化
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: a69cc4ecad861ec9515c16006c1f8a22970b4b9a
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72824505"
---
# <a name="initializing-a-miniport-driver"></a>ミニポート ドライバーの初期化



ネットワークデバイスが使用可能になると、システムはデバイスを管理するために NDIS ミニポートドライバーを読み込みます (ドライバーがまだ読み込まれていない場合)。 すべてのミニポートドライバーは[Driverentry](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_initialize)関数を提供する必要があります。 ドライバーが読み込まれた後、システムは**Driverentry**を呼び出します。 **Driverentry**は、ミニポートドライバーの特性を ndis に登録します (サポートされている ndis のバージョンとドライバーのエントリポイントを含む)。

システムは[Driverentry](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_initialize)に2つの引数を渡します。

-   I/o システムによって作成された driver オブジェクトへのポインター。

-   ドライバー固有のパラメーターが格納される場所を指定するレジストリパスへのポインター。

[Driverentry](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_initialize)では、ミニポートドライバーは、 [NdisMRegisterMiniportDriver](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismregisterminiportdriver)関数の呼び出しでこれらの両方のポインターを渡します。 ミニポートドライバーは、標準の*Miniportxxx*関数のセットをエクスポートします。そのためには、 [**NDIS\_ミニポート\_ドライバー\_特性**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_miniport_driver_characteristics)の構造体にエントリポイントを格納し、その構造体をに**渡します。NdisMRegisterMiniportDriver**。 

ミニポートドライバーの**Driverentry**は、 **NdisMRegisterMiniportDriver**への呼び出しによって返される値を返します。

また、ミニポートドライバーは、 [Driverentry](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_initialize)で必要なドライバー固有のその他の初期化も実行します。 ドライバーは、 [*MiniportInitializeEx*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_initialize)関数でアダプター固有の初期化を実行します。 アダプターの初期化の詳細については、「[アダプターの初期化](initializing-a-miniport-adapter.md)」を参照してください。

[Driverentry](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_initialize)は、ndis ライブラリが関連する情報を独自のストレージにコピーするため、 [**NDIS\_ミニポート\_ドライバー\_の特性**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_miniport_driver_characteristics)構造をスタックに割り当てることができます。 **Driverentry**では、そのメンバーにドライバーで指定された値を設定する前に、 [NdisZeroMemory](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndiszeromemory)を使用してこの構造体のメモリをクリアする必要があります。 **MajorNdisVersion**と**MinorNdisVersion**のメンバーには、ドライバーがサポートする NDIS のメジャーバージョンとマイナーバージョンが含まれている必要があります。 特性の構造体の各 Xxx**ハンドラー**メンバーで、 **driverentry**はドライバーによって指定された*miniportxxx*関数のエントリポイントを設定するか、メンバーを**NULL**にする必要があります。

ミニポートドライバーでオプションのサービスを構成できるようにするために、NDIS は[NdisMRegisterMiniportDriver](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismregisterminiportdriver)へのミニポートドライバーの呼び出しのコンテキスト内で[MiniportSetOptions](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-set_options)関数を呼び出します。 オプションのサービスの詳細については、「[オプションのミニポートドライバーサービスの構成](configuring-optional-miniport-driver-services.md)」を参照してください。

[NdisMRegisterMiniportDriver](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismregisterminiportdriver)を呼び出すドライバーは、 **driverentry**が返された後、いつでも[*MiniportInitializeEx*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_initialize)関数を呼び出すように NDIS に準備する必要があります。 このようなドライバーには、レジストリに格納されている十分なインストールおよび構成情報が必要です。または、ドライバーが実行する必要のある NIC 固有のリソースを設定するために、 **NdisXxx** bus タイプ固有の構成関数の呼び出しから使用できます。ネットワーク i/o 操作。

ミニポートドライバーは、 [**NdisMRegisterMiniportDriver**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismregisterminiportdriver)を呼び出すことによって割り当てられたリソースを解放するために、最終的に[**NdisMDeregisterMiniportDriver**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismderegisterminiportdriver)を呼び出す必要があります。 **NdisMRegisterMiniportDriver**への呼び出しが成功した後にドライバーの初期化が失敗した場合、ドライバーは[driverentry](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_initialize)内から**NdisMDeregisterMiniportDriver**を呼び出すことができます。 それ以外の場合、ミニポートドライバーは、 [*Miniportdriverunload*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_unload)関数に割り当てられているドライバー固有のリソースを解放する必要があります。 つまり、NdisMRegisterMiniportDriver が NDIS_STATUS_SUCCESS を返さない場合、 **Driverentry**はコントロールを返す前に割り当てられたリソースを解放する必要があります。 このエラーが発生した場合、ドライバーは読み込まれません。 詳細については、「[ミニポートドライバーのアンロード](unloading-a-miniport-driver.md)」を参照してください。

 

 





