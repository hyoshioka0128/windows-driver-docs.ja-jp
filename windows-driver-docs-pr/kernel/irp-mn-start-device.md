---
title: IRP_MN_START_DEVICE
description: すべての PnP ドライバーは、この IRP を処理する必要があります。
ms.date: 08/12/2017
ms.assetid: 0aac1346-b5c7-4dcc-ab86-03e8fd151505
keywords:
- IRP_MN_START_DEVICE カーネルモードドライバーのアーキテクチャ
ms.localizationpriority: medium
ms.openlocfilehash: 5c461c2e52b1c6a37bc079a9114a5761bcc78ba2
ms.sourcegitcommit: 7681ac46c42782602bd3449d61f7ed4870ef3ba7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/07/2020
ms.locfileid: "82922518"
---
# <a name="irp_mn_start_device"></a>IRP\_の\_全\_開始デバイス


すべての PnP ドライバーは、この IRP を処理する必要があります。

## <a name="value"></a>値

0x00

<a name="major-code"></a>主要コード
----------

[**IRP\_MJ\_PNP**](irp-mj-pnp.md)

<a name="when-sent"></a>送信時
---------

PnP マネージャーは、デバイスにハードウェアリソースが割り当てられた後、この IRP を送信します。 デバイスが最近列挙され、初めて起動されているか、リソースの再調整のために停止した後にデバイスが再起動している可能性があります。

場合によっては、PnP マネージャーが、既に開始されているデバイスに**IRP\_\_\_** を使用した開始デバイスを送信し、デバイスが現在使用しているものとは異なるリソースのセットを提供することがあります。 ドライバーは、 [**IoInvalidateDeviceState**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ioinvalidatedevicestate)を呼び出して、pnp\_\_リソース要件\_を変更したフラグが設定された後続の IRP [**\_\_クエリ\_PNP\_デバイス\_状態**](irp-mn-query-pnp-device-state.md)要求に応答することによって、このアクションを開始します。 バスドライバーでは、このメカニズムを使用して、たとえば PCI から PCI へのブリッジで新しいアパーチャを開くことができます。

PnP マネージャーは、システムスレッドのコンテキストで\_この IRP を IRQL パッシブレベルで送信します。

## <a name="input-parameters"></a>入力パラメーター


[**IO\_スタック\_の場所**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_io_stack_location)構造の**AllocatedResources**メンバーは、PnP マネージャーによってデバイスに割り当てられたハードウェアリソースを説明する[**\_CM リソース\_リスト**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_cm_resource_list)を指します。 この一覧には、未加工の形式のリソースが含まれています。 生のリソースを使用してデバイスをプログラミングします。

**AllocatedResourcesTranslated**は、PnP マネージャーによってデバイスに割り当てられたハードウェアリソースが記述されている[**CM\_リソース\_リスト**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_cm_resource_list)を指します。 この一覧には、翻訳された形式のリソースが含まれています。 変換されたリソースを使用して、割り込みベクター、map i/o space、および map メモリを接続します。

## <a name="output-parameters"></a>出力パラメーター


None

## <a name="io-status-block"></a>I/O ステータス ブロック


ドライバーは、 **Irp-&gt;iostatus**を、状態が\_SUCCESS に設定されるか、または状態\_が "失敗\_"\_や "不足しているリソース" などの適切なエラー状態に設定されます。

ドライバーがデバイスに対して開始操作を実行するのに時間がかかる場合、IRP を保留中とし\_てマークし、状態を保留中に戻すことができます。

<a name="operation"></a>Operation
---------

この IRP は、デバイスの親バスドライバーによって最初に処理され、その後、デバイススタック内の上位の各ドライバーによって処理される必要があります。

この IRP に応答して、ドライバーはデバイスを初めて起動するか、停止したデバイスを再起動します。 デバイスを起動するために必要な操作は、デバイスによって異なりますが、デバイスの電源をオンにしたり、デバイス固有の初期化を実行したり、割り込みを接続したりすることができます。

ドライバーは、通常、デバイスを初めて起動するか、 [**irp\_\_の停止\_**](irp-mn-stop-device.md)後にデバイスを再起動する場合と同じ方法で、この irp を処理できます。ただし、ドライバーが停止後に再起動時にデバイスの状態を復元する必要がある場合を除きます。

Windows Vista 以降のオペレーティングシステムでは、ドライバーが**irp\_\_を\_開始するデバイス**の irp を常に保留し、後で処理を完了することをお勧めします。 この順序を使用すると、システムはデバイスの再起動を非同期に処理できます。 (Windows Vista より前のオペレーティングシステムでは、ドライバー\_はディスパッチルーチンから保留状態を返すことができますが、PnP マネージャーはデバイスの再起動とその他の操作で重複しません)。

開始 IRP の処理の詳細については、「[デバイスを開始する](https://docs.microsoft.com/windows-hardware/drivers/kernel/starting-a-device)」を参照してください。

**この IRP を送信しています**

システムで使用するために予約されています。 ドライバーは、この IRP を送信することはできません。

<a name="requirements"></a>必要条件
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>ヘッダー</p></td>
<td>Wdm.h (Wdm.h、Ntddk.h、Ntifs.h を含む)</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>関連項目


[**IRP\_の\_全\_停止デバイス**](irp-mn-stop-device.md)

 

 




