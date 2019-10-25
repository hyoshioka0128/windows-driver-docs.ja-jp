---
title: StorPort ミニポート ドライバーのレジストリ エントリ
description: StorPort は、StorPort およびミニポート操作の動作を構成するために、一連のレジストリエントリを定義します。
ms.assetid: 543EC6A4-113C-4525-8063-28854B50760E
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: b712c6cbe0bdedb4bbbd1fa964da17861b88d67f
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72842717"
---
# <a name="registry-entries-for-storport-miniport-drivers"></a>StorPort ミニポート ドライバーのレジストリ エントリ


StorPort は、StorPort およびミニポート操作の動作を構成するために、一連のレジストリエントリを定義します。 値は、ミニポートドライバーまたはインスタンスごとに設定されます。

## <a name="span-idservice_entriesspanspan-idservice_entriesspanspan-idservice_entriesspanservice-entries"></a><span id="Service_Entries"></span><span id="service_entries"></span><span id="SERVICE_ENTRIES"></span>サービスエントリ


ミニポートのレジストリエントリは、 *\\parameters*サブキー、およびミニポートのサービスキーのデバイスサブキー *\\の\\パラメーター*によってキー付けされます。 個々のアダプターエントリに対して、サブキーは *\\パラメーター\\Device1*などのアダプターインデックスを含むように拡張されます。

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
<td align="left">タスクバーの検索ボックスに</td>
<td align="left">任意</td>
</tr>
<tr class="odd">
<td align="left">Path</td>
<td align="left"><p>ミニポートスコープ:</p>
<p>HKLM\System\CurrentControlSet\Services&lt;ミニポート名&gt;\Parameters\Device</p>
<p>アダプターのスコープ:</p>
<p>HKLM\System\CurrentControlSet\Services&lt;ミニポート名&gt;\Parameters\Device&lt;アダプタ #&gt;</p></td>
</tr>
<tr class="even">
<td align="left">Value</td>
<td align="left"><p>任意のミニポート固有のデータ。</p></td>
</tr>
<tr class="odd">
<td align="left">説明</td>
<td align="left"><p>Storport はこのレジストリデータを取得し、ミニポートの<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/storport/nc-storport-hw_find_adapter" data-raw-source="[&lt;strong&gt;HwStorFindAdapter&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/storport/nc-storport-hw_find_adapter)"><strong>HwStorFindAdapter</strong></a>ルーチンを呼び出すときに、<em>パラメーター</em>としてミニポートにバッファーを渡します。</p></td>
</tr>
<tr class="even">
<td align="left">当て</td>
<td align="left"><p>Windows Server 2003 以降。</p></td>
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
<td align="left">タスクバーの検索ボックスに</td>
<td align="left">REG_DWORD</td>
</tr>
<tr class="odd">
<td align="left">Path</td>
<td align="left"><p>ミニポートスコープ:</p>
<p>HKLM\System\CurrentControlSet\Services&lt;ミニポート名&gt;\Parameters\Device</p>
<p>アダプターのスコープ:</p>
<p>HKLM\System\CurrentControlSet\Services&lt;ミニポート名&gt;\Parameters\Device&lt;アダプタ #&gt;</p></td>
</tr>
<tr class="even">
<td align="left">Value</td>
<td align="left"><p>既定値:30</p>
<p>最大: 600</p>
<p>単位: 秒</p></td>
</tr>
<tr class="odd">
<td align="left">説明</td>
<td align="left"><p>この値は、ミニポートドライバーが、リンクがダウンした後、storport がミニポートドライバーに i/o を再起動するまでの待機時間を通知するために使用されます。</p></td>
</tr>
<tr class="even">
<td align="left">当て</td>
<td align="left"><p>Windows Server 2003 以降。</p></td>
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
<td align="left">タスクバーの検索ボックスに</td>
<td align="left">REG_DWORD</td>
</tr>
<tr class="odd">
<td align="left">Path</td>
<td align="left"><p>ミニポートスコープ:</p>
<p>HKLM\System\CurrentControlSet\Services&lt;ミニポート名&gt;\Parameters\Device</p>
<p>アダプターのスコープ:</p>
<p>HKLM\System\CurrentControlSet\Services&lt;ミニポート名&gt;\Parameters\Device&lt;アダプタ #&gt;</p></td>
</tr>
<tr class="even">
<td align="left">Value</td>
<td align="left"><p>既定値: 255</p>
<p>最大: レジストリで設定されている場合は8</p></td>
</tr>
<tr class="odd">
<td align="left">説明</td>
<td align="left"><p>この値は、ターゲットデバイスの論理ユニット (LUN) の最大数を設定します。</p></td>
</tr>
<tr class="even">
<td align="left">当て</td>
<td align="left"><p>Windows Server 2003 以降。</p></td>
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
<td align="left">タスクバーの検索ボックスに</td>
<td align="left">REG_BINARY</td>
</tr>
<tr class="odd">
<td align="left">Path</td>
<td align="left"><p>ミニポートスコープ:</p>
<p>HKLM\System\CurrentControlSet\Services&lt;ミニポート名&gt;\Parameters\Device</p>
<p>アダプターのスコープ:</p>
<p>HKLM\System\CurrentControlSet\Services&lt;ミニポート名&gt;\Parameters\Device&lt;アダプタ #&gt;</p></td>
</tr>
<tr class="even">
<td align="left">Value</td>
<td align="left"><p>既定値: 0xffffffff</p>
<p>0の場合、StorPort は既定値を使用します。</p></td>
</tr>
<tr class="odd">
<td align="left">説明</td>
<td align="left"><p>この値は、キャッシュされていない拡張機能の最大アドレス値を設定します。</p></td>
</tr>
<tr class="even">
<td align="left">当て</td>
<td align="left"><p>Windows Server 2003 以降。</p></td>
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
<td align="left">タスクバーの検索ボックスに</td>
<td align="left">REG_BINARY</td>
</tr>
<tr class="odd">
<td align="left">Path</td>
<td align="left"><p>ミニポートスコープ:</p>
<p>HKLM\System\CurrentControlSet\Services&lt;ミニポート名&gt;\Parameters\Device</p>
<p>アダプターのスコープ:</p>
<p>HKLM\System\CurrentControlSet\Services&lt;ミニポート名&gt;\Parameters\Device&lt;アダプタ #&gt;</p></td>
</tr>
<tr class="even">
<td align="left">Value</td>
<td align="left"><p>既定値: 0x00000000</p>
<p>MinimumUCXAddress &gt;= MaximumUCXAddress-PAGE_SIZE の場合、StorPort では既定値が使用されます。</p></td>
</tr>
<tr class="odd">
<td align="left">説明</td>
<td align="left"><p>この値は、キャッシュされていない拡張機能の最小アドレス値を設定します。</p></td>
</tr>
<tr class="even">
<td align="left">当て</td>
<td align="left"><p>Windows Server 2003 以降。</p></td>
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
<td align="left"><strong>の配置を防止する</strong></td>
</tr>
<tr class="even">
<td align="left">タスクバーの検索ボックスに</td>
<td align="left">REG_DWORD</td>
</tr>
<tr class="odd">
<td align="left">Path</td>
<td align="left"><p>ミニポートスコープ:</p>
<p>HKLM\System\CurrentControlSet\Services&lt;ミニポート名&gt;\Parameters\Device</p>
<p>アダプターのスコープ:</p>
<p>HKLM\System\CurrentControlSet\Services&lt;ミニポート名&gt;\Parameters\Device&lt;アダプタ #&gt;</p></td>
</tr>
<tr class="even">
<td align="left">Value</td>
<td align="left"><p>既定値: 0</p>
<p>最小: 3</p>
<p>最大:16</p></td>
</tr>
<tr class="odd">
<td align="left">説明</td>
<td align="left"><p>StorPort は、この値を使用して、キャッシュされていない拡張バッファーの割り当てのアラインメント値として使用する2つの基数 (例: 1 &lt;&lt; 値) を計算します。</p></td>
</tr>
<tr class="even">
<td align="left">当て</td>
<td align="left"><p>Windows Server 2003 以降。</p></td>
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
<td align="left">タスクバーの検索ボックスに</td>
<td align="left">REG_DWORD</td>
</tr>
<tr class="odd">
<td align="left">Path</td>
<td align="left"><p>ミニポートスコープ:</p>
<p>HKLM\System\CurrentControlSet\Services&lt;ミニポート名&gt;\Parameters\Device</p>
<p>アダプターのスコープ:</p>
<p>HKLM\System\CurrentControlSet\Services&lt;ミニポート名&gt;\Parameters\Device&lt;アダプタ #&gt;</p></td>
</tr>
<tr class="even">
<td align="left">Value</td>
<td align="left"><p>既定値: 1000</p>
<p>最小:16</p>
<p>最大: 255</p></td>
</tr>
<tr class="odd">
<td align="left">説明</td>
<td align="left"><p>アダプターが処理できる数または要求。 設定した場合、範囲は既定値よりも小さくなります。</p></td>
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
<td align="left">タスクバーの検索ボックスに</td>
<td align="left">REG_DWORD</td>
</tr>
<tr class="odd">
<td align="left">Path</td>
<td align="left"><p>ミニポートスコープ:</p>
<p>HKLM\System\CurrentControlSet\Services&lt;ミニポート名&gt;\Parameters</p></td>
</tr>
<tr class="even">
<td align="left">Value</td>
<td align="left"><p>既定値: 6、 <strong>Bustypefiber</strong></p>
<p>最大: 0x7f、値が大きい場合は、既定値として扱われます。</p></td>
</tr>
<tr class="odd">
<td align="left">説明</td>
<td align="left"><p>この値は、ミニポートドライバーが管理するアダプターのバスの種類を示すために使用されます。 値は、バス列挙型の<strong>STORAGE_BUS_TYPE</strong>に対応します。</p></td>
</tr>
<tr class="even">
<td align="left">当て</td>
<td align="left"><p>Windows Server 2003 以降。</p></td>
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
<td align="left">タスクバーの検索ボックスに</td>
<td align="left">REG_DWORD</td>
</tr>
<tr class="odd">
<td align="left">Path</td>
<td align="left"><p>ミニポートスコープ:</p>
<p>HKLM\System\CurrentControlSet\Services&lt;ミニポート名&gt;\Parameters</p></td>
</tr>
<tr class="even">
<td align="left">Value</td>
<td align="left"><p>最小: 0</p>
<p>最大: 65535</p>
<p>単位: 秒</p></td>
</tr>
<tr class="odd">
<td align="left">説明</td>
<td align="left"><p>ミニポートドライバーによって管理されるデバイスの i/o タイムアウト値を示します。 このレジストリ値が存在しない場合、システムはグローバルディスク i/o タイムアウト値を使用します。</p></td>
</tr>
<tr class="even">
<td align="left">当て</td>
<td align="left"><p>Windows 8 以降。</p></td>
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
<td align="left">タスクバーの検索ボックスに</td>
<td align="left">REG_DWORD</td>
</tr>
<tr class="odd">
<td align="left">Path</td>
<td align="left"><p>ミニポートスコープ:</p>
<p>HKLM\System\CurrentControlSet\Services&lt;ミニポート名&gt;\Parameters</p></td>
</tr>
<tr class="even">
<td align="left">Value</td>
<td align="left"><p>既定値: 0</p>
<p>単位: ミリ秒</p></td>
</tr>
<tr class="odd">
<td align="left">説明</td>
<td align="left"><p>このレジストリ値が 0 &gt; 場合、ミニポートドライバーに送信された i/o 要求が指定された期間内に完了していない場合、StorPort は受信 i/o 要求をキューに保持します。</p></td>
</tr>
<tr class="even">
<td align="left">当て</td>
<td align="left"><p>Windows 8 以降。</p></td>
</tr>
</tbody>
</table>

 

## <a name="span-iddevice_enumeration_entriesspanspan-iddevice_enumeration_entriesspanspan-iddevice_enumeration_entriesspandevice-enumeration-entries"></a><span id="Device_Enumeration_Entries"></span><span id="device_enumeration_entries"></span><span id="DEVICE_ENUMERATION_ENTRIES"></span>デバイス列挙エントリ


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
<td align="left">タスクバーの検索ボックスに</td>
<td align="left">REG_DWORD</td>
</tr>
<tr class="odd">
<td align="left">Path</td>
<td align="left"><p>アダプターのスコープ:</p>
<p>HKLM\System\CurrentControlSet\Enum&lt;インスタンスパス&gt;\Device Parameters\StorPort</p></td>
</tr>
<tr class="even">
<td align="left">Value</td>
<td align="left"><p>既定値: 255</p>
<p>最小:18</p>
<p>最大: 255</p>
<p>単位: バイト</p></td>
</tr>
<tr class="odd">
<td align="left">説明</td>
<td align="left"><p>ミニポートドライバーが StorPort に返す<em>センスデータ</em>サイズを示します。</p></td>
</tr>
<tr class="even">
<td align="left">当て</td>
<td align="left"><p>Windows Server 2003 以降。</p></td>
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
<td align="left">タスクバーの検索ボックスに</td>
<td align="left">REG_DWORD</td>
</tr>
<tr class="odd">
<td align="left">Path</td>
<td align="left"><p>論理ユニットのスコープ:</p>
<p>HKLM\CurrentControlSet\Enum\SCSI&lt;HardwareId&gt;&lt;InstanceId&gt;\Device Parameters\StorPort</p></td>
</tr>
<tr class="even">
<td align="left">Value</td>
<td align="left"><p>既定値:25</p>
<p>最大: 100</p>
<p>単位: キューの深さの割合</p></td>
</tr>
<tr class="odd">
<td align="left">説明</td>
<td align="left"><p><strong>SRB</strong>の<strong>ScsiStatus</strong>で<strong>SCSISTAT_QUEUE_FULL</strong>を設定することによって、ミニポートがデバイスのビジー状態を報告する場合、StorPort は論理ユニットキューを一時停止し、特定の量の i/o 要求がミニポートによって完了するまで待機します。要求. StorPort が待機する i/o 要求の量は、このレジストリ値を使用して、現在ミニポートに送信されている i/o 要求の数と比較して計算されます。</p></td>
</tr>
<tr class="even">
<td align="left">当て</td>
<td align="left"><p>Windows Server 2003 以降。</p></td>
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
<td align="left">タスクバーの検索ボックスに</td>
<td align="left">REG_DWORD</td>
</tr>
<tr class="odd">
<td align="left">Path</td>
<td align="left"><p>論理ユニットのスコープ:</p>
<p>HKLM\CurrentControlSet\Enum\SCSI&lt;HardwareId&gt;&lt;InstanceId&gt;\Device Parameters\StorPort</p></td>
</tr>
<tr class="even">
<td align="left">Value</td>
<td align="left"><p>既定値: 250</p>
<p>単位: ミリ秒</p></td>
</tr>
<tr class="odd">
<td align="left">説明</td>
<td align="left"><p><strong>SRB</strong>の<strong>Srbstatus</strong>で<strong>SRB_STATUS_BUSY</strong>を設定することによってミニポートがデバイスのビジー状態を報告する場合、StorPort は、ユニットキューを一時停止し、指定された時間待機してから、i/o 要求の送信を再開します。</p></td>
</tr>
<tr class="even">
<td align="left">当て</td>
<td align="left"><p>Windows Server 2003 以降。</p></td>
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
<td align="left">タスクバーの検索ボックスに</td>
<td align="left">REG_DWORD</td>
</tr>
<tr class="odd">
<td align="left">Path</td>
<td align="left"><p>論理ユニットのスコープ:</p>
<p>HKLM\CurrentControlSet\Enum\SCSI&lt;HardwareId&gt;&lt;InstanceId&gt;\Device Parameters\StorPort</p></td>
</tr>
<tr class="even">
<td align="left">Value</td>
<td align="left"><p>既定値: 250</p>
<p>単位: ミリ秒</p></td>
</tr>
<tr class="odd">
<td align="left">説明</td>
<td align="left"><p><strong>SRB</strong>の<strong>Srbstatus</strong>で<strong>SRB_STATUS_BUSY</strong>を設定することによって、ミニポートでデバイスのビジー状態が報告されると、StorPort は論理ユニットキューを一時停止し、指定した時間待機してから、i/o 要求の送信を再開します。</p></td>
</tr>
<tr class="even">
<td align="left">当て</td>
<td align="left"><p>Windows Server 2003 以降。</p></td>
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
<td align="left">タスクバーの検索ボックスに</td>
<td align="left">REG_DWORD</td>
</tr>
<tr class="odd">
<td align="left">Path</td>
<td align="left"><p>論理ユニットのスコープ:</p>
<p>HKLM\CurrentControlSet\Enum\SCSI&lt;HardwareId&gt;&lt;InstanceId&gt;\Device Parameters\StorPort</p></td>
</tr>
<tr class="even">
<td align="left">Value</td>
<td align="left"><p>既定値:10</p></td>
</tr>
<tr class="odd">
<td align="left">説明</td>
<td align="left"><p>ミニポートでデバイスがビジー状態になっている場合、またはリンクダウンした場合に、StorPort が<strong>Srb</strong>を再発行するために再試行します。</p></td>
</tr>
<tr class="even">
<td align="left">当て</td>
<td align="left"><p>Windows Server 2003 以降。</p></td>
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
<td align="left">タスクバーの検索ボックスに</td>
<td align="left">REG_DWORD</td>
</tr>
<tr class="odd">
<td align="left">Path</td>
<td align="left"><p>アダプターのスコープ:</p>
<p>HKLM\System\CurrentControlSet\Enum&lt;インスタンスパス&gt;\Device Parameters\StorPort</p></td>
</tr>
<tr class="even">
<td align="left">Value</td>
<td align="left"><p>既定値: 0、無効</p></td>
</tr>
<tr class="odd">
<td align="left">説明</td>
<td align="left"><p>このレジストリ値が &gt; 0 の場合は、アイドル状態の電源管理が有効になります。 アイドル状態の電源管理は、アダプターに接続されている論理ユニットを対象としています。</p></td>
</tr>
<tr class="even">
<td align="left">当て</td>
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
<td align="left">タスクバーの検索ボックスに</td>
<td align="left">REG_DWORD</td>
</tr>
<tr class="odd">
<td align="left">Path</td>
<td align="left"><p>論理ユニットのスコープ:</p>
<p>HKLM\CurrentControlSet\Enum\SCSI&lt;HardwareId&gt;&lt;InstanceId&gt;\Device Parameters\StorPort</p></td>
</tr>
<tr class="even">
<td align="left">Value</td>
<td align="left"><p>既定値: 0、有効</p></td>
</tr>
<tr class="odd">
<td align="left">説明</td>
<td align="left"><p>このレジストリ値が &gt; 0 の場合、この論理ユニットのアイドル電源管理は無効になります。</p></td>
</tr>
<tr class="even">
<td align="left">当て</td>
<td align="left"><p>Windows 8 以降。</p></td>
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
<td align="left">タスクバーの検索ボックスに</td>
<td align="left">REG_DWORD</td>
</tr>
<tr class="odd">
<td align="left">Path</td>
<td align="left"><p>論理ユニットのスコープ:</p>
<p>HKLM\CurrentControlSet\Enum\SCSI&lt;HardwareId&gt;&lt;InstanceId&gt;\Device Parameters\StorPort</p></td>
</tr>
<tr class="even">
<td align="left">Value</td>
<td align="left"><p>既定値: MAXULONG。未設定を示します。 ミニポートでタイムアウト値が指定されていない場合、実際の既定値は5分、つまり 5 * 60 * 1000 です。</p>
<p>単位: ミリ秒</p></td>
</tr>
<tr class="odd">
<td align="left">説明</td>
<td align="left"><p>この値は、1つの論理ユニットがアイドル状態になったときに電源を切るために必要な最小時間を指定します。</p></td>
</tr>
<tr class="even">
<td align="left">当て</td>
<td align="left"><p>Windows 8 以降。</p></td>
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
<td align="left">タスクバーの検索ボックスに</td>
<td align="left">REG_DWORD</td>
</tr>
<tr class="odd">
<td align="left">Path</td>
<td align="left"><p>アダプターのスコープ:</p>
<p>HKLM\System\CurrentControlSet\Enum&lt;インスタンスパス&gt;\Device Parameters\StorPort</p></td>
</tr>
<tr class="even">
<td align="left">Value</td>
<td align="left"><p>既定: 有効</p></td>
</tr>
<tr class="odd">
<td align="left">説明</td>
<td align="left"><p>値 &gt; 0 の場合、アダプターのランタイム電源管理は無効になります。 これにより、特定のアダプターのランタイム電源管理が無効になります。</p>
<div class="alert">
<strong>注</strong>  このアダプターに接続されているデバイスのランタイム電源管理は影響を受けません。
</div>
<div>
 
</div></td>
</tr>
<tr class="even">
<td align="left">当て</td>
<td align="left"><p>Windows 8 以降。</p></td>
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
<td align="left">タスクバーの検索ボックスに</td>
<td align="left">REG_DWORD</td>
</tr>
<tr class="odd">
<td align="left">Path</td>
<td align="left"><p>アダプターのスコープ:</p>
<p>HKLM\System\CurrentControlSet\Enum&lt;インスタンスパス&gt;\Device Parameters\StorPort</p></td>
</tr>
<tr class="even">
<td align="left">Value</td>
<td align="left"><p>既定値:60</p>
<p>単位: 秒</p></td>
</tr>
<tr class="odd">
<td align="left">説明</td>
<td align="left"><p>アイドル状態のアダプターの電源を切る前にランタイム電源フレームワークが待機する必要がある時間を指定します。</p></td>
</tr>
<tr class="even">
<td align="left">当て</td>
<td align="left"><p>Windows 8 以降。</p></td>
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
<td align="left">タスクバーの検索ボックスに</td>
<td align="left">REG_DWORD</td>
</tr>
<tr class="odd">
<td align="left">Path</td>
<td align="left"><p>アダプターのスコープ:</p>
<p>HKLM\System\CurrentControlSet\Enum&lt;インスタンスパス&gt;\Device Parameters\StorPort</p></td>
</tr>
<tr class="even">
<td align="left">Value</td>
<td align="left"><p>既定: enabled (D3Cold がサポートされている場合)</p></td>
</tr>
<tr class="odd">
<td align="left">説明</td>
<td align="left"><p>値 &gt; 0 の場合、アダプターの D3Cold サポートは無効になります。</p></td>
</tr>
<tr class="even">
<td align="left">当て</td>
<td align="left"><p>Windows 8 以降。</p></td>
</tr>
</tbody>
</table>

 

 

 




