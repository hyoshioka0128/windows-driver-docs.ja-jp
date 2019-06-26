---
title: シリアル IRP の主要な関数コード
description: シリアル IRP 主な機能のコードのドキュメント
keywords:
- WDK のシリアル デバイス
- シリアル ドライバー WDK
- シリアル IRP コード
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: dc55bec9961072ea7d8595ccbcda269a563124c1
ms.sourcegitcommit: da49bbd01df836def12aae732f9a0e85c15a8a9f
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/26/2019
ms.locfileid: "67395212"
---
# <a name="serial-irp-major-function-codes"></a>シリアル IRP の主要な関数コード
このトピックでは、シリアル IRP の主な機能コードを説明します。

ヘッダー:Wdm.h (Wdm.h または Ntddk.h を含む)

## <a name="irpmjcreate"></a>IRP_MJ_CREATE

[Irp_mj_create 用](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-create)要求は、シリアル デバイスを開きます。

### <a name="when-sent"></a>送信されたときに

クライアントは、ポートまたはポートに接続されているデバイスにアクセスできる前に、シリアル デバイスを開く必要があります。

### <a name="input-parameters"></a>入力パラメーター

なし。

### <a name="output-parameters"></a>出力パラメーター

なし。

### <a name="io-status-block"></a>状態の I/O ブロック

**情報**フィールドが 0 に設定されます。

**状態**フィールドは、次の値のいずれかに設定されます。

|状態値|説明|
|----|----|
|STATUS_SUCCESS|シリアル デバイスが正常に開きました。|
|STATUS_ACCESS_DENIED|デバイスは既に開いています。|
|STATUS_DELETE_PENDING|シリアルは、デバイスを削除する予定です。|
|STATUS_INSUFFICIENT_RESOURCES|プラグ アンド プレイの開始状態では、デバイスまたはドライバーが内部データ構造体を割り当てられませんでした。|
|STATUS_NOT_A_DIRECTORY|シリアル デバイスをディレクトリとして開くことができません。|
|STATUS_PENDING|シリアルには、後で処理要求がキューに登録します。|
|STATUS_SHARED_IRQ_BUSY|デバイスに割り当てられている割り込みは、開いている別のデバイスで使用中です。|

### <a name="operation"></a>操作

使用する、シリアル デバイスを開く必要があります。 シリアル デバイスは、排他的なデバイスです。ファイルの 1 つだけ開くことができるポートを特定の時点。

## <a name="irpmjdevicecontrol"></a>IRP_MJ_DEVICE_CONTROL

IRP_MJ_DEVICE_CONTROL 要求には、シリアル ポートが動作します。

### <a name="when-sent"></a>送信されたときに

クライアントは、デバイスに対する制御要求を使用します。

* ポートに関する情報を取得します。
* 取得およびレジスタを設定します。
* 取得および設定の動作モード

シリアルでサポートされるデバイス制御要求の説明は、次を参照してください。、 [ntddser.h](https://docs.microsoft.com/en-us/windows-hardware/drivers/ddi/content/ntddser/)ヘッダー。

### <a name="input-parameters"></a>入力パラメーター。

特定の要求

### <a name="output-parameters"></a>出力パラメーター

特定の要求

### <a name="io-status-block"></a>状態の I/O ブロック

特定の要求

### <a name="operation"></a>操作

特定の要求

## <a name="irpmjflushbuffers"></a>IRP_MJ_FLUSH_BUFFERS

[IRP_MJ_FLUSH_BUFFER](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-flush-buffers)要求は、シリアル デバイスの内部書き込みバッファーをフラッシュします。

### <a name="when-sent"></a>送信されたときに

クライアントでは、フラッシュの要求を使用して、フラッシュの要求の前に送信されるクライアント要求を書き込むすべてのシリアルが完了したときを調べます。

### <a name="input-parameters"></a>入力パラメーター。

なし。

### <a name="output-parameters"></a>出力パラメーター

なし。

### <a name="io-status-block"></a>状態の I/O ブロック

**情報**メンバーが 0 に設定されます。

**状態**メンバーの状態値は次のいずれかに設定されます。

|状態値|説明|
|----|----|
|STATUS_SUCCESS|要求は正常に完了しました。|
|STATUS_CANCELLED|クライアントでは、要求が取り消されました。 シリアルは、デバイスのエラーが発生したデバイスのエラーがある場合は、要求をキャンセルするシリアルが構成されている場合も、要求をキャンセルします。|
|STATUS_DELETE_PENDING|ドライバーは、デバイスを削除する予定です。|
|STATUS_PENDING|シリアルには、後で処理要求がキューに登録します。|

### <a name="operation"></a>操作

シリアル キューおよび処理を開始、要求が受信される順序で要求のフラッシュを読み書きします。 呼び出された後、シリアルがフラッシュの要求を完了する**IoCompleteRequest**のすべての書き込みをフラッシュの要求の前に受信した要求。 *ただし、フラッシュの要求の完了では、デバイス スタックの他のドライバーによって、すべての以前に開始した書き込み要求が完了したことは示しません。* などのフィルター ドライバーでは書き込み要求を処理するも可能性があります。 クライアントは、クライアントは解放するか、書き込み要求の IRP を再利用する前に、デバイス スタックのすべてのドライバーが書き込み要求が完了したことを確認する必要があります。

## <a name="irpmjinternaldevicecontrol"></a>IRP_MJ_INTERNAL_DEVICE_CONTROL
[IRP_MJ_INTERNAL_DEVICE_CONTROL](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-internal-device-control)シリアル デバイスで要求が内部の動作モードを設定します。

### <a name="when-sent"></a>送信されたときに

クライアントは、内部のデバイスに対する制御要求を使用します。

* 設定と基本設定のリセット
* コントロールの待機またはスリープ解除の操作

内部デバイスに対する制御要求の説明は、次を参照してください。、 [ntddser.h](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddser/)ヘッダー。

### <a name="input-parameters"></a>入力パラメーター。

特定の要求

### <a name="output-parameters"></a>出力パラメーター

特定の要求

### <a name="io-status-block"></a>状態の I/O ブロック

特定の要求

### <a name="operation"></a>操作

特定の要求

## <a name="irpmjpnp"></a>IRP_MJ_PNP

[IRP_MJ_PNP](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-pnp)要求は、プラグ アンド プレイをサポートしています。

### <a name="when-sent"></a>送信されたときに

PnP マネージャーがデバイスのクエリに IRP_MJ_PNP 要求を送信し、開始、停止、およびデバイスを削除します。

### <a name="input-parameters"></a>入力パラメーター。

特定の要求

### <a name="output-parameters"></a>出力パラメーター

特定の要求

### <a name="io-status-block"></a>状態の I/O ブロック

特定の要求

### <a name="operation"></a>操作

シリアルには、次のプラグ アンド プレイの要求がサポートされています。

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

シリアルでは、さらに処理することがなく、デバイス スタックを他のすべてのプラグ アンド プレイ要求を送信します。

シリアルは、次のシリアル-特定のプラグ アンド プレイの要求を処理を実行します。

**IRP_MN_QUERY_ID** (BusQueryHardwardIDs 型)

シリアルがワイド文字の文字列を追加してシリアル デバイスがマルチポート ISA カード上にある場合は、"* PNP0502"ハードウェア Id の文字列にします。

**IRP_MN_FILTER_RESOURCE_REQUIREMENTS**

マルチポート ISA カードのシリアル デバイスは、同じ割り込み状態レジスタおよび同じ割り込みを共有します。

プラグ アンド プレイの要求の一般的な操作の説明は、次を参照してください。[プラグ アンド プレイ マイナー Irp](https://docs.microsoft.com/windows-hardware/drivers/kernel/plug-and-play-minor-irps)します。

## <a name="irpmjpower"></a>IRP_MJ_POWER

[対し、IRP_MJ_POWER](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-power)要求の電源管理を制御します。

### <a name="when-sent"></a>送信されたときに

電源マネージャーは、クエリを実行し、電源の状態を設定する電源要求を使用します。

###  <a name="input-parameters"></a>入力パラメーター。

特定の要求

### <a name="output-parameters"></a>出力パラメーター

特定の要求

### <a name="io-status-block"></a>状態の I/O ブロック

特定の要求

### <a name="operation"></a>操作

シリアルには、次の電源の要求がサポートされています。

* [IRP_MN_QUERY_POWER](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-query-power)
* [IRP_MN_SET_POWER](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-set-power)

シリアルは、下位レベルのドライバーを実行するすべての他の power 要求デバイス スタックを送信します。

シリアルでは、関数のドライバーまたは下位レベルのフィルター ドライバーとしてシリアルを使用するシリアル デバイス スタックの既定の電源ポリシー所有者です。

これらの要求の一般的な操作に関する詳細については、次を参照してください。 [Power Irp の処理の規則](https://docs.microsoft.com/windows-hardware/drivers/kernel/rules-for-handling-power-irps)します。

## <a name="irpmjqueryinformation"></a>IRP_MJ_QUERY_INFORMATION

[IRP_MJ_QUERY_INFORMATION](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-query-information)要求は、シリアル デバイスのファイルの情報をクエリします。 

### <a name="when-sent"></a>送信されたときに

クライアントは、標準的な情報を入手して、シリアル デバイス上に開かれたファイルに関する情報を配置するクエリ情報の要求を使用します。

### <a name="input-parameters"></a>入力パラメーター。

**Parameters.QueryFile.FileInformationClass**に設定されている**FileStandardInformation**または**FilePositionInformation**します。

### <a name="output-parameters"></a>出力パラメーター

|パラメーター|説明|
|----|----|
|**FileStandardInformation**|**AssociatedIrp.SystemBuffer**シリアルを使用して標準的な情報を出力するクライアントに割り当てられた FILE_STANDARD_INFORMATION 構造へのポインターします。|
|**FilePositionInformation**|**AssociatedIrp.SystemBuffer**位置情報を出力するシリアルを使用して、メンバーをクライアントに割り当てられた FILE_POSITION_INFORMATION 構造体をポイントします。|

### <a name="io-status-block"></a>状態の I/O ブロック

要求が成功した場合、**情報**メンバーが 0 に設定されます。

**状態**メンバーの状態値は次のいずれかに設定されます。

|状態値|説明|
|----|----|
|STATUS_SUCCESS|要求は正常に完了しました。|
|STATUS_CANCELLED|クライアントでは、要求が取り消されました。 シリアルは、デバイスのエラーが発生したデバイスのエラーがある場合は、要求をキャンセルするシリアルが構成されている場合も、要求をキャンセルします。|
|STATUS_DELETE_PENDING|シリアルは、デバイスを削除する予定です。|
|STATUS_INVALID_PARAMETER|要求された情報がサポートされていません。|
|STATUS_PENDING|シリアルには、後で処理要求がキューに登録します。|

### <a name="operation"></a>操作

シリアル型の要求をサポートする**FileStandardInformation**と**FilePositionInformation**します。

標準的なファイル情報は常に 0 に設定または**FALSE**必要に応じて、します。 位置情報は、0 を常に設定されます。

## <a name="irpmjread"></a>IRP_MJ_READ

A [IRP_MJ_READ](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-read)要求は、クライアントにシリアル デバイスからデータを転送します。

### <a name="when-sent"></a>送信されたときに

クライアントは、シリアル デバイス上のデータを読み取るたびに、読み取り要求を使用します。

### <a name="input-parameters"></a>入力パラメーター。

**Parameters.Read.Length**メンバーは、クライアントの読み取りバッファーに転送するバイト数に設定されます。

### <a name="output-parameters"></a>出力パラメーター

**AssociatedIrp.SystemBuffer**シリアル コピー データがシリアル デバイスでご覧クライアント割り当ての読み取りバッファーへのポインターします。

### <a name="io-status-block"></a>状態の I/O ブロック

**情報**メンバーをクライアントの読み取りバッファーに転送されたバイト数に設定されます。

**状態**メンバーは、次の値のいずれかに設定されます。

|状態値|説明|
|----|----|
|STATUS_SUCCESS|要求は正常に完了しました。|
|STATUS_CANCELLED|クライアントでは、要求が取り消されました。 シリアルは、デバイスのエラーが発生したデバイスのエラーがある場合は、要求をキャンセルするシリアルが構成されている場合も、要求をキャンセルします。|
|STATUS_DELETE_PENDING|シリアルは、デバイスを削除する予定です。|
|STATUS_PENDING|シリアルには、後で処理要求がキューに登録します。|
|STATUS_TIMEOUT|要求の完了時に、合計のタイムアウト値または間隔のタイムアウト値を超えています。|

### <a name="operation"></a>操作

クライアントは、読み取り要求を終了するのにタイムアウト イベントを使用することができます。 ただし、シリアル デバイスが開かれたときに、デバイスのタイムアウト設定を定義がありません。 カーネル モードのクライアントが使用できる、 [IOCTL_SERIAL_INTERNAL_BASIC_SETTINGS](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddser/ni-ntddser-ioctl_serial_internal_basic_settings)タイムアウト パラメーターを 0 (タイムアウトなしのイベントを使用) に設定します。 ユーザー モードとカーネル モードのクライアントが使用できる、 [IOCTL_SERIAL_SET_TIMEOUTS](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddser/ni-ntddser-ioctl_serial_set_timeouts)要求タイムアウト パラメーターを設定します。 

読み取りし、書き込みのタイムアウトについての詳細についてを参照してください。[設定の読み取りおよびシリアル デバイスの書き込みタイムアウト](https://docs.microsoft.com/previous-versions/ff547486(v=vs.85))します。

## <a name="irpmjsetinformation"></a>IRP_MJ_SET_INFORMATION

[IRP_MJ_SET_INFORMATION](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-shutdown)要求は、シリアル デバイスのファイルの情報を設定します。

### <a name="when-sent"></a>送信されたときに

クライアントは、シリアル デバイス上に開かれたファイルの現在のファイルの終端位置を変更するのにセット情報の要求を使用します。

### <a name="input-parameters"></a>入力パラメーター。
**Parameters.SetFile.FileInformationClass**に設定されているメンバー **FileEndOfFileInformation**または**FileAllocationInformation**します。

### <a name="output-parameters"></a>出力パラメーター

なし。

### <a name="io-status-block"></a>状態の I/O ブロック

要求が成功した場合、**情報**メンバーが 0 に設定されます。

**状態**メンバーの状態値は次のいずれかに設定されます。

|状態値|説明|
|----|----|
|STATUS_SUCCESS|要求は正常に完了しました。|
|STATUS_CANCELLED|クライアントでは、要求が取り消されました。 シリアルは、デバイスのエラーが発生したデバイスのエラーがある場合は、要求をキャンセルするシリアルが構成されている場合も、要求をキャンセルします。|
|STATUS_DELETE_PENDING|シリアルは、デバイスを削除する予定です。|
|STATUS_INVALID_PARAMETER|指定したファイルの情報がサポートされていません。|
|STATUS_PENDING|シリアルには、後で処理要求がキューに登録します。|

### <a name="operation"></a>操作

シリアル型の要求をサポートする**FileEndOfFileInformation**と**FileAllocationInformation**します。 ただし、シリアルはファイルの情報を実際には設定されません。 ファイルの終端位置は、0 を常に設定されます。

## <a name="irpmjsystemcontrol"></a>IRP_MJ_SYSTEM_CONTROL

[IRP_MJ_SYSTEM_CONTROL](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-system-control)要求は、WMI 要求をサポートしています。

### <a name="when-sent"></a>送信されたときに

WMI のカーネル モード コンポーネントは、シリアルがシリアル デバイス用の WMI プロバイダーとして登録した後、いつでも、IRP_MJ_SYSTEM_CONTROL 要求を送信できます。 WMI Irp 通常が送信されるユーザー モードのデータ コンシューマーが WMI データを要求されたときにします。

### <a name="input-parameters"></a>入力パラメーター。

特定の要求

### <a name="output-parameters"></a>出力パラメーター

特定の要求

### <a name="io-status-block"></a>状態の I/O ブロック

WMI 要求の場合は、シリアルは、次の値の 1 つに状態フィールドを設定します。

|状態値|説明|
|----|----|
|STATUS_SUCCESS|要求は正常に完了しました。|
|STATUS_BUFFER_TOO_SMALL|出力バッファーのバイト単位で、サイズは、要求された情報に必要なサイズより小さいです。|
|STATUS_INSUFFICIENT_RESOURCES|シリアル ポート名を保存する十分なシステム リソースが発生しました。|
|STATUS_INVALID_DEVICE_REQUEST|要求が無効です。|
|STATUS_WMI_GUID_NOT_FOUND|WMI の GUID を指定することはできません。|

### <a name="operation"></a>操作

シリアル使用[WmiSystemControl](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wmilib/nf-wmilib-wmisystemcontrol) WMI システム コントロールの要求を処理します。 シリアルが WMI ライブラリのコールバック ルーチンの次の種類を登録する**WmiSystemControl**デバイスに送信された WMI 要求を処理するために呼び出し。

* [DpWmiQueryReginfo](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wmilib/nc-wmilib-wmi_query_reginfo_callback)
* [DpWmiQueryDataBlock](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wmilib/nc-wmilib-wmi_query_datablock_callback)
* [DpWmiSetDataBlock](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wmilib/nc-wmilib-wmi_set_datablock_callback)
* [DpWmiSetDataItem](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wmilib/nc-wmilib-wmi_set_dataitem_callback)

シリアルでは、他のシステム コントロール要求はサポートされていません。 非 WMI 要求の場合は、シリアルは、現在のスタックの場所をスキップし、デバイス スタック ダウン要求を送信します。

シリアル レジスタ WMI GUID は、次の表で説明します。

シリアル WMI GUID に関連付けられているデータの構造 

| SERIAL_PORT_WMI_NAME_GUID | USHORT、WCSTR 続く |
| ------------------------- | -------------------------- |
| SERIAL_PORT_WMI_COMM_GUID | SERIAL_WMI_COMM_DATA |
| SERIAL_PORT_WMI_HW_GUID | SERIAL_WMI_HW_DATA |
| SERIAL_PORT_WMI_PERF_GUID | SERIAL_WMI_PERF_DATA |
| SERIAL_PORT_WMI_PROPERTIES_GUID | WMI_SERIAL_PORT_PROPERTIES |

シリアル デバイスの WMI 名前エントリの値の値である**PortName**デバイスのプラグ アンド プレイのレジストリ キーの下。

## <a name="irpmjwrite"></a>IRP_MJ_WRITE

[IRP_MJ_WRITE](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-write)要求がクライアントからシリアル デバイスにデータを転送します。

### <a name="when-sent"></a>送信されたときに

クライアントは、シリアル デバイスにデータを書き込むたびに、書き込み要求を使用します。

### <a name="input-parameters"></a>入力パラメーター。

**Parameters.Write.Length**メンバーは、クライアントに割り当てられた書き込みバッファーからシリアル デバイスにコピーするバイト数に設定されます。

**AssociatedIrp.SystemBuffer**メンバー ポイントをクライアントに割り当てられた書き込みバッファーにシリアル コピーする対象からデータをシリアル デバイスにします。

### <a name="output-parameters"></a>出力パラメーター

なし。

### <a name="io-status-block"></a>状態の I/O ブロック

*情報*メンバー シリアル デバイスにクライアントの書き込みバッファーから実際にコピーされたバイト数に設定されます。

*状態*メンバーは、次の値のいずれかに設定されます。

|状態値|説明|
|----|----|
|STATUS_SUCCESS|要求は正常に完了しました。|
|STATUS_CANCELLED|クライアントでは、要求が取り消されました。 シリアルは、デバイスのエラーが発生したデバイスのエラーがある場合は、要求をキャンセルするシリアルが構成されている場合も、要求をキャンセルします。|
|STATUS_DELETE_PENDING|シリアルは、デバイスを削除する予定です。|
|STATUS_PENDING|シリアルには、後で処理要求がキューに登録します。|
|STATUS_TIMEOUT|書き込み要求の合計時間を超過しました。|

### <a name="operation"></a>操作

クライアントは、タイムアウト イベントを使用して、書き込み要求を終了します。 ただし、シリアル デバイスが開かれると、デバイスの設定のタイムアウト イベントを定義はありません。 カーネル モードのクライアントが使用できる、 [IOCTL_SERIAL_INTERNAL_BASIC_SETTINGS](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddser/ni-ntddser-ioctl_serial_internal_basic_settings)タイムアウト パラメーターを 0 (タイムアウトなしのイベントを使用) に設定して、 [IOCTL_SERIAL_SET_TIMEOUTS](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddser/ni-ntddser-ioctl_serial_set_timeouts)要求タイムアウトを設定するにはパラメーター。 読み取りし、書き込みのタイムアウトについての詳細についてを参照してください。[設定の読み取りおよびシリアル デバイスの書き込みタイムアウト](https://docs.microsoft.com/previous-versions/ff547486(v=vs.85))します。

## <a name="related-topics"></a>関連トピック

[プラグ アンド プレイのマイナー Irp](https://docs.microsoft.com/windows-hardware/drivers/kernel/plug-and-play-minor-irps)

[電源 Irp を処理するための規則](https://docs.microsoft.com/windows-hardware/drivers/kernel/rules-for-handling-power-irps)

[コント ローラーのシリアル ドライバーの設計ガイド](https://docs.microsoft.com/en-us/windows-hardware/drivers/serports/)
