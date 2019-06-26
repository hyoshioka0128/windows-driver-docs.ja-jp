---
title: StorPort ミニポート ドライバーのレジストリ エントリ
description: StorPort では、StorPort およびミニポートの操作の動作を構成するレジストリ エントリのセットを定義します。
ms.assetid: 543EC6A4-113C-4525-8063-28854B50760E
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: a122a246d60b796d9b00295256368522a01e8808
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67368943"
---
# <a name="registry-entries-for-storport-miniport-drivers"></a>StorPort ミニポート ドライバーのレジストリ エントリ


StorPort では、StorPort およびミニポートの操作の動作を構成するレジストリ エントリのセットを定義します。 スコープのミニポート ドライバーまたはインスタンスごとに値が設定されます。

## <a name="span-idserviceentriesspanspan-idserviceentriesspanspan-idserviceentriesspanservice-entries"></a><span id="Service_Entries"></span><span id="service_entries"></span><span id="SERVICE_ENTRIES"></span>サービスのエントリ


ミニポートのレジストリ エントリはによってキー指定され、 *\\パラメーター*サブキー、 *\\パラメーター\\デバイス*ミニポートのサービス キーのサブキー。 、個々 のアダプターのエントリのサブキーが拡張され、アダプターのインデックスをなど、 *\\パラメーター\\Device1*します。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left">名前</td>
<td align="left"><strong>DriverParameter</strong></td>
</tr>
<tr class="even">
<td align="left">種類</td>
<td align="left">任意</td>
</tr>
<tr class="odd">
<td align="left">パス</td>
<td align="left"><p>ミニポート スコープ:</p>
<p>HKLM\System\CurrentControlSet\Services&lt;miniport name&gt;\Parameters\Device</p>
<p>アダプターのスコープ:</p>
<p>Hklm \system\currentcontrolset\services&lt;ミニポート名&gt;\Parameters\Device&lt;アダプター #&gt;</p></td>
</tr>
<tr class="even">
<td align="left">Value</td>
<td align="left"><p>ミニポート特定データ。</p></td>
</tr>
<tr class="odd">
<td align="left">説明</td>
<td align="left"><p>Storport がこのレジストリ データを取得し、としてミニポートにバッファーを渡します<em>パラメーター</em>ミニポートの呼び出し時に<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/storport/nc-storport-hw_find_adapter" data-raw-source="[&lt;strong&gt;HwStorFindAdapter&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/storport/nc-storport-hw_find_adapter)"> <strong>HwStorFindAdapter</strong> </a>ルーチン。</p></td>
</tr>
<tr class="even">
<td align="left">適用対象します。</td>
<td align="left"><p>Windows Server 2003 で開始しています。</p></td>
</tr>
</tbody>
</table>

 

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left">名前</td>
<td align="left"><strong>LinkDownTimeoutValue</strong></td>
</tr>
<tr class="even">
<td align="left">種類</td>
<td align="left">REG_DWORD</td>
</tr>
<tr class="odd">
<td align="left">パス</td>
<td align="left"><p>ミニポート スコープ:</p>
<p>HKLM\System\CurrentControlSet\Services&lt;miniport name&gt;\Parameters\Device</p>
<p>アダプターのスコープ:</p>
<p>Hklm \system\currentcontrolset\services&lt;ミニポート名&gt;\Parameters\Device&lt;アダプター #&gt;</p></td>
</tr>
<tr class="even">
<td align="left">Value</td>
<td align="left"><p>既定:30</p>
<p>最大:600</p>
<p>単位: 秒</p></td>
</tr>
<tr class="odd">
<td align="left">説明</td>
<td align="left"><p>StorPort ミニポート ドライバーに I/O を再起動する前に待機方法ダウン時間の長いリンクになった後、この値は、ミニポート ドライバーが Storport を通知するために使用されます。</p></td>
</tr>
<tr class="even">
<td align="left">適用対象します。</td>
<td align="left"><p>Windows Server 2003 で開始しています。</p></td>
</tr>
</tbody>
</table>

 

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left">名前</td>
<td align="left"><strong>MaximumLogicalUnit</strong></td>
</tr>
<tr class="even">
<td align="left">種類</td>
<td align="left">REG_DWORD</td>
</tr>
<tr class="odd">
<td align="left">パス</td>
<td align="left"><p>ミニポート スコープ:</p>
<p>HKLM\System\CurrentControlSet\Services&lt;miniport name&gt;\Parameters\Device</p>
<p>アダプターのスコープ:</p>
<p>Hklm \system\currentcontrolset\services&lt;ミニポート名&gt;\Parameters\Device&lt;アダプター #&gt;</p></td>
</tr>
<tr class="even">
<td align="left">Value</td>
<td align="left"><p>既定:255</p>
<p>最大:設定すると、レジストリに 8</p></td>
</tr>
<tr class="odd">
<td align="left">説明</td>
<td align="left"><p>この値は、ターゲット デバイスの論理ユニット (LUN) の最大数を設定します。</p></td>
</tr>
<tr class="even">
<td align="left">適用対象します。</td>
<td align="left"><p>Windows Server 2003 で開始しています。</p></td>
</tr>
</tbody>
</table>

 

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left">名前</td>
<td align="left"><strong>MaximumUCXAddress</strong></td>
</tr>
<tr class="even">
<td align="left">種類</td>
<td align="left">REG_BINARY</td>
</tr>
<tr class="odd">
<td align="left">パス</td>
<td align="left"><p>ミニポート スコープ:</p>
<p>HKLM\System\CurrentControlSet\Services&lt;miniport name&gt;\Parameters\Device</p>
<p>アダプターのスコープ:</p>
<p>Hklm \system\currentcontrolset\services&lt;ミニポート名&gt;\Parameters\Device&lt;アダプター #&gt;</p></td>
</tr>
<tr class="even">
<td align="left">Value</td>
<td align="left"><p>既定:0 xffffffff</p>
<p>StorPort が既定値を使用して 0 の場合</p></td>
</tr>
<tr class="odd">
<td align="left">説明</td>
<td align="left"><p>この値は、キャッシュされていない拡張機能のアドレスの最大値を設定します。</p></td>
</tr>
<tr class="even">
<td align="left">適用対象します。</td>
<td align="left"><p>Windows Server 2003 で開始しています。</p></td>
</tr>
</tbody>
</table>

 

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left">名前</td>
<td align="left"><strong>MinimumUCXAddress</strong></td>
</tr>
<tr class="even">
<td align="left">種類</td>
<td align="left">REG_BINARY</td>
</tr>
<tr class="odd">
<td align="left">パス</td>
<td align="left"><p>ミニポート スコープ:</p>
<p>HKLM\System\CurrentControlSet\Services&lt;miniport name&gt;\Parameters\Device</p>
<p>アダプターのスコープ:</p>
<p>Hklm \system\currentcontrolset\services&lt;ミニポート名&gt;\Parameters\Device&lt;アダプター #&gt;</p></td>
</tr>
<tr class="even">
<td align="left">Value</td>
<td align="left"><p>既定:0x00000000</p>
<p>ときに MinimumUCXAddress &gt;= MaximumUCXAddress - PAGE_SIZE、StorPort は既定値を使用します。</p></td>
</tr>
<tr class="odd">
<td align="left">説明</td>
<td align="left"><p>この値は、キャッシュされていない拡張機能の最小アドレス値を設定します。</p></td>
</tr>
<tr class="even">
<td align="left">適用対象します。</td>
<td align="left"><p>Windows Server 2003 で開始しています。</p></td>
</tr>
</tbody>
</table>

 

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left">名前</td>
<td align="left"><strong>UncachedExtAlignment</strong></td>
</tr>
<tr class="even">
<td align="left">種類</td>
<td align="left">REG_DWORD</td>
</tr>
<tr class="odd">
<td align="left">パス</td>
<td align="left"><p>ミニポート スコープ:</p>
<p>HKLM\System\CurrentControlSet\Services&lt;miniport name&gt;\Parameters\Device</p>
<p>アダプターのスコープ:</p>
<p>Hklm \system\currentcontrolset\services&lt;ミニポート名&gt;\Parameters\Device&lt;アダプター #&gt;</p></td>
</tr>
<tr class="even">
<td align="left">Value</td>
<td align="left"><p>既定:0</p>
<p>最小:3</p>
<p>最大:16</p></td>
</tr>
<tr class="odd">
<td align="left">説明</td>
<td align="left"><p>StorPort、基本の 2 つの指数を計算する値を使用して (例: 1 &lt; &lt;値)、キャッシュされていない拡張バッファーの割り当ての配置の値として使用します。</p></td>
</tr>
<tr class="even">
<td align="left">適用対象します。</td>
<td align="left"><p>Windows Server 2003 で開始しています。</p></td>
</tr>
</tbody>
</table>

 

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left">名前</td>
<td align="left"><strong>NumberOfRequests</strong></td>
</tr>
<tr class="even">
<td align="left">種類</td>
<td align="left">REG_DWORD</td>
</tr>
<tr class="odd">
<td align="left">パス</td>
<td align="left"><p>ミニポート スコープ:</p>
<p>HKLM\System\CurrentControlSet\Services&lt;miniport name&gt;\Parameters\Device</p>
<p>アダプターのスコープ:</p>
<p>Hklm \system\currentcontrolset\services&lt;ミニポート名&gt;\Parameters\Device&lt;アダプター #&gt;</p></td>
</tr>
<tr class="even">
<td align="left">Value</td>
<td align="left"><p>既定:1000</p>
<p>最小:16</p>
<p>最大:255</p></td>
</tr>
<tr class="odd">
<td align="left">説明</td>
<td align="left"><p>アダプターで処理できる要求または数。 設定すると、範囲は、既定値より小さい。</p></td>
</tr>
</tbody>
</table>

 

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left">名前</td>
<td align="left"><strong>BusType</strong></td>
</tr>
<tr class="even">
<td align="left">種類</td>
<td align="left">REG_DWORD</td>
</tr>
<tr class="odd">
<td align="left">パス</td>
<td align="left"><p>ミニポート スコープ:</p>
<p>Hklm \system\currentcontrolset\services&lt;ミニポート名&gt;\Parameters</p></td>
</tr>
<tr class="even">
<td align="left">Value</td>
<td align="left"><p>既定:6、 <strong>BusTypeFiber</strong></p>
<p>最大:0x7f、値が大きい場合は、既定値として扱われます。</p></td>
</tr>
<tr class="odd">
<td align="left">説明</td>
<td align="left"><p>この値は、ミニポート ドライバーを管理するアダプターのバスの種類を示すために使用されます。 値は、バスの列挙型に対応します。<strong>STORAGE_BUS_TYPE</strong>します。</p></td>
</tr>
<tr class="even">
<td align="left">適用対象します。</td>
<td align="left"><p>Windows Server 2003 で開始しています。</p></td>
</tr>
</tbody>
</table>

 

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left">名前</td>
<td align="left"><strong>IoTimeoutValue</strong></td>
</tr>
<tr class="even">
<td align="left">種類</td>
<td align="left">REG_DWORD</td>
</tr>
<tr class="odd">
<td align="left">パス</td>
<td align="left"><p>ミニポート スコープ:</p>
<p>Hklm \system\currentcontrolset\services&lt;ミニポート名&gt;\Parameters</p></td>
</tr>
<tr class="even">
<td align="left">Value</td>
<td align="left"><p>最小:0</p>
<p>最大:65535</p>
<p>単位: 秒</p></td>
</tr>
<tr class="odd">
<td align="left">説明</td>
<td align="left"><p>ミニポート ドライバーによって管理されるデバイスの I/O タイムアウト値を示します。 このレジストリ値が存在しない場合は、グローバルなディスク I/O タイムアウト値が使用されます。</p></td>
</tr>
<tr class="even">
<td align="left">適用対象します。</td>
<td align="left"><p>Windows 8 で開始しています。</p></td>
</tr>
</tbody>
</table>

 

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left">名前</td>
<td align="left"><strong>IoLatencyCap</strong></td>
</tr>
<tr class="even">
<td align="left">種類</td>
<td align="left">REG_DWORD</td>
</tr>
<tr class="odd">
<td align="left">パス</td>
<td align="left"><p>ミニポート スコープ:</p>
<p>Hklm \system\currentcontrolset\services&lt;ミニポート名&gt;\Parameters</p></td>
</tr>
<tr class="even">
<td align="left">Value</td>
<td align="left"><p>既定:0</p>
<p>単位: ミリ秒</p></td>
</tr>
<tr class="odd">
<td align="left">説明</td>
<td align="left"><p>このレジストリ値が場合&gt;0、StorPort を保持する受信の I/O 要求キューのミニポート ドライバーに送信されるすべての I/O 要求が指定された時間に完了しなかったときにします。</p></td>
</tr>
<tr class="even">
<td align="left">適用対象します。</td>
<td align="left"><p>Windows 8 で開始しています。</p></td>
</tr>
</tbody>
</table>

 

## <a name="span-iddeviceenumerationentriesspanspan-iddeviceenumerationentriesspanspan-iddeviceenumerationentriesspandevice-enumeration-entries"></a><span id="Device_Enumeration_Entries"></span><span id="device_enumeration_entries"></span><span id="DEVICE_ENUMERATION_ENTRIES"></span>デバイス列挙のエントリ


<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left">名前</td>
<td align="left"><strong>TotalSenseDataBytes</strong></td>
</tr>
<tr class="even">
<td align="left">種類</td>
<td align="left">REG_DWORD</td>
</tr>
<tr class="odd">
<td align="left">パス</td>
<td align="left"><p>アダプターのスコープ:</p>
<p>HKLM\System\CurrentControlSet\Enum&lt;インスタンス パス&gt;\Device Parameters\StorPort</p></td>
</tr>
<tr class="even">
<td align="left">Value</td>
<td align="left"><p>既定:255</p>
<p>最小:18</p>
<p>最大:255</p>
<p>単位: バイト</p></td>
</tr>
<tr class="odd">
<td align="left">説明</td>
<td align="left"><p>示す、<em>センス データ</em>StorPort ミニポート ドライバーを返すサイズ。</p></td>
</tr>
<tr class="even">
<td align="left">適用対象します。</td>
<td align="left"><p>Windows Server 2003 で開始しています。</p></td>
</tr>
</tbody>
</table>

 

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left">名前</td>
<td align="left"><strong>QueueFullWaitIoPercentage</strong></td>
</tr>
<tr class="even">
<td align="left">種類</td>
<td align="left">REG_DWORD</td>
</tr>
<tr class="odd">
<td align="left">パス</td>
<td align="left"><p>論理ユニットのスコープ:</p>
<p>HKLM\CurrentControlSet\Enum\SCSI&lt;HardwareId&gt;&lt;InstanceId&gt;\Device Parameters\StorPort</p></td>
</tr>
<tr class="even">
<td align="left">Value</td>
<td align="left"><p>既定:25</p>
<p>最大:100</p>
<p>単位:キューの深さの割合</p></td>
</tr>
<tr class="odd">
<td align="left">説明</td>
<td align="left"><p>報告するとミニポート ビジー状態のデバイスを設定して<strong>SCSISTAT_QUEUE_FULL</strong>で<strong>ScsiStatus</strong>の<strong>SRB</strong>StorPort の論理ユニットのキューを一時停止し、は、一定量まで待機します。/O 要求はの新たな要求を送信する前に、ミニポートによって完了します。 StorPort になるまでの I/O 要求の量は、現在ミニポートに送信 I/O 要求の数の基準とした場合は、このレジストリ値を使用して計算されます。</p></td>
</tr>
<tr class="even">
<td align="left">適用対象します。</td>
<td align="left"><p>Windows Server 2003 で開始しています。</p></td>
</tr>
</tbody>
</table>

 

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left">名前</td>
<td align="left"><strong>BusyPauseTime</strong></td>
</tr>
<tr class="even">
<td align="left">種類</td>
<td align="left">REG_DWORD</td>
</tr>
<tr class="odd">
<td align="left">パス</td>
<td align="left"><p>論理ユニットのスコープ:</p>
<p>HKLM\CurrentControlSet\Enum\SCSI&lt;HardwareId&gt;&lt;InstanceId&gt;\Device Parameters\StorPort</p></td>
</tr>
<tr class="even">
<td align="left">Value</td>
<td align="left"><p>既定:250</p>
<p>単位: ミリ秒</p></td>
</tr>
<tr class="odd">
<td align="left">説明</td>
<td align="left"><p>報告すると、ミニポート ビジー状態のデバイスを設定して<strong>SRB_STATUS_BUSY</strong>で、 <strong>SrbStatus</strong>の<strong>SRB</strong>StorPort はユニット キューを一時停止し、指定した時間の待機I/O の送信を開始する前にもう一度要求します。</p></td>
</tr>
<tr class="even">
<td align="left">適用対象します。</td>
<td align="left"><p>Windows Server 2003 で開始しています。</p></td>
</tr>
</tbody>
</table>

 

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left">名前</td>
<td align="left"><strong>BusyPauseTime</strong></td>
</tr>
<tr class="even">
<td align="left">種類</td>
<td align="left">REG_DWORD</td>
</tr>
<tr class="odd">
<td align="left">パス</td>
<td align="left"><p>論理ユニットのスコープ:</p>
<p>HKLM\CurrentControlSet\Enum\SCSI&lt;HardwareId&gt;&lt;InstanceId&gt;\Device Parameters\StorPort</p></td>
</tr>
<tr class="even">
<td align="left">Value</td>
<td align="left"><p>既定:250</p>
<p>単位: ミリ秒</p></td>
</tr>
<tr class="odd">
<td align="left">説明</td>
<td align="left"><p>報告すると、ミニポート ビジー状態のデバイスを設定して<strong>SRB_STATUS_BUSY</strong>で、 <strong>SrbStatus</strong>の<strong>SRB</strong>StorPort が論理ユニットのキューを一時停止し、指定した待機I/O 要求をもう一度送信を開始する前に合計時間。</p></td>
</tr>
<tr class="even">
<td align="left">適用対象します。</td>
<td align="left"><p>Windows Server 2003 で開始しています。</p></td>
</tr>
</tbody>
</table>

 

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left">名前</td>
<td align="left"><strong>BusyRetryCount</strong></td>
</tr>
<tr class="even">
<td align="left">種類</td>
<td align="left">REG_DWORD</td>
</tr>
<tr class="odd">
<td align="left">パス</td>
<td align="left"><p>論理ユニットのスコープ:</p>
<p>HKLM\CurrentControlSet\Enum\SCSI&lt;HardwareId&gt;&lt;InstanceId&gt;\Device Parameters\StorPort</p></td>
</tr>
<tr class="even">
<td align="left">Value</td>
<td align="left"><p>既定:10</p></td>
</tr>
<tr class="odd">
<td align="left">説明</td>
<td align="left"><p>再発行する StorPort の再試行、 <strong>Srb</strong>ミニポートがビジー状態のデバイスまたはリンクを下へ報告するとします。</p></td>
</tr>
<tr class="even">
<td align="left">適用対象します。</td>
<td align="left"><p>Windows Server 2003 で開始しています。</p></td>
</tr>
</tbody>
</table>

 

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left">名前</td>
<td align="left"><strong>EnableIdlePowerManagement</strong></td>
</tr>
<tr class="even">
<td align="left">種類</td>
<td align="left">REG_DWORD</td>
</tr>
<tr class="odd">
<td align="left">パス</td>
<td align="left"><p>アダプターのスコープ:</p>
<p>HKLM\System\CurrentControlSet\Enum&lt;インスタンス パス&gt;\Device Parameters\StorPort</p></td>
</tr>
<tr class="even">
<td align="left">Value</td>
<td align="left"><p>既定:0、無効になっています</p></td>
</tr>
<tr class="odd">
<td align="left">説明</td>
<td align="left"><p>このレジストリ値が場合&gt;アイドルし、0 の電源管理を有効にします。 アイドル状態の電源管理は、アダプターに接続されている論理ユニットです。</p></td>
</tr>
<tr class="even">
<td align="left">適用対象します。</td>
<td align="left"><p>Windows 7 以降。</p></td>
</tr>
</tbody>
</table>

 

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left">名前</td>
<td align="left"><strong>DisableIdlePowerManagement</strong></td>
</tr>
<tr class="even">
<td align="left">種類</td>
<td align="left">REG_DWORD</td>
</tr>
<tr class="odd">
<td align="left">パス</td>
<td align="left"><p>論理ユニットのスコープ:</p>
<p>HKLM\CurrentControlSet\Enum\SCSI&lt;HardwareId&gt;&lt;InstanceId&gt;\Device Parameters\StorPort</p></td>
</tr>
<tr class="even">
<td align="left">Value</td>
<td align="left"><p>既定:0、有効になっています。</p></td>
</tr>
<tr class="odd">
<td align="left">説明</td>
<td align="left"><p>このレジストリ値が場合&gt;この論理ユニットのアイドル状態し、0 の電源管理は無効です。</p></td>
</tr>
<tr class="even">
<td align="left">適用対象します。</td>
<td align="left"><p>Windows 8 で開始しています。</p></td>
</tr>
</tbody>
</table>

 

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left">名前</td>
<td align="left"><strong>MinimumIdleTimeoutInMS</strong></td>
</tr>
<tr class="even">
<td align="left">種類</td>
<td align="left">REG_DWORD</td>
</tr>
<tr class="odd">
<td align="left">パス</td>
<td align="left"><p>論理ユニットのスコープ:</p>
<p>HKLM\CurrentControlSet\Enum\SCSI&lt;HardwareId&gt;&lt;InstanceId&gt;\Device Parameters\StorPort</p></td>
</tr>
<tr class="even">
<td align="left">Value</td>
<td align="left"><p>既定:MAXULONG を示す設定を解除します。 ミニポートはタイムアウト値を提供しない場合、実際の既定値は 5 分間、または 5 * 60 * 1000 が。</p>
<p>単位: ミリ秒</p></td>
</tr>
<tr class="odd">
<td align="left">説明</td>
<td align="left"><p>この値は、最小限の時間アイドル状態になると、power framework が論理ユニットの電源を待つ必要がありますを指定します。</p></td>
</tr>
<tr class="even">
<td align="left">適用対象します。</td>
<td align="left"><p>Windows 8 で開始しています。</p></td>
</tr>
</tbody>
</table>

 

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left">名前</td>
<td align="left"><strong>DisableRuntimePowerManagement</strong></td>
</tr>
<tr class="even">
<td align="left">種類</td>
<td align="left">REG_DWORD</td>
</tr>
<tr class="odd">
<td align="left">パス</td>
<td align="left"><p>アダプターのスコープ:</p>
<p>HKLM\System\CurrentControlSet\Enum&lt;インスタンス パス&gt;\Device Parameters\StorPort</p></td>
</tr>
<tr class="even">
<td align="left">Value</td>
<td align="left"><p>既定: 有効になっています。</p></td>
</tr>
<tr class="odd">
<td align="left">説明</td>
<td align="left"><p>場合、値&gt;0 の場合、アダプターの実行時の電源管理が無効になっています。 これには、特定のアダプターの実行時の電源管理が無効にします。</p>
<div class="alert">
<strong>注</strong>  このアダプターに接続されているデバイスの電源管理をランタイムが影響を受けません。
</div>
<div>
 
</div></td>
</tr>
<tr class="even">
<td align="left">適用対象します。</td>
<td align="left"><p>Windows 8 で開始しています。</p></td>
</tr>
</tbody>
</table>

 

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left">名前</td>
<td align="left"><strong>IdleTimeoutInMS</strong></td>
</tr>
<tr class="even">
<td align="left">種類</td>
<td align="left">REG_DWORD</td>
</tr>
<tr class="odd">
<td align="left">パス</td>
<td align="left"><p>アダプターのスコープ:</p>
<p>HKLM\System\CurrentControlSet\Enum&lt;インスタンス パス&gt;\Device Parameters\StorPort</p></td>
</tr>
<tr class="even">
<td align="left">Value</td>
<td align="left"><p>既定:60</p>
<p>単位: 秒</p></td>
</tr>
<tr class="odd">
<td align="left">説明</td>
<td align="left"><p>時間を指定するランタイム power framework がアイドル状態のアダプターを切る前に待機する必要があります。</p></td>
</tr>
<tr class="even">
<td align="left">適用対象します。</td>
<td align="left"><p>Windows 8 で開始しています。</p></td>
</tr>
</tbody>
</table>

 

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left">名前</td>
<td align="left"><strong>DisableD3Cold</strong></td>
</tr>
<tr class="even">
<td align="left">種類</td>
<td align="left">REG_DWORD</td>
</tr>
<tr class="odd">
<td align="left">パス</td>
<td align="left"><p>アダプターのスコープ:</p>
<p>HKLM\System\CurrentControlSet\Enum&lt;インスタンス パス&gt;\Device Parameters\StorPort</p></td>
</tr>
<tr class="even">
<td align="left">Value</td>
<td align="left"><p>(D3Cold がサポートされている) 場合に有効な既定値。</p></td>
</tr>
<tr class="odd">
<td align="left">説明</td>
<td align="left"><p>場合、値&gt;0 の場合、D3Cold アダプターを無効化をサポートします。</p></td>
</tr>
<tr class="even">
<td align="left">適用対象します。</td>
<td align="left"><p>Windows 8 で開始しています。</p></td>
</tr>
</tbody>
</table>

 

 

 




