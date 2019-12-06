---
title: シリアル IRP の主要な関数コード
description: ドキュメントのシリアル IRP の主要な関数コード
keywords:
- シリアルデバイス WDK
- シリアルドライバー WDK
- シリアル IRP コード
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 2c6742c5c9e50dd212fce83387f6cb27c0451a0a
ms.sourcegitcommit: ba3199328ea5d80119eafc399dc989e11e7ae1d6
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/05/2019
ms.locfileid: "74862591"
---
# <a name="serial-irp-major-function-codes"></a>シリアル IRP の主要な関数コード
このトピックでは、シリアル IRP の主要な関数コードについて説明します。

ヘッダー: Wdm (Wdm .h または Ntddk を含む)

## <a name="irp_mj_create"></a>IRP_MJ_CREATE

[IRP_MJ_CREATE](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-create)要求によって、シリアルデバイスが開かれます。

### <a name="when-sent"></a>送信日時

クライアントは、ポートまたはポートに接続されているデバイスにアクセスする前に、シリアルデバイスを開く必要があります。

### <a name="input-parameters"></a>入力パラメーター

なし。

### <a name="output-parameters"></a>出力パラメーター

なし。

### <a name="io-status-block"></a>I/o 状態ブロック

**情報**フィールドは0に設定されます。

**Status**フィールドは、次のいずれかの値に設定されます。

|ステータス値|説明|
|----|----|
|STATUS_SUCCESS|シリアルデバイスが正常に開かれました。|
|STATUS_ACCESS_DENIED|デバイスは既に開いています。|
|STATUS_DELETE_PENDING|シリアルはデバイスを削除しています。|
|STATUS_INSUFFICIENT_RESOURCES|デバイスがプラグアンドプレイ開始状態でないか、ドライバーが内部データ構造を割り当てることができませんでした。|
|STATUS_NOT_A_DIRECTORY|シリアルデバイスをディレクトリとして開くことはできません。|
|STATUS_PENDING|シリアルは、後で処理するために要求をキューに入れました。|
|STATUS_SHARED_IRQ_BUSY|デバイスに割り当てられている割り込みが、別の開いているデバイスによって使用されています。|

### <a name="operation"></a>操作

シリアルデバイスを使用するには、そのデバイスを開く必要があります。 シリアルデバイスは、排他的なデバイスです。特定の時点で、ポートで開くことができるファイルは1つだけです。

## <a name="irp_mj_device_control"></a>IRP_MJ_DEVICE_CONTROL

IRP_MJ_DEVICE_CONTROL 要求は、シリアルポートを操作します。

### <a name="when-sent"></a>送信日時

クライアントは、次の場合にデバイス制御要求を使用します。

* ポートに関する情報を取得する
* レジスタの取得と設定
* 動作モードの取得と設定

シリアルでサポートされているデバイス制御要求の詳細については、 [ntddser](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddser/)ヘッダーを参照してください。

### <a name="input-parameters"></a>入力パラメーター。

特定の要求

### <a name="output-parameters"></a>出力パラメーター

特定の要求

### <a name="io-status-block"></a>I/o 状態ブロック

特定の要求

### <a name="operation"></a>操作

特定の要求

## <a name="irp_mj_flush_buffers"></a>IRP_MJ_FLUSH_BUFFERS

[IRP_MJ_FLUSH_BUFFER](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-flush-buffers)要求は、シリアルデバイスの内部書き込みバッファーをフラッシュします。

### <a name="when-sent"></a>送信日時

クライアントは、フラッシュ要求を使用して、クライアントがフラッシュ要求の前に送信したすべての書き込み要求がシリアルによって完了したことを確認します。

### <a name="input-parameters"></a>入力パラメーター。

なし。

### <a name="output-parameters"></a>出力パラメーター

なし。

### <a name="io-status-block"></a>I/o 状態ブロック

**情報**メンバーが0に設定されています。

**Status**メンバーは、次のいずれかの状態値に設定されます。

|ステータス値|説明|
|----|----|
|STATUS_SUCCESS|要求は正常に完了しました。|
|STATUS_CANCELLED|クライアントが要求を取り消しました。 また、デバイスエラーが発生し、シリアルがデバイスエラーが発生した場合に要求をキャンセルするように構成されている場合にも、シリアルは要求をキャンセルします。|
|STATUS_DELETE_PENDING|ドライバーは、デバイスを削除しています。|
|STATUS_PENDING|シリアルは、後で処理するために要求をキューに入れました。|

### <a name="operation"></a>操作

シリアルキューを作成し、要求を受信する順序で書き込み要求とフラッシュ要求の処理を開始します。 シリアルは、フラッシュ要求の前に受け取ったすべての書き込み要求に対して**IoCompleteRequest**を呼び出すと、フラッシュ要求を完了します。 *ただし、フラッシュ要求の完了は、以前に開始されたすべての書き込み要求が、デバイススタック内の他のドライバーによって完了したことを示すものではありません。* たとえば、フィルタードライバーが書き込み要求を処理している可能性があります。 クライアントは、書き込み要求の IRP を解放または再利用する前に、デバイススタック内のすべてのドライバーが書き込み要求を完了したことを確認する必要があります。

## <a name="irp_mj_internal_device_control"></a>IRP_MJ_INTERNAL_DEVICE_CONTROL
[IRP_MJ_INTERNAL_DEVICE_CONTROL](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-internal-device-control)要求は、シリアルデバイスで内部の動作モードを設定します。

### <a name="when-sent"></a>送信日時

クライアントは、次のための内部デバイス制御要求を使用します。

* 基本設定の取得とリセット
* 待機/ウェイク操作の制御

デバイスコントロールの内部要求の詳細については、 [ntddser](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddser/)ヘッダーを参照してください。

### <a name="input-parameters"></a>入力パラメーター。

特定の要求

### <a name="output-parameters"></a>出力パラメーター

特定の要求

### <a name="io-status-block"></a>I/o 状態ブロック

特定の要求

### <a name="operation"></a>操作

特定の要求

## <a name="irp_mj_pnp"></a>IRP_MJ_PNP

[IRP_MJ_PNP](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-pnp)要求ではプラグアンドプレイがサポートされています。

### <a name="when-sent"></a>送信日時

PnP マネージャーは、デバイスを照会し、デバイスの起動、停止、および削除を行うために IRP_MJ_PNP 要求を送信します。

### <a name="input-parameters"></a>入力パラメーター。

特定の要求

### <a name="output-parameters"></a>出力パラメーター

特定の要求

### <a name="io-status-block"></a>I/o 状態ブロック

特定の要求

### <a name="operation"></a>操作

Serial は、次のプラグアンドプレイ要求をサポートしています。

* [IRP_MN_CANCEL_REMOVE_DEVICE](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-cancel-remove-device)
* [IRP_MN_CANCEL_STOP_DEVICE](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-cancel-stop-device)
* [IRP_MN_FILTER_RESOURCE_REQUIREMENTS](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-filter-resource-requirements)
* [IRP_MN_QUERY_CAPABILITIES](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-query-capabilities)
* [IRP_MN_QUERY_DEVICE_RELATIONS](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-query-device-relations)
* [IRP_MN_QUERY_ID](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-query-id)
* [IRP_MN_QUERY_PNP_DEVICE_STATE](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-query-pnp-device-state)
* [IRP_MN_QUERY_REMOVE_DEVICE](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-query-remove-device)
* [IRP_MN_QUERY_RESOURCE_REQUIREMENTS](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-query-resource-requirements)
* [IRP_MN_QUERY_STOP_DEVICE](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-query-stop-device)
* [IRP_MN_REMOVE_DEVICE](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-remove-device)
* [IRP_MN_START_DEVICE](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-start-device)
* [IRP_MN_STOP_DEVICE](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-stop-device)
* [IRP_MN_SURPRISE_REMOVAL](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-surprise-removal)

シリアルは、その他のすべてのプラグアンドプレイ要求をデバイススタックに送信します。それ以降の処理は行われません。

Serial は、プラグアンドプレイ要求に対して次のシリアル固有の処理を実行します。

**IRP_MN_QUERY_ID** (型 Busqueryハード)

シリアルデバイスがマルチポート ISA カード上にある場合、シリアルは、ワイド文字の文字列 "* PNP0502" をハードウェア Id の文字列に追加します。

**IRP_MN_FILTER_RESOURCE_REQUIREMENTS**

マルチポート ISA カード上のシリアルデバイスは、同じ割り込み状態レジスタと同じ割り込みを共有します。

プラグアンドプレイ要求の一般的な操作の詳細については[プラグアンドプレイ「小さな irp](https://docs.microsoft.com/windows-hardware/drivers/kernel/plug-and-play-minor-irps)」を参照してください。

## <a name="irp_mj_power"></a>IRP_MJ_POWER

[IRP_MJ_POWER](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-power)要求は電源管理を制御します。

### <a name="when-sent"></a>送信日時

電源マネージャーは、電源要求を使用してクエリを実行し、電源状態を設定します。

###  <a name="input-parameters"></a>入力パラメーター。

特定の要求

### <a name="output-parameters"></a>出力パラメーター

特定の要求

### <a name="io-status-block"></a>I/o 状態ブロック

特定の要求

### <a name="operation"></a>操作

Serial は次の電源要求をサポートしています。

* [IRP_MN_QUERY_POWER](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-query-power)
* [IRP_MN_SET_POWER](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-set-power)

シリアルは、下位レベルのドライバーによって完了されるように、デバイススタックの他のすべての電源要求を送信します。

Serial は、関数ドライバーまたは下位レベルのフィルタードライバーとして Serial を使用するシリアルデバイススタックの既定の電源ポリシー所有者です。

これらの要求の一般的な操作の詳細については、「[電源 irp を処理するためのルール](https://docs.microsoft.com/windows-hardware/drivers/kernel/rules-for-handling-power-irps)」を参照してください。

## <a name="irp_mj_query_information"></a>IRP_MJ_QUERY_INFORMATION

[IRP_MJ_QUERY_INFORMATION](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-query-information)要求は、シリアルデバイスのファイルの最後情報を照会します。 

### <a name="when-sent"></a>送信日時

クライアントは、クエリ情報要求を使用して、シリアルデバイスで開かれたファイルに関する標準的な情報と位置情報を取得します。

### <a name="input-parameters"></a>入力パラメーター。

**パラメーターの QueryFile. FileInformationClass**は**fileinformationclass**または**fileinformationclass**に設定されます。

### <a name="output-parameters"></a>出力パラメーター

|パラメーター|説明|
|----|----|
|**FileStandardInformation**|**AssociatedIrp**メンバーは、シリアルが標準情報を出力するために使用する、クライアントによって割り当てられた FILE_STANDARD_INFORMATION 構造体を指します。|
|**FilePositionInformation**|AssociatedIrp のメンバーは、シリアルが位置情報を出力するために使用する、クライアントに割り当てられた FILE_POSITION_INFORMATION 構造体を指し**ます**。|

### <a name="io-status-block"></a>I/o 状態ブロック

要求が成功した場合、**情報**メンバーは0に設定されます。

**Status**メンバーは、次のいずれかの状態値に設定されます。

|ステータス値|説明|
|----|----|
|STATUS_SUCCESS|要求は正常に完了しました。|
|STATUS_CANCELLED|クライアントが要求を取り消しました。 また、デバイスエラーが発生し、シリアルがデバイスエラーが発生した場合に要求をキャンセルするように構成されている場合にも、シリアルは要求をキャンセルします。|
|STATUS_DELETE_PENDING|シリアルはデバイスを削除しています。|
|STATUS_INVALID_PARAMETER|要求された情報はサポートされていません。|
|STATUS_PENDING|シリアルは、後で処理するために要求をキューに入れました。|

### <a name="operation"></a>操作

Serial は、 **Filestandardinformation**と**filestandardinformation**型の要求をサポートしています。

標準ファイルの情報は、必要に応じて常に0または**FALSE**に設定されます。 位置情報は常に0に設定されます。

## <a name="irp_mj_read"></a>IRP_MJ_READ

[IRP_MJ_READ](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-read)要求は、シリアルデバイスからクライアントにデータを転送します。

### <a name="when-sent"></a>送信日時

クライアントは、シリアルデバイス上のデータを読み取るときに、読み取り要求を使用します。

### <a name="input-parameters"></a>入力パラメーター。

**Parameters. read. Length**メンバーは、クライアントの読み取りバッファーに転送するバイト数に設定されます。

### <a name="output-parameters"></a>出力パラメーター

**AssociatedIrp**のメンバーは、クライアントが割り当てた読み取りバッファーを指します。このデータは、シリアルデバイス上でデータが読み取られます。

### <a name="io-status-block"></a>I/o 状態ブロック

**情報**メンバーは、クライアントの読み取りバッファーに転送されるバイト数に設定されます。

**Status**メンバーは、次のいずれかの値に設定されます。

|ステータス値|説明|
|----|----|
|STATUS_SUCCESS|要求は正常に完了しました。|
|STATUS_CANCELLED|クライアントが要求を取り消しました。 また、デバイスエラーが発生し、シリアルがデバイスエラーが発生した場合に要求をキャンセルするように構成されている場合にも、シリアルは要求をキャンセルします。|
|STATUS_DELETE_PENDING|シリアルはデバイスを削除しています。|
|STATUS_PENDING|シリアルは、後で処理するために要求をキューに入れました。|
|STATUS_TIMEOUT|要求の完了に要する時間が、タイムアウトの合計値または間隔のタイムアウト値を超えました。|

### <a name="operation"></a>操作

クライアントは、タイムアウトイベントを使用して読み取り要求を終了できます。 ただし、シリアルデバイスを開くと、デバイスのタイムアウト設定が定義されていないことに注意してください。 カーネルモードのクライアントは、 [IOCTL_SERIAL_INTERNAL_BASIC_SETTINGS](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddser/ni-ntddser-ioctl_serial_internal_basic_settings)を使用してタイムアウトパラメーターを0に設定できます (タイムアウトイベントは使用されません)。 ユーザーモードとカーネルモードのクライアントは、 [IOCTL_SERIAL_SET_TIMEOUTS](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddser/ni-ntddser-ioctl_serial_set_timeouts)要求を使用して、タイムアウトパラメーターを設定できます。 

読み取りと書き込みのタイムアウトの詳細については、「[シリアルデバイスの読み取りおよび書き込みタイムアウトの設定](https://docs.microsoft.com/previous-versions/ff547486(v=vs.85))」を参照してください。

## <a name="irp_mj_set_information"></a>IRP_MJ_SET_INFORMATION

[IRP_MJ_SET_INFORMATION](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-shutdown)要求は、シリアルデバイスに関するファイルの最終情報を設定します。

### <a name="when-sent"></a>送信日時

クライアントは、設定情報要求を使用して、シリアルデバイスで開かれているファイルの現在のファイルの終了位置を変更します。

### <a name="input-parameters"></a>入力パラメーター。
**Parameters. FileInformationClass**メンバーは**fileendoffileinformation**または**fileの情報**に設定されています。

### <a name="output-parameters"></a>出力パラメーター

なし。

### <a name="io-status-block"></a>I/o 状態ブロック

要求が成功した場合、**情報**メンバーは0に設定されます。

**Status**メンバーは、次のいずれかの状態値に設定されます。

|ステータス値|説明|
|----|----|
|STATUS_SUCCESS|要求は正常に完了しました。|
|STATUS_CANCELLED|クライアントが要求を取り消しました。 また、デバイスエラーが発生し、シリアルがデバイスエラーが発生した場合に要求をキャンセルするように構成されている場合にも、シリアルは要求をキャンセルします。|
|STATUS_DELETE_PENDING|シリアルはデバイスを削除しています。|
|STATUS_INVALID_PARAMETER|指定されたファイルの末尾情報はサポートされていません。|
|STATUS_PENDING|シリアルは、後で処理するために要求をキューに入れました。|

### <a name="operation"></a>操作

Serial では、 **Fileendoffileinformation**と**fileて information**型の要求がサポートされています。 ただし、シリアルは実際にファイル情報を設定しません。 ファイルの終端位置は常に0に設定されます。

## <a name="irp_mj_system_control"></a>IRP_MJ_SYSTEM_CONTROL

[IRP_MJ_SYSTEM_CONTROL](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-system-control)要求では、WMI 要求がサポートされています。

### <a name="when-sent"></a>送信日時

WMI カーネルモードコンポーネントは、シリアルデバイスの WMI プロバイダーとしてシリアルレジスタの後でいつでも IRP_MJ_SYSTEM_CONTROL 要求を送信できます。 通常、WMI Irp は、ユーザーモードデータコンシューマーが WMI データを要求したときに送信されます。

### <a name="input-parameters"></a>入力パラメーター。

特定の要求

### <a name="output-parameters"></a>出力パラメーター

特定の要求

### <a name="io-status-block"></a>I/o 状態ブロック

WMI 要求の場合、[状態] フィールドは次のいずれかの値に設定されます。

|ステータス値|説明|
|----|----|
|STATUS_SUCCESS|要求は正常に完了しました。|
|STATUS_BUFFER_TOO_SMALL|出力バッファーのサイズ (バイト単位) が要求された情報の必要なサイズを下回っています。|
|STATUS_INSUFFICIENT_RESOURCES|シリアルポート名を保存するための十分なシステムリソースがありませんでした。|
|STATUS_INVALID_DEVICE_REQUEST|要求が無効です。|
|STATUS_WMI_GUID_NOT_FOUND|WMI GUID はサポートされていません。|

### <a name="operation"></a>操作

Serial は、WMI システムコントロール要求を処理するために、の使い方を[使用します](https://docs.microsoft.com/windows-hardware/drivers/ddi/wmilib/nf-wmilib-wmisystemcontrol)。 シリアルでは、次の種類の WMI ライブラリコールバックルーチンが登録されます。これにより、デバイスに送信**される wmi**要求を処理するための呼び出しが実行されます。

* [この情報を持つ](https://docs.microsoft.com/windows-hardware/drivers/ddi/wmilib/nc-wmilib-wmi_query_reginfo_callback)
* [すべてのクエリを](https://docs.microsoft.com/windows-hardware/drivers/ddi/wmilib/nc-wmilib-wmi_query_datablock_callback)
* [このようにしてください。](https://docs.microsoft.com/windows-hardware/drivers/ddi/wmilib/nc-wmilib-wmi_set_datablock_callback)
* [\N この Setdataitem](https://docs.microsoft.com/windows-hardware/drivers/ddi/wmilib/nc-wmilib-wmi_set_dataitem_callback)

Serial は、他のシステム制御要求をサポートしていません。 WMI 以外の要求の場合、シリアルは現在のスタック位置をスキップし、デバイススタックで要求を送信します。

シリアルは、次の表に示す WMI GUID を登録します。

シリアル WMI GUID に関連付けられたデータ構造 

| SERIAL_PORT_WMI_NAME_GUID | USHORT の後に WCSTR が続く |
| ------------------------- | -------------------------- |
| SERIAL_PORT_WMI_COMM_GUID | SERIAL_WMI_COMM_DATA |
| SERIAL_PORT_WMI_HW_GUID | SERIAL_WMI_HW_DATA |
| SERIAL_PORT_WMI_PERF_GUID | SERIAL_WMI_PERF_DATA |
| SERIAL_PORT_WMI_PROPERTIES_GUID | WMI_SERIAL_PORT_PROPERTIES |

シリアルデバイスの WMI 名は、デバイスのプラグアンドプレイレジストリキーの下にあるエントリ値**PortName**の値です。

## <a name="irp_mj_write"></a>IRP_MJ_WRITE

[IRP_MJ_WRITE](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-write)要求は、クライアントからシリアルデバイスにデータを転送します。

### <a name="when-sent"></a>送信日時

クライアントは、シリアルデバイスにデータを書き込むときに、書き込み要求を使用します。

### <a name="input-parameters"></a>入力パラメーター。

**Parameters. Length**メンバーは、クライアントが割り当てた書き込みバッファーからシリアルデバイスにコピーするバイト数に設定されます。

**AssociatedIrp**メンバーは、シリアルデバイスへのデータのコピー元となる、クライアントが割り当てた書き込みバッファーを指します。

### <a name="output-parameters"></a>出力パラメーター

なし。

### <a name="io-status-block"></a>I/o 状態ブロック

*情報*メンバーは、クライアントの書き込みバッファーからシリアルデバイスに実際にコピーされたバイト数に設定されます。

*Status*メンバーは、次のいずれかの値に設定されます。

|ステータス値|説明|
|----|----|
|STATUS_SUCCESS|要求は正常に完了しました。|
|STATUS_CANCELLED|クライアントが要求を取り消しました。 また、デバイスエラーが発生し、シリアルがデバイスエラーが発生した場合に要求をキャンセルするように構成されている場合にも、シリアルは要求をキャンセルします。|
|STATUS_DELETE_PENDING|シリアルはデバイスを削除しています。|
|STATUS_PENDING|シリアルは、後で処理するために要求をキューに入れました。|
|STATUS_TIMEOUT|書き込み要求に許可された合計時間を超えました。|

### <a name="operation"></a>操作

クライアントは、タイムアウトイベントを使用して、書き込み要求を終了できます。 ただし、シリアルデバイスを開いたときに、デバイスに設定されたタイムアウトイベントは未定義であることに注意してください。 カーネルモードクライアントは、 [IOCTL_SERIAL_INTERNAL_BASIC_SETTINGS](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddser/ni-ntddser-ioctl_serial_internal_basic_settings)を使用してタイムアウトパラメーターを0に設定できます (タイムアウトイベントは使用されません)。また、タイムアウトパラメーターを設定するための[IOCTL_SERIAL_SET_TIMEOUTS](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddser/ni-ntddser-ioctl_serial_set_timeouts)要求です。 読み取りと書き込みのタイムアウトの詳細については、「[シリアルデバイスの読み取りおよび書き込みタイムアウトの設定](https://docs.microsoft.com/previous-versions/ff547486(v=vs.85))」を参照してください。

## <a name="related-topics"></a>関連トピック

[プラグアンドプレイの小さな Irp](https://docs.microsoft.com/windows-hardware/drivers/kernel/plug-and-play-minor-irps)

[電源 Irp を処理するための規則](https://docs.microsoft.com/windows-hardware/drivers/kernel/rules-for-handling-power-irps)

[シリアルコントローラードライバーの設計ガイド](https://docs.microsoft.com/windows-hardware/drivers/serports/)
