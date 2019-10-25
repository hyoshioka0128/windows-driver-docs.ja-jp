---
title: IRP_MN_START_DEVICE
description: すべての PnP ドライバーは、この IRP を処理する必要があります。
ms.date: 08/12/2017
ms.assetid: 0aac1346-b5c7-4dcc-ab86-03e8fd151505
keywords:
- IRP_MN_START_DEVICE カーネルモードドライバーのアーキテクチャ
ms.localizationpriority: medium
ms.openlocfilehash: 23ca09dabcc2000a75662db4a632a0ffc3908cb9
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72827946"
---
# <a name="irp_mn_start_device"></a>\_デバイスを起動\_IRP\_


すべての PnP ドライバーは、この IRP を処理する必要があります。

<a name="major-code"></a>主要コード
----------

[**IRP\_MJ\_PNP**](irp-mj-pnp.md)送信時
---------

PnP マネージャーは、デバイスにハードウェアリソースが割り当てられた後、この IRP を送信します。 デバイスが最近列挙され、初めて起動されているか、リソースの再調整のために停止した後にデバイスが再起動している可能性があります。

PnP マネージャーが、既に開始されているデバイスに\_デバイスを起動して、現在使用されているものとは異なるリソースのセットを提供することにより、IRP\_が実行されている場合は、そのデバイスに対して**デバイスを起動\_** ドライバーは、 [**IoInvalidateDeviceState**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ioinvalidatedevicestate)を呼び出し、PNP\_リソースを使用して、後続の[**IRP\_\_クエリ\_pnp\_デバイス\_状態**](irp-mn-query-pnp-device-state.md)要求に応答することによって、このアクションを開始\_要件\_フラグセットが変更されました。 バスドライバーでは、このメカニズムを使用して、たとえば PCI から PCI へのブリッジで新しいアパーチャを開くことができます。

PnP マネージャーは、システムスレッドのコンテキストでこの IRP を IRQL パッシブ\_レベルで送信します。

## <a name="input-parameters"></a>入力パラメーター


[**IO\_スタック\_の場所**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_io_stack_location)の構造体の AllocatedResources メンバーは、 [**CM\_リソース\_リスト**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_cm_resource_list)を指します。この一覧には、PnP マネージャーによって割り当てられたハードウェアリソースが記述されて**います。** ドライブ. この一覧には、未加工の形式のリソースが含まれています。 生のリソースを使用してデバイスをプログラミングします。

**AllocatedResourcesTranslated**は、PnP マネージャーによってデバイスに割り当てられたハードウェアリソースが記述されている[**CM\_リソース\_リスト**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_cm_resource_list)を指します。 この一覧には、翻訳された形式のリソースが含まれています。 変換されたリソースを使用して、割り込みベクター、map i/o space、および map メモリを接続します。

## <a name="output-parameters"></a>出力パラメーター


なし

## <a name="io-status-block"></a>I/O ステータス ブロック


ドライバーは、 **Irp&gt;iostatus. status**を STATUS\_SUCCESS に設定します。または、状態\_失敗、状態\_不足しているリソース\_リソースなど、適切なエラー状態に設定します。

ドライバーがデバイスの開始操作を実行するのに時間がかかる場合は、IRP pending および return STATUS\_PENDING としてマークできます。

<a name="operation"></a>操作
---------

この IRP は、デバイスの親バスドライバーによって最初に処理され、その後、デバイススタック内の上位の各ドライバーによって処理される必要があります。

この IRP に応答して、ドライバーはデバイスを初めて起動するか、停止したデバイスを再起動します。 デバイスを起動するために必要な操作は、デバイスによって異なりますが、デバイスの電源をオンにしたり、デバイス固有の初期化を実行したり、割り込みを接続したりすることができます。

通常、ドライバーは、デバイスを初めて起動するか、または[**irp\_\_\_** ](irp-mn-stop-device.md)完了後にデバイスを再起動した場合と同じ方法で、この irp を処理できます。ただし、ドライバーが停止後に再起動時にデバイスの状態を復元する必要がある場合を除きます。

Windows Vista 以降のオペレーティングシステムでは、デバイスの irp\_開始し、後で処理を完了するために、ドライバーは常に**irp\_** を保留\_ことをお勧めします。 この順序を使用すると、システムはデバイスの再起動を非同期に処理できます。 (Windows Vista より前のオペレーティングシステムでは、ドライバーはディスパッチルーチンから状態\_PENDING を返すことができますが、その他の操作では、PnP マネージャーがデバイスの再起動と重複することはありません)。

開始 IRP の処理の詳細については、「[デバイスを開始する](https://docs.microsoft.com/windows-hardware/drivers/kernel/starting-a-device)」を参照してください。

**この IRP を送信しています**

システム用に予約されています。 ドライバーは、この IRP を送信することはできません。

<a name="requirements"></a>要件
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>Header</p></td>
<td>Wdm (Wdm .h、Ntddk、または Ntifs を含む)</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>関連項目


[**IRP\_\_\_デバイスの停止**](irp-mn-stop-device.md)

 

 




