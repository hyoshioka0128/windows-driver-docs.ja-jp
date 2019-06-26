---
title: Storport のキュー管理
description: Storport のキュー管理
ms.assetid: 29fddcac-abc9-4aa4-8485-56120805ae34
keywords:
- Storport ドライバー WDK、キューの管理
- WDK Storport のキュー
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8f84c0dd1a69eab9e97f7150c9030eb0708d6c8b
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67386118"
---
# <a name="storport-queue-management"></a>Storport のキュー管理


## <span id="ddk_storport_queue_management_kg"></span><span id="DDK_STORPORT_QUEUE_MANAGEMENT_KG"></span>


高パフォーマンス記憶域アダプターの機能を利用するには、ミニポート ドライバーは、自分のデバイスのキューの一時停止と再開の効率を最大化するための方法でこれらのキューを制御する必要があります。

SCSI ポート キュー モデルでは、キューの管理は、ポート、ドライバーの排他ドメインです。 Storport キュー モデルでは、ポート、ドライバーは、ミニポート ドライバーに大量のキューの管理制御を提供するいくつかのキュー管理サポート ルーチンを提供します。

Storport キュー モデルですべての要求は lun ごとのキューでポート ドライバーでキューに登録します。 拡張の SRB サポートのない論理ユニットごとに 255 未処理の要求の最大ことができます。 それ以外の場合、キューの深さは、使用可能なシステム リソースまたはアダプターの機能によってのみ制限されます。 キューの深さが設定された制限に達すると、Storport は未処理の要求ユニットの数が最大のキューを下回るまで、その論理単位にそれ以降の要求を保持します。

アダプターが持つことができます、未処理の要求の数に Storport から定義済みの制限はありません。 たとえば、255 のキューの深さで接続して論理ユニットを 55 でアダプターでした投稿 14,025 (55 x 255) の最大要求一度に。 ポート ドライバーのキューのモデルの説明については、次の図を参照してください。

![ポート ドライバーのキューのモデルを示す図](images/queues.png)

ドライバーのキューのモデルをポートします。

システムに、ミニポート ドライバーの呼び出し、アダプターと論理ユニットが両方の要求を受信できる状態にある場合、 [ **HwStorBuildIo** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/storport/nc-storport-hw_buildio)と[ **HwStorStartIo**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/storport/nc-storport-hw_startio)ルーチンをこの順序で。

SCSI ポートとは異なりは、Storport は、ビジー状態のポート ドライバーに通知するミニポート ドライバーを許可します。 これらの通信は、論理ユニットまたはアダプターのいずれかの一時停止またはビジー状態のシグナルのミニポート ドライバーを許可する次の 8 つルーチンによって処理されます。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">Storport ルーチン</th>
<th align="left">実行されるアクション</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/storport/nf-storport-storportpausedevice" data-raw-source="[&lt;strong&gt;StorPortPauseDevice&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/storport/nf-storport-storportpausedevice)"><strong>StorPortPauseDevice</strong></a></p></td>
<td align="left"><p>一定の時間には、デバイスを停止します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/storport/nf-storport-storportresumedevice" data-raw-source="[&lt;strong&gt;StorPortResumeDevice&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/storport/nf-storport-storportresumedevice)"><strong>StorPortResumeDevice</strong></a></p></td>
<td align="left"><p>一時停止しているデバイスを再開します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/storport/nf-storport-storportpause" data-raw-source="[&lt;strong&gt;StorPortPause&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/storport/nf-storport-storportpause)"><strong>StorPortPause</strong></a></p></td>
<td align="left"><p>アダプターを一定の時間に停止します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/storport/nf-storport-storportresume" data-raw-source="[&lt;strong&gt;StorPortResume&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/storport/nf-storport-storportresume)"><strong>StorPortResume</strong></a></p></td>
<td align="left"><p>一時停止中のアダプターを再開します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/storport/nf-storport-storportdevicebusy" data-raw-source="[&lt;strong&gt;StorPortDeviceBusy&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/storport/nf-storport-storportdevicebusy)"><strong>StorPortDeviceBusy</strong></a></p></td>
<td align="left"><p>いることをデバイス ビジー デバイスのキューが指定された数の I/O 要求を完了するまで。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/storport/nf-storport-storportdeviceready" data-raw-source="[&lt;strong&gt;StorPortDeviceReady&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/storport/nf-storport-storportdeviceready)"><strong>StorPortDeviceReady</strong></a></p></td>
<td align="left"><p>もう一度要求を受信する準備がビジー状態のデバイスを確認します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/storport/nf-storport-storportbusy" data-raw-source="[&lt;strong&gt;StorPortBusy&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/storport/nf-storport-storportbusy)"><strong>StorPortBusy</strong></a></p></td>
<td align="left"><p>アダプター ビジー状態までように指定された数の I/O 要求が完了します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/storport/nf-storport-storportready" data-raw-source="[&lt;strong&gt;StorPortReady&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/storport/nf-storport-storportready)"><strong>StorPortReady</strong></a></p></td>
<td align="left"><p>もう一度要求を受信する準備がビジー状態のアダプターを確認します。</p></td>
</tr>
</tbody>
</table>

 

デバイスが一時停止またはビジー状態の間は、ポート ドライバーなし要求をデバイスに送信します。 ミニポート ドライバーがビジー状態で要求が完了したかどうか (SRB\_状態\_ビジーまたは SCSISTAT\_ビジー)、ポート ドライバーは、不特定数の要求が失敗するまでの時間を要求を再試行またはが完了します。

SCSI ポートのキューのモデルでは使用できないキューの明示的な管理のルーチンのセットを提供するだけでなく、Storport キュー モデルは、SCSI ポートを使用する暗黙的なキュー管理ルーチンを使用しません。 具体的には、 **NextRequest**と**NextLuRequest**通知は無視されます。

 

 




