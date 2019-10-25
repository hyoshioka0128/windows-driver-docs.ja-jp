---
title: パラレル デバイスの I/O 要求に対するデバイス固有の操作
description: 並列デバイスの i/o 要求に対するデバイス固有の操作をドキュメント化します。
keywords:
- パラレルデバイス WDK
- パラレルドライバー WDK
- パラレル IRP コード
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 615d1e94a7a7b04edf7474183b60fed9b10114f2
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72831490"
---
# <a name="device-specific-operations-for-io-requests-for-parallel-devices"></a>パラレル デバイスの I/O 要求に対するデバイス固有の操作
このトピックでは、並列デバイスの i/o 要求に対する、デバイス固有の次の操作について説明します。

* [IRP_MJ_CREATE](#irp_mj_create)
* [IRP_MJ_DEVICE_CONTROL](#irp_mj_device_control)
* [IRP_MJ_INTERNAL_DEVICE_CONTROL](#irp_mj_internal_device_control)
* [IRP_MJ_QUERY_INFORMATION](#irp_mj_query_information)
* [IRP_MJ_READ](#irp_mj_read)
* [IRP_MJ_WRITE](#irp_mj_write)


##  <a name="irp_mj_create"></a>IRP_MJ_CREATE
[IRP_MJ_CREATE](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-create)要求によって、並列デバイスが開かれます。

### <a name="when-sent"></a>送信時
クライアントは、デバイスにアクセスする前に、 [IRP_MJ_CREATE](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-create)要求を使用して並列デバイスを開く必要があります。

### <a name="input-parameters"></a>入力パラメーター
なし。

### <a name="output-parameters"></a>出力パラメーター
なし。

### <a name="io-status-block"></a>I/O ステータス ブロック
情報メンバーが0に設定されています。

Status メンバーは、次のいずれかの値に設定されます。


STATUS_SUCCESS 

デバイスが正常に開かれました。

STATUS_ACCESS_DENIED 

デバイスは既に開いています。

STATUS_DELETE_PENDING 

デバイスの状態が "プラグアンドプレイ" になりました。

STATUS_DEVICE_REMOVED 

デバイスは削除されています。

STATUS_INVALID_DEVICE_REQUEST 

ハードウェアが存在しません。

STATUS_NOT_A_DIRECTORY 

デバイスがディレクトリではありません。

### <a name="operation"></a>操作
パラレルデバイスは、排他的なデバイスです。 パラレルデバイスが開いている場合、パラレルポート用のシステム提供のバスドライバーは、デバイスが閉じられるまで、デバイスに対する後続の[IRP_MJ_CREATE](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-create)要求をすべて失敗させます。 クライアントは、デバイスに他の i/o 要求を送信する前に、または[並列デバイスコールバックルーチン](https://docs.microsoft.com/windows-hardware/drivers/ddi/index)を呼び出すために、並列デバイスを開く必要があります。

詳細については、「[並列デバイスのオープンと使用](https://docs.microsoft.com/windows-hardware/drivers/parports/opening-and-using-a-parallel-device)」を参照してください。


##  <a name="irp_mj_device_control"></a>IRP_MJ_DEVICE_CONTROL
[IRP_MJ_DEVICE_CONTROL](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-device-control)要求は、並列デバイスを操作します。

### <a name="when-sent"></a>送信時
クライアントは、次の種類の操作に対してデバイス制御要求を使用します。

* デバイスに関する情報を取得する
* デバイスの動作モードの設定

「[デバイス制御要求」を](https://docs.microsoft.com/windows-hardware/drivers/ddi/index)参照してください。

### <a name="input-parameters"></a>入力パラメーター
要求固有。

### <a name="output-parameters"></a>出力パラメーター
要求固有。

### <a name="io-status-block"></a>I/O ステータス ブロック
**情報**メンバーは、要求に固有です。 

**Status**メンバーは、要求固有の値、または次の一般的な状態の値のいずれかに設定されます。


STATUS_SUCCESS
 
要求は正常に完了しました。

STATUS_CANCELLED 

要求は取り消されました。

STATUS_DELETE_PENDING 

デバイスは削除されています。

STATUS_DEVICE_REMOVED 

デバイスは削除されています。

STATUS_INVALID_PARAMETER 

パラレルポート用のシステム指定のバスドライバーは、要求をサポートしていません。

あります 

要求は保留中です。

STATUS_UNSUCCESSFUL 

要求が正常に完了しませんでした。

### <a name="operation"></a>操作
操作は、要求に固有です。


##  <a name="irp_mj_internal_device_control"></a>IRP_MJ_INTERNAL_DEVICE_CONTROL
[IRP_MJ_INTERNAL_DEVICE_CONTROL](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-internal-device-control)要求は、並列デバイスで内部の動作モードを設定します。

### <a name="when-sent"></a>送信時
クライアントは、次の種類の操作に対して内部デバイス制御要求を使用します。

* パラレルポートの通信モードを IEEE 1284 互換に設定する
* パラレルポートに関する接続情報の取得
* デバイスで排他的に使用するためにパラレルポートをロックおよびロック解除する

「[並列デバイスの内部デバイス制御要求」を](https://docs.microsoft.com/windows-hardware/drivers/ddi/index)参照してください。

### <a name="input-parameters"></a>入力パラメーター
要求固有。

### <a name="output-parameters"></a>出力パラメーター
要求固有。

### <a name="io-status-block"></a>I/O ステータス ブロック
**情報**メンバーは、要求に固有です。 

**Status**メンバーは、要求固有の値、または次の一般的な状態の値のいずれかに設定されます。


STATUS_SUCCESS
 
要求は正常に完了しました。

STATUS_CANCELLED 

要求は取り消されました。

STATUS_DELETE_PENDING 

デバイスは削除されています。

STATUS_DEVICE_REMOVED 

デバイスは削除されています。

STATUS_INVALID_PARAMETER 

パラレルバスドライバーは、要求をサポートしていません。

あります 

要求は保留中です。

STATUS_UNSUCCESSFUL 

要求が正常に完了しませんでした。

### <a name="operation"></a>操作

操作は、要求に固有です。


##  <a name="irp_mj_query_information"></a>IRP_MJ_QUERY_INFORMATION
[IRP_MJ_QUERY_INFORMATION](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-query-information)要求は、並列デバイスを表すファイルに関する情報を取得します。

### <a name="when-sent"></a>送信時
クライアントは、クエリ情報要求を送信して、ファイルサイズまたはファイルポインターの現在のバイトオフセットを決定します。

### <a name="input-parameters"></a>入力パラメーター
**パラメーター QueryFile. FileInformationClass**メンバーは**fileinformationclass**または**fileinformationclass**に設定されます。


**Filestandardinformation**要求:
 
**AssociatedIrp**のメンバーは、ファイル情報の出力に対してクライアントが割り当てる[FILE_STANDARD_INFORMATION](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_file_standard_information)構造体を指します。

**FILE_STANDARD_INFORMATION**構造体のサイズ (バイト単位) には、**パラメーターの値**を設定します。

**Filepositioninformation**要求: 

**AssociatedIrp**は、ファイル情報の出力にクライアントが割り当てる[FILE_POSITION_INFORMATION](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_file_position_information)構造体を指します。

**FILE_POSITION_INFORMATION**構造体の**パラメーターの値**は、バイト単位で設定されます。

### <a name="output-parameters"></a>出力パラメーター
**AssociatedIrp**は、要求された情報を参照します。

**Filestandardinformation**要求の種類: 

**FILE_STANDARD_INFORMATION**構造体の次のメンバーを設定します。

* **QuadPart**が0に設定されています。
* **Endoffile**は、割り当て**サイズ**のメンバーの値に設定されます。
* **Numberoflinks**は0に設定されます。
* **Deletepending**は**FALSE**に設定されています。
* **ディレクトリ**が**FALSE**に設定されています。

**Filepositioninformation**要求の種類:
 
**FILE_POSITION_INFORMATION**構造体の**currentbyteoffset. QuadPart**メンバーを0に設定します。

### <a name="io-status-block"></a>I/O ステータス ブロック
要求が成功した場合、**情報**メンバーは、要求の種類に関連付けられている構造体のサイズ (バイト単位) に設定されます。 それ以外の場合、**情報**メンバーは0に設定されます。

**Status**メンバーは、次のいずれかの状態値に設定されます。


STATUS_SUCCESS 

要求は正常に完了しました。

STATUS_BUFFER_TOO_SMALL 

入力パラメーターで指定された構造体のサイズ (バイト単位) が、要求の種類に関連付けられている構造体のバイト単位のサイズを下回っています。

STATUS_DEVICE_REMOVED 

デバイスは削除されています。

STATUS_INVALID_PARAMETER 

指定された種類の情報が無効です。

### <a name="operation"></a>操作
パラレルポート用のシステム提供のバスドライバーは、次の種類の情報に対するクエリをサポートしています。

* **FileStandardInformation**
* **FilePositionInformation**


##  <a name="irp_mj_read"></a>IRP_MJ_READ
[IRP_MJ_READ](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-read)要求は、並列デバイスから入力データを取得します。

### <a name="when-sent"></a>送信時
クライアントは、 [IRP_MJ_READ](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-read)要求を使用して、並列デバイスから入力を取得します。

### <a name="input-parameters"></a>入力パラメーター
**Parameters. Read. Length**メンバーは、並列デバイスから読み取るバイト数を指します。

### <a name="output-parameters"></a>出力パラメーター
**AssociatedIrp**のメンバーは、読み取りデータに対してクライアントが割り当てる読み取りバッファーを指します。 バッファーは、要求されたバイト数を保持するのに十分な大きさである必要があります。

### <a name="io-status-block"></a>I/O ステータス ブロック
**情報**メンバーは、並列デバイスから実際に読み取られたバイト数に設定されます。

**Status**メンバーは、次のいずれかの状態値に設定されます。


STATUS_SUCCESS
 
要求は正常に完了しました。

STATUS_DELETE_PENDING 

デバイスは削除されています。

STATUS_CANCELLED 

要求は取り消されました。

あります 

要求は、並列デバイスの作業キューでキューに登録されます。

STATUS_INVALID_PARAMETER 

**Parameters. 書き込み. ByteOffset**メンバーが0ではありません。 読み取り要求と書き込み要求は、どちらもこのメンバーを使用することに注意してください。

STATUS_DEVICE_REMOVED 

デバイスは削除されています。

### <a name="operation"></a>操作
パラレルポート用のシステム提供のバスドライバーは、並列デバイスに対して読み取りプロトコルセットを使用します。 既定の読み取りプロトコルは NIBBLE_MODE です。 クライアントは、 [IOCTL_IEEE1284_NEGOTIATE](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddpar/ni-ntddpar-ioctl_ieee1284_negotiate)要求を使用して、読み取りプロトコルをネゴシエートできます。

パラレルポートバスドライバーは、読み取り要求に対してキャンセルルーチンを設定し、読み取り要求を保留中としてマークし、ワークキューで読み取り要求をキューに入れます。 読み取り要求は、読み取り要求が完了するかクライアントによって取り消されるまでキャンセルできる状態で、ワークキューに保持されます。

詳細については、「[並列デバイスの読み取りと書き込み](https://docs.microsoft.com/windows-hardware/drivers/parports/reading-and-writing-a-parallel-device)」を参照してください。


##  <a name="irp_mj_write"></a>IRP_MJ_WRITE
[IRP_MJ_WRITE](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-write)要求は、出力データを並列デバイスに転送します。

### <a name="when-sent"></a>送信時
クライアントは、出力データを並列デバイスに転送するときに、 [IRP_MJ_WRITE](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-write)要求を使用します。

### <a name="input-parameters"></a>入力パラメーター
**AssociatedIrp バッファー**は、データ書き込み用にクライアントが割り当てた書き込みバッファーを指します。 バッファーは、並列デバイスに書き込むために要求されたバイト数を保持するのに十分な大きさである必要があります。

**Parameters. write. Length**メンバーは、並列デバイスに書き込むバイト数を指します。

### <a name="output-parameters"></a>出力パラメーター
なし。

### <a name="io-status-block"></a>I/O ステータス ブロック
**情報**メンバーは、実際に並列デバイスに書き込まれたバイト数に設定されます。

**Status**メンバーは、次のいずれかの値に設定されます。

STATUS_SUCCESS
 
要求は正常に完了しました。

STATUS_DELETE_PENDING 

デバイスは削除されています。

STATUS_CANCELLED 

要求は取り消されました。

あります 

要求は、並列デバイスの作業キューでキューに登録されます。

STATUS_INVALID_PARAMETER 

**Parameters. 書き込み. ByteOffset**メンバーが0ではありません。

STATUS_DEVICE_REMOVED 

デバイスは削除されています。

### <a name="operation"></a>操作
パラレルポート用のシステム提供のバスドライバーは、並列デバイスに設定されている書き込みプロトコルを使用してデータを転送します。 既定の書き込みプロトコルは、セントロニクスです。 クライアントは、 [IOCTL_IEEE1284_NEGOTIATE](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddpar/ni-ntddpar-ioctl_ieee1284_negotiate)要求を使用して書き込みプロトコルをネゴシエートできます。 

パラレルポートバスドライバーは、書き込み要求に対してキャンセルルーチンを設定し、書き込み要求を保留中としてマークし、ワークキューで書き込み要求をキューに入れます。 書き込み要求は、要求が完了するか取り消されるまでキャンセルできる状態で保持されます。

詳細については、「[並列デバイスの読み取りと書き込み](https://docs.microsoft.com/windows-hardware/drivers/parports/reading-and-writing-a-parallel-device)」を参照してください。

## <a name="related-topics"></a>関連トピック

[パラレルデバイスのデバイス制御要求](https://docs.microsoft.com/windows-hardware/drivers/ddi/index)。

[FILE_POSITION_INFORMATION](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_file_position_information) [FILE_STANDARD_INFORMATION](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_file_standard_information)

[並列デバイスを開いて使用する](https://docs.microsoft.com/windows-hardware/drivers/parports/opening-and-using-a-parallel-device)

[パラレルポートに接続されているパラレルデバイスの操作](https://docs.microsoft.com/windows-hardware/drivers/parports/operating-a-parallel-device-attached-to-a-parallel-port.md)

[並列デバイスのコールバックルーチン](https://docs.microsoft.com/windows-hardware/drivers/ddi/index)

[並列デバイスの読み取りと書き込み](https://docs.microsoft.com/windows-hardware/drivers/parports/reading-and-writing-a-parallel-device)

