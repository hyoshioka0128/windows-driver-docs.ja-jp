---
title: フィルター モジュールの起動
description: フィルター モジュールの起動
ms.assetid: 493cb922-22bc-4845-b5a2-6f610559534d
keywords:
- フィルターモジュール WDK ネットワーク、開始
- フィルターモジュールの開始
- フィルタードライバーの WDK ネットワーク、フィルターモジュールの開始
- NDIS フィルタードライバー WDK、フィルターモジュールの開始
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 98a33a249353b8af370c0b0f26849ad7158f1392
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72841834"
---
# <a name="starting-a-filter-module"></a>フィルター モジュールの起動





一時停止しているフィルターモジュールを開始するために、NDIS はフィルタードライバーの[*Filtersetmoduleoptions*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-filter_set_module_options)関数 (存在する場合) を呼び出した後、 [*filterrestart*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-filter_restart)関数を呼び出します。 フィルターモジュールは、 *Filterrestart*関数での実行の開始時に*再起動*状態になります。

ドライバーが[*Filtersetmoduleoptions*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-filter_set_module_options)のエントリポイントを提供した場合、ドライバーはフィルターモジュールの部分特性を変更できます。 詳細については、「[データバイパスモード](data-bypass-mode.md)」を参照してください。

フィルタードライバーの[*Filterrestart*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-filter_restart)関数を呼び出すと、ndis は、NDIS\_フィルターの**RestartAttributes**メンバー内のドライバーをフィルター処理するために、\_ndis にポインターを渡して[ **\_属性構造を再起動**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_restart_attributes)し[ **\_\_PARAMETERS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_filter_restart_parameters)構造体を再起動します。 フィルタードライバーは、基になるドライバーで指定されている再起動属性を変更できます。 再起動属性を変更する方法の詳細については、「 *Filterrestart*」を参照してください。

**注**  ndis は、スタック内の任意のフィルターモジュールに対して[*filterrestart*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-filter_restart)関数を呼び出す前に、スタック内のすべてのフィルターモジュールに対して[*filtersetmoduleoptions*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-filter_set_module_options)を呼び出します。

 

NDIS は、ドライバースタックを再起動するために、プラグアンドプレイ操作の一部としてフィルターモジュールを開始します。 ドライバースタックの再起動の概要については、「[ドライバースタックの再起動](restarting-a-driver-stack.md)」を参照してください。

*再起動*状態のフィルターモジュールの代わりに、フィルタードライバーは次のようになります。

-   通常の送信および受信操作を再開するために必要なすべての操作を完了します。

    送信操作と受信操作の詳細については、「[フィルターモジュールの送受信操作](filter-module-send-and-receive-operations.md)」を参照してください。

-   フィルターモジュールの構成可能なパラメーターの読み取りまたは書き込みを行うことができます。

-   ネットワークデータの表示を受信できます。 ドライバーは、このようなデータをコピーしてキューに置いて後でドライバーに示すことも、データを破棄することもできます。

-   新しい受信通知を開始することはできません。

-   では、 [**NdisFSendNetBufferListsComplete**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisfsendnetbufferlistscomplete)関数を呼び出すことによって、 [*filtersendnetbufferlists*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-filter_send_net_buffer_lists)関数に対して行われたすべての新しい送信要求を直ちに拒否する必要があります。 各[NET\_BUFFER\_LIST](net-buffer-list-structure.md)の完全な状態を NDIS\_status\_一時停止状態に設定する必要があります。

-   では、 [**NdisFIndicateStatus**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisfindicatestatus)関数を使用して状態を示すことができます。

    ステータスの表示の詳細については、「[フィルターモジュールの状態](filter-module-status-indications.md)の表示」を参照してください。

-   は、 [*FilterOidRequest*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-filter_oid_request)関数で OID 要求を処理する必要があります。

    OID 要求の詳細については、「[フィルターモジュール OID 要求](filter-module-oid-requests.md)」を参照してください。

-   新しい送信要求を開始することはできません。

-   [**NdisFReturnNetBufferLists**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisfreturnnetbufferlists)関数を呼び出すことによって、新しい受信通知を NDIS に直ちに返す必要があります。 必要に応じて、ドライバーはこのような受信表示をコピーしてから返すようにすることができます。

-   基になるドライバーに OID 要求を作成して、更新された構成情報を設定または照会することができます。

-   では、 [*Filterstatus*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-filter_status)関数の状態を処理する必要があります。

-   NDIS\_STATUS\_SUCCESS または failure status を示す必要があります。 フィルターモジュールが再起動されない場合は、NDIS によってデタッチされ、必須のフィルターの場合は、NDIS によってドライバースタック全体が終了します。

フィルタードライバーは、送信および受信操作を正常に再開した後、再起動操作を完了する必要があります。 フィルタードライバーは、NDIS\_STATUS\_SUCCESS または NDIS\_STATUS\_[*Filterrestart*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-filter_restart)から返されることによって、同期または非同期的に再起動操作を完了できます。

ドライバーが NDIS\_STATUS\_PENDING を返した場合、再起動操作の完了後に[**NdisFRestartComplete**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisfrestartcomplete)関数を呼び出す必要があります。 この場合、ドライバーは再起動操作の最終ステータスを**NdisFRestartComplete**に渡します。

再起動操作が完了すると、フィルターモジュールは [*実行中*] 状態になります。 ドライバーは、通常の送受信処理を再開します。

NDIS は、フィルタードライバーが*再起動*中の間に、要求、アタッチ、デタッチ、一時停止などの他のプラグアンドプレイ操作を開始しません。 NDIS は、フィルタードライバーが*実行中*の状態になった後に、一時停止要求を開始できます。 フィルターモジュールの一時停止の詳細については、「[フィルターモジュールの一時停止](pausing-a-filter-module.md)」を参照してください。

 

 





