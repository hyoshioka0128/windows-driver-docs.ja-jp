---
title: フィルター ドライバーの初期化
description: フィルター ドライバーの初期化
ms.assetid: e24b18b5-76d3-4d56-bf60-0dea91ba014e
keywords:
- フィルター ドライバー WDK ネットワーク、初期化しています
- NDIS フィルター ドライバー WDK、初期化しています
- フィルター ドライバーの初期化
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 55a64599b62de6a971752c7968724bbfbcf0d701
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67371831"
---
# <a name="initializing-a-filter-driver"></a>フィルター ドライバーの初期化



フィルター ドライバーの初期化は、システム、ドライバーの読み込み直後後に発生します。 システム サービスとしてのフィルター ドライバーの読み込み。 システムでは、前に、実行時に、またはミニポート ドライバーの読み込み後にいつでもフィルター ドライバーを読み込むことができます。 NDIS は、フィルター ドライバーでサポートされる型のミニポート アダプターが使用可能になり、フィルター ドライバーの初期化が完了したら、フィルター モジュールをミニポート アダプターにアタッチできます。

ドライバー スタックの起動中に、システムは、既に読み込まれていない場合、フィルター ドライバーを読み込みます。 フィルター モジュールが含まれるドライバー スタックを起動する方法の詳細については、次を参照してください。[開始ドライバー スタック](starting-a-driver-stack.md)します。

フィルター ドライバーが読み込まれると、システム呼び出してドライバーの[DriverEntry](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_initialize)ルーチン。 

システムは、2 つの引数を渡します[DriverEntry](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_initialize):

-   I/O システムによって作成されたドライバー オブジェクトへのポインター。

-   ドライバー固有のパラメーターを格納する場所を指定するレジストリ パスへのポインター。

[DriverEntry](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_initialize) NDIS フィルター ドライバーとドライバーが正常に登録されている場合に STATUS_SUCCESS、またはその同等の NDIS_STATUS_SUCCESS を返します。 場合**DriverEntry**伝達することによって返されたエラー状態で初期化が失敗した、 **NdisXxx**関数またはカーネル モードのサポート ルーチンでは、によってドライバーいないは読み込まれません。 **DriverEntry**実行する必要があります。 つまり、同期的には、STATUS_PENDING またはその同等 NDIS_STATUS_PENDING を返すことはできません。

フィルター ドライバーをドライバー オブジェクトを渡します、 [NdisFRegisterFilterDriver](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndisfregisterfilterdriver) NDIS フィルター ドライバーとしてを使用して登録するときに機能します。 ドライバーは、レジストリ パスを使用して、構成情報を取得します。 フィルター ドライバーの構成情報にアクセスする方法の詳細については、次を参照してください。[フィルター ドライバーの構成の情報にアクセスする](accessing-configuration-information-for-a-filter-driver.md)します。

フィルター ドライバーは呼び出し**NdisFRegisterFilterDriver**からその**DriverEntry**ルーチン。 フィルター ドライバーのセットをエクスポートする*FilterXxx*関数を渡すことによって、 [ **NDIS\_フィルター\_ドライバー\_特性**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_filter_driver_characteristics)構造体を**NdisFRegisterFilterDriver**で、 *FilterCharacteristics*パラメーター。

NDIS\_フィルター\_ドライバー\_の特性構造が必須とオプションのエントリ ポイントを指定します*FilterXxx*関数。 一部の省略可能な関数を迂回することができます。 機能のバイパスの詳細については、次を参照してください。[データ バイパス モード](data-bypass-mode.md)します。

呼び出すドライバー [NdisFRegisterFilterDriver](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndisfregisterfilterdriver)のいずれかに即時の呼び出しを準備する必要があります、 *FilterXxx*関数。

NDIS\_フィルター\_ドライバー\_の特性構造は、これらの必須のエントリ ポイントを指定します*FilterXxx*関数。

[*FilterAttach*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-filter_attach)

[*FilterDetach*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-filter_detach)

[*FilterRestart*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-filter_restart)

[*FilterPause*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-filter_pause)

NDIS\_フィルター\_ドライバー\_の特性構造が省略可能であり、実行時に、変更不可のこれらのエントリ ポイントを指定します*FilterXxx*関数。

[*FilterSetOptions*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-set_options)

[*FilterSetModuleOptions*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-filter_set_module_options)

[*FilterOidRequest*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-filter_oid_request)

[*FilterOidRequestComplete*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-filter_oid_request_complete)

[*FilterStatus*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-filter_status)

[*FilterNetPnPEvent*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-filter_net_pnp_event)

[*FilterDevicePnPEventNotify*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-filter_device_pnp_event_notify)

[*FilterCancelSendNetBufferLists*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-filter_cancel_send_net_buffer_lists)

NDIS\_フィルター\_ドライバー\_特性構造体は、これらの省略可能であり、実行時に、変更可能な既定のエントリ ポイントを指定*FilterXxx*関数。

[*FilterSendNetBufferLists*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-filter_send_net_buffer_lists)

[*FilterSendNetBufferListsComplete*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-filter_send_net_buffer_lists_complete)

[*FilterReturnNetBufferLists*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-filter_return_net_buffer_lists)

[*FilterReceiveNetBufferLists*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-filter_receive_net_buffer_lists)

上記の 4 つの関数も定義、 [ **NDIS\_フィルター\_部分\_特性**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_filter_partial_characteristics)構造体。 この構造体は、実行時に呼び出すことによって変更可能な関数を指定します、 [ **NdisSetOptionalHandlers** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndissetoptionalhandlers)関数を[ *FilterSetModuleOptions*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-filter_set_module_options)関数。 エントリ ポイントを提供する場合は、フィルター ドライバーを変更すると、実行時にこれらの部分の特性、 *FilterSetModuleOptions*します。 部分的な特性は、フィルター モジュールごとに異なるがあります。 詳細については、次を参照してください。[フィルター モジュールの開始](starting-a-filter-module.md)します。

NDIS 呼び出し、 *FilterSetOptions*関数への呼び出しのコンテキスト内で**NdisFRegisterFilterDriver**します。 *FilterSetOptions* NDIS を省略可能なサービスに登録します。 詳細については、次を参照してください。[省略可能なフィルター ドライバー サービスを構成する](configuring-optional-filter-driver-services.md)します。

場合への呼び出し**NdisFRegisterFilterDriver**成功すると、NDIS に変数を入力する*NdisFilterDriverHandle*フィルター ドライバーのハンドルを使用します。 フィルター ドライバーは、このハンドルを保存しなど、NDIS 関数にこのハンドルを渡します後で[ **NdisFDeregisterFilterDriver**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndisfderegisterfilterdriver)、入力パラメーターとしてフィルター ドライバーのハンドルを必要とします。 ドライバーをアンロードするときに呼び出す必要があります、 **NdisFDeregisterFilterDriver**関数によって割り当てられたドライバー リソースを解放する**NdisFRegisterFilterDriver**します。

後*FilterSetOptions*フィルター モジュールでは、返される、 *Detached*状態。 NDIS フィルター ドライバーを呼び出すことができます[ *FilterAttach* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-filter_attach)関数呼び出しの後、いつでも*FilterSetOptions*を返します。 ドライバーのフィルター モジュールに固有の初期化を実行する、 *FilterAttach*関数。 ドライバー スタックへのフィルター モジュールのインポートに関する詳細については、次を参照してください。[フィルター モジュールのアタッチ](attaching-a-filter-module.md)します。

フィルター ドライバーで必要なその他の個々 のドライバーの初期化を実行も**DriverEntry**します。 フィルター ドライバーに割り当てるドライバー固有のリソースをリリースする必要があります、 [ *FilterDriverUnload* ](https://docs.microsoft.com/windows-hardware/drivers/network/unloading-a-filter-driver)ルーチン。 詳細については、次を参照してください。[フィルター ドライバーをアンロード](unloading-a-filter-driver.md)します。

 

 





