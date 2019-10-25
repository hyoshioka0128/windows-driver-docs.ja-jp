---
title: Storport のキュー管理
description: Storport のキュー管理
ms.assetid: 29fddcac-abc9-4aa4-8485-56120805ae34
keywords:
- Storport ドライバー WDK、キュー管理
- WDK Storport をキューに置いてください
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2c883d3f0ccde0b12bae7f0cb390fcde787483cd
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72844458"
---
# <a name="storport-queue-management"></a>Storport のキュー管理


## <span id="ddk_storport_queue_management_kg"></span><span id="DDK_STORPORT_QUEUE_MANAGEMENT_KG"></span>


高パフォーマンスの記憶域アダプターの機能を利用するには、ミニポートドライバーがデバイスキューを管理する必要があります。これらのキューの一時停止と再開は、効率を最大化する方法で行う必要があります。

SCSI ポートキューモデルでは、キュー管理はポートドライバーの排他的ドメインです。 Storport キューモデルでは、ポートドライバーに複数のキュー管理サポートルーチンが用意されています。これにより、ミニポートドライバーは大量のキュー管理制御を行うことができます。

Storport キューモデルでは、すべての要求は論理ユニットごとのキューのポートドライバーでキューに登録されます。 拡張 SRB をサポートしていない場合、各論理ユニットは最大255の未処理の要求を持つことができます。 それ以外の場合、キューの深さは、使用可能なシステムリソースまたはアダプターの機能によってのみ制限されます。 キューの深さに制限が設定されている場合、その論理ユニットに対する未処理の要求の数がキューの最大値を下回るまで、Storport はその論理ユニットに対してさらに要求を保持します。

アダプターが持つことができる未処理の要求の数には、Storport からの定義済みの制限はありません。 たとえば、55論理ユニットが接続されているアダプタで、キューの深さが255の場合、一度に最大 14025 (55 x 255) 要求が送信される可能性があります。 ポートドライバーのキューモデルの説明については、次の図を参照してください。

![ポートドライバーのキューモデルを示す図](images/queues.png)

ポートドライバーのキューモデル

アダプターと論理ユニットの両方で要求を受信する準備が整っている場合、システムはミニポートドライバーの[**HwStorBuildIo**](https://docs.microsoft.com/windows-hardware/drivers/ddi/storport/nc-storport-hw_buildio)ルーチンと[**HwStorStartIo**](https://docs.microsoft.com/windows-hardware/drivers/ddi/storport/nc-storport-hw_startio)ルーチンをこの順序で呼び出します。

SCSI ポートとは異なり、Storport はミニポートドライバーがポートドライバーにビジー状態の状態を通知することを許可します。 これらの通信は、次の8つのルーチンによって処理されます。これにより、論理ユニットまたはアダプターが一時停止中またはビジー状態のときにミニポートドライバーが通知を行うことができます。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">Storport ルーチン</th>
<th align="left">実行されたアクション</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/storport/nf-storport-storportpausedevice" data-raw-source="[&lt;strong&gt;StorPortPauseDevice&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/storport/nf-storport-storportpausedevice)"><strong>StorPortPauseDevice</strong></a></p></td>
<td align="left"><p>指定した期間だけデバイスを一時停止します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/storport/nf-storport-storportresumedevice" data-raw-source="[&lt;strong&gt;StorPortResumeDevice&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/storport/nf-storport-storportresumedevice)"><strong>StorPortResumeDevice</strong></a></p></td>
<td align="left"><p>一時停止しているデバイスを再開します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/storport/nf-storport-storportpause" data-raw-source="[&lt;strong&gt;StorPortPause&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/storport/nf-storport-storportpause)"><strong>StorPortPause</strong></a></p></td>
<td align="left"><p>指定した期間だけアダプターを一時停止します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/storport/nf-storport-storportresume" data-raw-source="[&lt;strong&gt;StorPortResume&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/storport/nf-storport-storportresume)"><strong>StorPortResume</strong></a></p></td>
<td align="left"><p>一時停止しているアダプターを再開します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/storport/nf-storport-storportdevicebusy" data-raw-source="[&lt;strong&gt;StorPortDeviceBusy&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/storport/nf-storport-storportdevicebusy)"><strong>StorPortDeviceBusy</strong></a></p></td>
<td align="left"><p>デバイスキューが指定された数の i/o 要求を完了するまで、デバイスがビジー状態になるようにします。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/storport/nf-storport-storportdeviceready" data-raw-source="[&lt;strong&gt;StorPortDeviceReady&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/storport/nf-storport-storportdeviceready)"><strong>StorPortDeviceReady</strong></a></p></td>
<td align="left"><p>ビジー状態のデバイスで要求を再度受信できるようにします。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/storport/nf-storport-storportbusy" data-raw-source="[&lt;strong&gt;StorPortBusy&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/storport/nf-storport-storportbusy)"><strong>StorPortBusy</strong></a></p></td>
<td align="left"><p>指定された数の i/o 要求を完了するまで、アダプターがビジー状態になるようにします。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/storport/nf-storport-storportready" data-raw-source="[&lt;strong&gt;StorPortReady&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/storport/nf-storport-storportready)"><strong>StorPortReady</strong></a></p></td>
<td align="left"><p>ビジー状態のアダプターで要求を再度受信できるようにします。</p></td>
</tr>
</tbody>
</table>

 

デバイスが一時停止中またはビジー状態のとき、ポートドライバーはデバイスに要求を送信しません。 ミニポートドライバーが、ビジー状態の要求 (SRB\_STATUS\_BUSY または SCSISTAT\_BUSY) を完了した場合、ポートドライバーは要求が失敗するか、完了するまで無期限に要求を再試行します。

SCSI ポートキューモデルでは使用できない一連の明示的なキュー管理ルーチンを指定するだけでなく、Storport キューモデルでは、SCSI ポートが使用する暗黙的なキュー管理ルーチンは使用しません。 特に、 **nextrequest**と**nextlurequest**の通知は無視されます。

 

 




