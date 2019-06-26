---
title: データ バイパス モード
description: データ バイパス モード
ms.assetid: 98061803-22de-4fa2-8582-2d382f84dd75
keywords:
- フィルター ドライバー WDK ネットワーク、データのバイパス モード
- NDIS フィルター ドライバー WDK、データのバイパス モード
- データは、モード WDK ネットワークをバイパスします。
- バイパス モード WDK ネットワーク
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9f15258293a0949b841fd9ec20251106d9297672
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67364948"
---
# <a name="data-bypass-mode"></a>データ バイパス モード





フィルター ドライバー*データ バイパス モード*システム パフォーマンスの向上を提供することができます。 NDIS は呼び出しません*FilterXxx*関数がバイパスされます。 たとえば場合、送信および受信サービスではありません。 指定したフィルター アプリケーションに必要なフィルター ドライバーは、送信をバイパスでき、受信機能。

フィルター ドライバーが関数を呼び出すときに、ドライバーの初期化中に、省略可能で、既定のエントリ ポイントを指定します、 [ **NdisFRegisterFilterDriver** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndisfregisterfilterdriver)関数。 エントリ ポイントは、 **NULL**関数で、既定では省略されます。 初期化の詳細については、次を参照してください。[フィルター ドライバーの初期化](initializing-a-filter-driver.md)します。

実行時にバイパスの状態を変更するには、ドライバーがのエントリ ポイントを指定する必要があります、 [ *FilterSetModuleOptions* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-filter_set_module_options)ドライバーの初期化中に機能します。 ドライバーを初期化できます、 [ **NDIS\_フィルター\_部分\_特性**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_filter_partial_characteristics)構造体し、する新しい特性を渡す、 [ **NdisSetOptionalHandlers** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndissetoptionalhandlers)のコンテキスト内で関数を*FilterSetModuleOptions*します。

NDIS 呼び出し、 *FilterSetModuleOptions*関数は、再起動操作の開始時に存在します。 フィルター ドライバーは、各フィルター モジュールを個別にバイパス モードを設定できます。 詳細については、次を参照してください。[フィルター モジュールの開始](starting-a-filter-module.md)します。

フィルター ドライバーは、次のオプションをバイパスできる*FilterXxx*関数で指定されている、 [ **NDIS\_フィルター\_ドライバー\_の特性**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_filter_driver_characteristics)構造体。

[*FilterSendNetBufferLists*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-filter_send_net_buffer_lists)

[*FilterSendNetBufferListsComplete*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-filter_send_net_buffer_lists_complete)

[*FilterCancelSendNetBufferLists*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-filter_cancel_send_net_buffer_lists)

[*FilterReturnNetBufferLists*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-filter_return_net_buffer_lists)

[*FilterReceiveNetBufferLists*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-filter_receive_net_buffer_lists)

設定する、 *FilterXxx*フィルター ドライバーを指定します、モードをバイパスする関数**NULL**関数のエントリ ポイント。 ただし、ドライバーが任意の NDIS 関数を呼び出す場合ですが、関連付けられている*FilterXxx*関数の場合、そのエントリ ポイントを提供する必要があります*FilterXxx*関数。 ドライバーを呼び出す場合など、 [ **NdisFIndicateReceiveNetBufferLists** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndisfindicatereceivenetbufferlists)関数を提供する必要がありますが、 [ *FilterReturnNetBufferLists* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-filter_return_net_buffer_lists)関数。

フィルター ドライバーが指定されている場合、 [ *FilterSendNetBufferLists* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-filter_send_net_buffer_lists)関数を送信要求をキューに配置する必要がありますも指定する必要が、 [ *FilterCancelSendNetBufferLists*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-filter_cancel_send_net_buffer_lists)関数。

フィルター ドライバーが指定されている場合、 [ *FilterReceiveNetBufferLists* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-filter_receive_net_buffer_lists)または[ **FilterReturnNetBufferLists** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-filter_return_net_buffer_lists)関数の場合、ドライバーの必要があります指定することも、 [ *FilterStatus* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-filter_status)関数。

実行時にバイパス モード設定を変更、フィルター ドライバーを呼び出すことができます、 [ **NdisFRestartFilter** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndisfrestartfilter)関数。 **NdisFRestartFilter**が指定されたフィルター モジュールの再起動操作している操作を一時停止をスケジュールします。 NDIS を呼び出すと*FilterSetModuleOptions*、フィルター ドライバーはそのフィルター モジュールの関数を呼び出すことで変更できる**NdisSetOptionalHandlers**エントリ ポイントの新しいセットを指定するとします。

**注**  一時停止と再起動、送信パス上にドロップするいくつかのネットワーク パケット、またはパス、またはその両方を受信します。 信頼性の高いトランスポート メカニズムを提供するネットワーク プロトコルがネットワークの場合は、損失パケットを I/O 操作を再試行可能性がありますが、信頼性を保証しないその他のプロトコルは、操作を再試行しないでください。

 

フィルター ドライバーは、オプションのドライバー サービスをサポートする追加の省略可能な関数を登録できます。 ドライバーはこれらの省略可能なサービスに登録、 [ *FilterSetOptions* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-set_options)関数。 これらの省略可能なサービスに関する詳細については、次を参照してください。[省略可能なフィルター ドライバー サービスを構成する](configuring-optional-filter-driver-services.md)します。

 

 





