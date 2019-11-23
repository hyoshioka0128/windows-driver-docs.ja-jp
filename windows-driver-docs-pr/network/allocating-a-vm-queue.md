---
title: VM キューの割り当て
description: VM キューの割り当て
ms.assetid: 2645a6e5-3824-469c-84d5-8e49fa01f494
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: b1a1d0fec4665ac6c690687f62530f37d3cc9764
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72835389"
---
# <a name="allocating-a-vm-queue"></a>VM キューの割り当て





構成パラメーターの初期セットを使用してキューを割り当てるには、後のドライバーが\_キューメソッド OID 要求を[割り当てる\_\_フィルターを受け取る oid を\_](https://docs.microsoft.com/windows-hardware/drivers/network/oid-receive-filter-allocate-queue)します。 [**Ndis\_OID\_要求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)構造体の**informationbuffer**メンバーには、最初に[**ndis\_RECEIVE\_QUEUE\_PARAMETERS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_receive_queue_parameters)構造体へのポインターが含まれています。 OID メソッド要求から正常に戻った後、 **ndis\_oid\_要求**構造の**informationbuffer**メンバーには、新しいキュー識別子と MSI-X テーブルエントリを持つ**ndis\_RECEIVE\_queue\_PARAMETERS**構造体へのポインターが含まれています。

[**NDIS\_receive\_queue\_PARAMETERS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_receive_queue_parameters)構造体は、\_キュー OID の[割り当て\_フィルターを受信](https://docs.microsoft.com/windows-hardware/drivers/network/oid-receive-filter-allocate-queue)\_、oid\_\_[フィルター\_キュー\_パラメーター](https://docs.microsoft.com/windows-hardware/drivers/network/oid-receive-filter-queue-parameters) oid を受け取る oid\_で使用されます。 VM キューのパラメーターの詳細については、「 [Vm キューのパラメーターの取得と更新](obtaining-and-updating-vm-queue-parameters.md)」を参照してください。

前のドライバーは、次のキュー構成パラメーターを使用して、 [ **\_キュー\_パラメーター構造を受け取る NDIS\_** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_receive_queue_parameters)を初期化します。

-   キューの種類 ( [**NDIS\_は、\_queue\_type 列挙型**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ne-ntddndis-_ndis_receive_queue_type)) を受信します。

-   キューのプロセッサ関係。

-   キュー名と仮想マシン名。

-   先読み分割パラメーター。

    **注**  NDIS 6.30 以降では、パケットデータを個別の先読みバッファーに分割することはサポートされなくなりました。

     

このような場合は、\_キュー\_パラメーターを受け取るように[ **、ndis を**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_receive_queue_parameters)\_設定できます。**これ  、** \_キュー\_受信\_キューに\_を受信\_パラメーターを受け取る\_、\_の\_を受信\_\_の**フラグ**のメンバーで\_必要なフラグを\_\_受信に渡す必要があります。 その他のフラグは、キューの割り当てには使用されません。

 

NDIS は、受信キューの割り当てに OID 要求を受信すると、キューパラメーターを確認します。 NDIS によって必要なリソースとキュー識別子が割り当てられると、基になるミニポートドライバーに OID 要求が送信されます。 キュー識別子は、関連付けられているネットワークアダプターに対して一意です。

ミニポートドライバーが受信キューに必要なソフトウェアとハードウェアリソースを正常に割り当てることができる場合は、正常終了の状態で OID 要求を完了します。

Ndis は、この OID 要求をミニポートドライバーに送信する前に、Ndis の**Queueid**メンバーにキュー識別子を割り当てて、 [ **\_queue\_PARAMETERS 構造体\_受信**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_receive_queue_parameters)し、そのメソッド要求をミニポートドライバーに渡します。 ミニポートドライバーは、 **MSIXTableEntry**メンバーに MSI-X テーブルエントリを提供します。

ミニポートドライバーは、割り当てられた受信キューのキュー識別子を保持する必要があります。 NDIS は、受信キューのキュー識別子を使用して、ミニポートドライバーを呼び出して受信キューに受信フィルターを設定したり、受信キューパラメーターを変更したり、受信キューを解放したりします。

既定のキュー (キュー識別子ゼロ) は常に割り当てられている  解放できない**ことに注意**してください。

 

その後のドライバーでは、その後の OID 要求で NDIS が提供するキュー識別子を使用する必要があります。たとえば、キューパラメーターを変更したり、キューを解放したりできます。 キュー id は、キューに関連付けられているすべての[**NET\_BUFFER\_リスト**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer_list)構造の OOB データにも含まれます。 ドライバーは、net [ **\_buffer\_list\_受信\_queue\_ID**](https://docs.microsoft.com/windows-hardware/drivers/network/net-buffer-list-receive-queue-id)マクロを使用して、NET\_BUFFER\_LIST 構造体のキュー識別子を取得します。

プロトコルドライバーでは、キューが正常に割り当てられてからキューが削除されるまで、いつでも VMQ フィルターを設定でき  ことに**注意**してください。

 

プロトコルドライバーは、キューの割り当てを完了するための完全なメソッド OID 要求[\_、\_フィルター\_キュー\_割り当て\_受信する oid](https://docs.microsoft.com/windows-hardware/drivers/network/oid-receive-filter-queue-allocation-complete)を発行します。 割り当てが完了すると、ミニポートドライバーは共有メモリおよびその他のリソースを割り当てることができます。 共有メモリリソースの割り当ての詳細については、「[共有メモリリソースの割り当て](shared-memory-resource-allocation.md)」を参照してください。

ミニポートドライバーが OID を受信した後\_フィルター\_キュー\_割り当て OID 要求を受信して正常に処理する\_、キューは*割り当て済み*の状態になります。 キューの状態の詳細については、「[キューの状態と操作](queue-states-and-operations.md)」を参照してください。

1つ以上の受信キューが割り当てられた後に、必要に応じて最初のフィルターを設定した後は、Oid を発行して、受信キューの現在のバッチの割り当てが完了したことをミニポートドライバーに通知するために、Oid 要求の[\_フィルター\_キュー\_\_割り当てを\_](https://docs.microsoft.com/windows-hardware/drivers/network/oid-receive-filter-queue-allocation-complete)必要があります。

そのキューにフィルターが設定されていない場合、ミニポートドライバーは受信キューにあるパケットを保持しないようにする必要があります。 キューにフィルターが設定されていない場合、またはすべてのフィルターがオフになっている場合は、キューを空にして、すべてのパケットを破棄する必要があります。 つまり、ドライバースタックが示されていないか、キューに保持されていません。

その後のドライバーでは、Oid を使用して[\_フィルターを受信し\_\_キュー](https://docs.microsoft.com/windows-hardware/drivers/network/oid-receive-filter-free-queue) oid を使用して、割り当てたキューを解放\_ます。 キューの解放の詳細については、「 [VM キューの解放](freeing-a-vm-queue.md)」を参照してください。

 

 





