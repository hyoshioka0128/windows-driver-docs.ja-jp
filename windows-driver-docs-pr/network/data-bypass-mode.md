---
title: データ バイパス モード
description: データ バイパス モード
ms.assetid: 98061803-22de-4fa2-8582-2d382f84dd75
keywords:
- フィルタードライバー WDK ネットワーク、データバイパスモード
- NDIS フィルタードライバー WDK、データバイパスモード
- データバイパスモード WDK ネットワーク
- バイパスモード WDK ネットワーク
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d84b72157aa7e54d084d68dba326e263cf4876f8
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72838173"
---
# <a name="data-bypass-mode"></a>データ バイパス モード





フィルタードライバー*データバイパスモード*は、システムパフォーマンスを向上させることができます。 NDIS は、バイパスされる*Filterxxx*関数を呼び出しません。 たとえば、特定のフィルターアプリケーションで送信サービスと受信サービスが不要な場合、フィルタードライバーは送信機能と受信機能をバイパスできます。

フィルタードライバーは、 [**NdisFRegisterFilterDriver**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisfregisterfilterdriver)関数を呼び出すときに、ドライバーの初期化中にバイパスできる関数の既定のエントリポイントを指定します。 既定でバイパスされる関数の場合、エントリポイントは**NULL**になります。 初期化の詳細については、「[フィルタードライバーの初期化](initializing-a-filter-driver.md)」を参照してください。

実行時にバイパス状態を変更するには、ドライバーの初期化中に、 [*Filtersetmoduleoptions*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-filter_set_module_options)関数のエントリポイントを指定する必要があります。 ドライバーは、 [**NDIS\_フィルター\_部分的な\_特性**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_filter_partial_characteristics)の構造を初期化し、 *Filtersetmoduleoptions*のコンテキスト内から新しい特性を[**NdisSetOptionalHandlers**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndissetoptionalhandlers)関数に渡すことができます。

NDIS は、再起動操作の開始時に*Filtersetmoduleoptions*関数を呼び出します (存在する場合)。 フィルタードライバーは、フィルターモジュールごとにバイパスモードを個別に設定できます。 詳細については、「[フィルターモジュールを開始する](starting-a-filter-module.md)」を参照してください。

フィルタードライバーは、 [**NDIS\_フィルター\_ドライバー\_特性**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_filter_driver_characteristics)の構造に指定されている次のオプションの*filterxxx*関数をバイパスできます。

[*FilterSendNetBufferLists*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-filter_send_net_buffer_lists)

[*FilterSendNetBufferListsComplete*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-filter_send_net_buffer_lists_complete)

[*FilterCancelSendNetBufferLists*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-filter_cancel_send_net_buffer_lists)

[*FilterReturnNetBufferLists*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-filter_return_net_buffer_lists)

[*FilterReceiveNetBufferLists*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-filter_receive_net_buffer_lists)

*Filterxxx*関数をバイパスモードに設定するには、フィルタードライバーでその関数のエントリポイントに**NULL**を指定します。 ただし、 *Filterxxx*関数に関連付けられているいずれかの NDIS 関数をドライバーが呼び出す場合は、その*filterxxx*関数のエントリポイントを提供する必要があります。 たとえば、ドライバーが[**NdisFIndicateReceiveNetBufferLists**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisfindicatereceivenetbufferlists)関数を呼び出す場合は、 [*filterreturnnetbufferlists*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-filter_return_net_buffer_lists)関数を指定する必要があります。

フィルタードライバーが[*Filtersendnetbufferlists*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-filter_send_net_buffer_lists)関数を指定し、送信要求をキューに置いている場合は、 [*filtercancelsendnetbufferlists*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-filter_cancel_send_net_buffer_lists)関数も指定する必要があります。

フィルタードライバーで[*FilterReceiveNetBufferLists*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-filter_receive_net_buffer_lists)関数または[**filterreturnnetbufferlists**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-filter_return_net_buffer_lists)関数が指定されている場合、ドライバーは[*filterstatus*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-filter_status)関数も指定する必要があります。

実行時にバイパスモードの設定を変更するには、フィルタードライバーで[**NdisFRestartFilter**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisfrestartfilter)関数を呼び出すことができます。 **NdisFRestartFilter**は、指定されたフィルターモジュールの再起動操作の後に一時停止操作をスケジュールします。 NDIS が*Filtersetmoduleoptions*を呼び出した場合、フィルタードライバーは**NdisSetOptionalHandlers**を呼び出し、エントリポイントの新しいセットを指定することによって、そのフィルターモジュールの関数を変更できます。

  一時停止と再起動により、一部のネットワークパケットが送信パスまたは受信パス、またはその両方にドロップされる可能性がある**ことに注意**してください。 信頼できるトランスポート機構を提供するネットワークプロトコルは、パケットが失われた場合にネットワーク i/o 操作を再試行することがありますが、信頼性を保証しない他のプロトコルは操作を再試行しません。

 

フィルタードライバーは、オプションのドライバーサービスをサポートする追加のオプション関数を登録できます。 ドライバーは、これらのオプションのサービスを[*FilterSetOptions*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-set_options)関数に登録します。 これらのオプションサービスの詳細については、「[オプションフィルタードライバーサービスの構成](configuring-optional-filter-driver-services.md)」を参照してください。

 

 





