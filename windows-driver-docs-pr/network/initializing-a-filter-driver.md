---
title: フィルター ドライバーの初期化
description: フィルター ドライバーの初期化
ms.assetid: e24b18b5-76d3-4d56-bf60-0dea91ba014e
keywords:
- フィルタードライバーの WDK ネットワーク, 初期化
- NDIS フィルタードライバー WDK、初期化
- フィルタードライバーの初期化
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 96f59e4d9378b93ac72d29f8f7ff9d74a198af65
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72824602"
---
# <a name="initializing-a-filter-driver"></a>フィルター ドライバーの初期化



フィルタードライバーの初期化は、システムによってドライバーが読み込まれた直後に発生します。 フィルタードライバーは、システムサービスとして読み込まれます。 システムは、ミニポートドライバーの読み込みの前、後、または後に、いつでもフィルタードライバーを読み込むことができます。 フィルタードライバーでサポートされている種類のミニポートアダプターが使用可能になり、フィルタードライバーの初期化が完了すると、NDIS はミニポートアダプターにフィルターモジュールをアタッチできます。

ドライバースタックの開始中は、フィルタードライバーがまだ読み込まれていなければ、システムによって読み込まれます。 フィルターモジュールを含むドライバースタックを開始する方法の詳細については、「[ドライバースタックの開始](starting-a-driver-stack.md)」を参照してください。

フィルタードライバーが読み込まれると、システムはドライバーの[Driverentry](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_initialize)ルーチンを呼び出します。 

システムは[Driverentry](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_initialize)に2つの引数を渡します。

-   I/o システムによって作成された driver オブジェクトへのポインター。

-   ドライバー固有のパラメーターが格納される場所を指定するレジストリパスへのポインター。

ドライバーが NDIS フィルタードライバーとして正常に登録されている場合、 [Driverentry](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_initialize)は STATUS_SUCCESS、またはそれと同等の NDIS_STATUS_SUCCESS を返します。 **NdisXxx**関数またはカーネルモードのサポートルーチンによって返されたエラー状態を伝達することによって、 **driverentry**が初期化に失敗した場合、ドライバーは読み込まれたままになりません。 **Driverentry**は同期的に実行する必要があります。つまり、ありますまたはそれに相当する NDIS_STATUS_PENDING を返すことはできません。

フィルタードライバーは、ドライバーオブジェクトをフィルタードライバーとして NDIS に登録するときに、 [NdisFRegisterFilterDriver](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisfregisterfilterdriver)関数に渡します。 ドライバーは、レジストリパスを使用して構成情報を取得できます。 フィルタードライバーの構成情報にアクセスする方法の詳細については、「[フィルタードライバーの構成情報](accessing-configuration-information-for-a-filter-driver.md)へのアクセス」を参照してください。

フィルタードライバーは、その**Driverentry**ルーチンから**NdisFRegisterFilterDriver**を呼び出します。 フィルタードライバーは、filterxxx*関数の*セットをエクスポートします。そのためには、 **NDISFREGISTERFILTERDRIVER** [**フィルター\_ドライバー\_特性**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_filter_driver_characteristics)の構造を*filterxxx*パラメーターに\_渡します。

NDIS\_フィルター\_ドライバー\_特性の構造では、必須および省略可能な*Filterxxx*関数のエントリポイントを指定します。 一部のオプションの関数は省略できます。 関数のバイパスの詳細については、「[データバイパスモード](data-bypass-mode.md)」を参照してください。

[NdisFRegisterFilterDriver](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisfregisterfilterdriver)を呼び出すドライバーは、その*filterxxx*関数を直接呼び出すために準備する必要があります。

NDIS\_フィルター\_ドライバー\_特性の構造では、これらの必須の*Filterxxx*関数のエントリポイントを指定します。

[*FilterAttach*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-filter_attach)

[*FilterDetach*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-filter_detach)

[*FilterRestart*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-filter_restart)

[*FilterPause*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-filter_pause)

NDIS\_フィルター\_ドライバー\_特性の構造では、これらのオプションのエントリポイントを指定します。実行時*には*変更できません。

[*FilterSetOptions*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-set_options)

[*FilterSetModuleOptions*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-filter_set_module_options)

[*FilterOidRequest*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-filter_oid_request)

[*FilterOidRequestComplete*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-filter_oid_request_complete)

[*FilterStatus*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-filter_status)

[*FilterNetPnPEvent*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-filter_net_pnp_event)

[*FilterDevicePnPEventNotify*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-filter_device_pnp_event_notify)

[*FilterCancelSendNetBufferLists*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-filter_cancel_send_net_buffer_lists)

NDIS\_フィルター\_ドライバー\_特性の構造では、これらのオプションの既定のエントリポイントを指定し、実行*時に変更できます。*

[*FilterSendNetBufferLists*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-filter_send_net_buffer_lists)

[*FilterSendNetBufferListsComplete*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-filter_send_net_buffer_lists_complete)

[*FilterReturnNetBufferLists*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-filter_return_net_buffer_lists)

[*FilterReceiveNetBufferLists*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-filter_receive_net_buffer_lists)

前の4つの関数は、「 [**NDIS\_FILTER\_部分的な\_特性**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_filter_partial_characteristics)の構造」にも定義されています。 この構造体は、 [*Filtersetmoduleoptions*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-filter_set_module_options)関数から[**NdisSetOptionalHandlers**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndissetoptionalhandlers)関数を呼び出すことによって、実行時に変更できる関数を指定します。 フィルタードライバーが実行時にこれらの部分特性を変更する場合は、 *Filtersetmoduleoptions*のエントリポイントを提供する必要があります。 部分特性は、フィルターモジュールごとに異なる場合があります。 詳細については、「[フィルターモジュールを開始する](starting-a-filter-module.md)」を参照してください。

NDIS は、 **NdisFRegisterFilterDriver**への呼び出しのコンテキスト内で*FilterSetOptions*関数を呼び出します。 *FilterSetOptions*は、オプションのサービスを NDIS に登録します。 詳細については、「[オプションフィルタードライバーサービスの構成](configuring-optional-filter-driver-services.md)」を参照してください。

**NdisFRegisterFilterDriver**への呼び出しが成功した場合、NDIS は*NdisFilterDriverHandle*の変数にフィルタードライバーハンドルを入力します。 フィルタードライバーはこのハンドルを保存し、後でこのハンドルを[**NdisFDeregisterFilterDriver**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisfderegisterfilterdriver)などの NDIS 関数に渡します。これには、入力パラメーターとしてフィルタードライバーハンドルが必要です。 ドライバーがアンロードされたら、 **NdisFDeregisterFilterDriver**関数を呼び出して、 **NdisFRegisterFilterDriver**によって割り当てられたドライバーリソースを解放する必要があります。

*FilterSetOptions*が返されると、フィルターモジュールは*デタッチ*された状態になります。 NDIS は、 *FilterSetOptions*の呼び出しが返された後、いつでもフィルタードライバーの[*filterattach*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-filter_attach)関数を呼び出すことができます。 ドライバーは、 *Filterattach*関数でモジュール固有のフィルターの初期化を実行します。 フィルターモジュールをドライバースタックにアタッチする方法の詳細については、「[フィルターモジュールのアタッチ](attaching-a-filter-module.md)」を参照してください。

フィルタードライバーは、 **Driverentry**で必要なドライバー固有のその他の初期化も実行します。 フィルタードライバーは、 [*Filterdriverunload*](https://docs.microsoft.com/windows-hardware/drivers/network/unloading-a-filter-driver)ルーチンに割り当てられているドライバー固有のリソースを解放する必要があります。 詳細については、「[フィルタードライバーのアンロード](unloading-a-filter-driver.md)」を参照してください。

 

 





