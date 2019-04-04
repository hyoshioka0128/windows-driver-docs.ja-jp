---
title: パラレル デバイスの I/O 要求に対するデバイス固有の操作
description: 並列のデバイスの I/O 要求の操作をデバイスに固有のドキュメントします。
keywords:
- 並列デバイス WDK
- 並列ドライバー WDK
- 並列 IRP コード
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 39f253f9095a330932c22673dc9b2f2528d618c4
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56573692"
---
# <a name="device-specific-operations-for-io-requests-for-parallel-devices"></a>パラレル デバイスの I/O 要求に対するデバイス固有の操作
このトピックでは、並列のデバイスの I/O 要求の次のデバイスに固有の操作をドキュメントします。

* [IRP_MJ_CREATE](#irp_mj_create)
* [IRP_MJ_DEVICE_CONTROL](#irp_mj_device_control)
* [IRP_MJ_INTERNAL_DEVICE_CONTROL](#irp_mj_internal_device_control)
* [IRP_MJ_QUERY_INFORMATION](#irp_mj_query_information)
* [IRP_MJ_READ](#irp_mj_read)
* [IRP_MJ_WRITE](#irp_mj_write)


##  <a name="irpmjcreate"></a>IRP_MJ_CREATE
[Irp_mj_create 用](https://msdn.microsoft.com/library/windows/hardware/ff550729)要求は、並列のデバイスを開きます。

### <a name="when-sent"></a>送信時
クライアントを使用する必要があります、 [irp_mj_create 用](https://msdn.microsoft.com/library/windows/hardware/ff550729)をデバイスにアクセスできる前に、並列のデバイスを開く要求。

### <a name="input-parameters"></a>入力パラメーター
なし。

### <a name="output-parameters"></a>出力パラメーター
なし。

### <a name="io-status-block"></a>I/O ステータス ブロック
情報メンバーは、0 に設定されます。

状態のメンバーは、次の値のいずれかに設定されます。


STATUS_SUCCESS 

デバイスが正常に開きました。

STATUS_ACCESS_DENIED 

デバイスは既に開いています。

STATUS_DELETE_PENDING 

デバイスが、プラグ アンド プレイに驚きを削除状態。

STATUS_DEVICE_REMOVED 

デバイスが削除されました。

STATUS_INVALID_DEVICE_REQUEST 

ハードウェアが存在することはありません。

STATUS_NOT_A_DIRECTORY 

デバイスは、ディレクトリではありません。

### <a name="operation"></a>操作
並列デバイスは、排他的なデバイスです。 並列デバイスが開いている場合は、パラレル ポートのシステム提供のバス ドライバーがその後で失敗した[irp_mj_create 用](https://msdn.microsoft.com/library/windows/hardware/ff550729)まで、デバイスが閉じられているデバイスを要求します。 デバイスまたは呼び出しに他の I/O 要求を送信する前に、クライアントは並列のデバイスを開く必要があります、[デバイス コールバック ルーチンを並列](https://msdn.microsoft.com/library/windows/hardware/ff544275)します。

詳細については、[の起動と使用の並列デバイス](https://msdn.microsoft.com/windows/hardware/drivers/parports/opening-and-using-a-parallel-device)を参照してください。


##  <a name="irpmjdevicecontrol"></a>IRP_MJ_DEVICE_CONTROL
[IRP_MJ_DEVICE_CONTROL](https://msdn.microsoft.com/library/windows/hardware/ff550744)要求が並列デバイスは動作します。

### <a name="when-sent"></a>送信時
クライアントは、次の種類の操作のデバイス制御要求を使用します。

* デバイスに関する情報を取得します。
* デバイスの動作モードを設定します。

参照してください[並列のデバイスのデバイスのコントロール要求](https://msdn.microsoft.com/library/windows/hardware/ff543945)します。

### <a name="input-parameters"></a>入力パラメーター
要求ごとに固有です。

### <a name="output-parameters"></a>出力パラメーター
要求ごとに固有です。

### <a name="io-status-block"></a>I/O ステータス ブロック
**情報**メンバーは、要求ごとに固有です。 

**状態**要求固有の値または汎用的な状態の値を次のいずれかにメンバーを設定します。


STATUS_SUCCESS
 
要求は正常に完了しました。

STATUS_CANCELLED 

要求が取り消されました。

STATUS_DELETE_PENDING 

デバイスが削除中です。

STATUS_DEVICE_REMOVED 

デバイスが削除されました。

STATUS_INVALID_PARAMETER 

パラレル ポートのシステム提供のバス ドライバーは、要求をサポートしていません。

STATUS_PENDING 

保留中の要求です。

STATUS_UNSUCCESSFUL 

要求が正常に完了しませんでした。

### <a name="operation"></a>操作
操作は、要求ごとに固有です。


##  <a name="irpmjinternaldevicecontrol"></a>IRP_MJ_INTERNAL_DEVICE_CONTROL
[IRP_MJ_INTERNAL_DEVICE_CONTROL](https://msdn.microsoft.com/library/windows/hardware/ff550766)並列デバイスで要求が内部の動作モードを設定します。

### <a name="when-sent"></a>送信時
クライアントは、次の種類の操作の内部デバイス制御要求を使用します。

* IEEE 1284 と互換性のある、パラレル ポートの通信モードに設定します。
* パラレル ポートに関する接続情報を取得します。
* ロックし、デバイスによって排他的に使用の並列のポートをロック解除

内部参照[並列のデバイスのデバイスのコントロール要求](https://msdn.microsoft.com/library/windows/hardware/ff543945)します。

### <a name="input-parameters"></a>入力パラメーター
要求ごとに固有です。

### <a name="output-parameters"></a>出力パラメーター
要求ごとに固有です。

### <a name="io-status-block"></a>I/O ステータス ブロック
**情報**メンバーは、要求ごとに固有です。 

**状態**要求固有の値または汎用的な状態の値を次のいずれかにメンバーを設定します。


STATUS_SUCCESS
 
要求は正常に完了しました。

STATUS_CANCELLED 

要求が取り消されました。

STATUS_DELETE_PENDING 

デバイスが削除中です。

STATUS_DEVICE_REMOVED 

デバイスが削除されました。

STATUS_INVALID_PARAMETER 

並列バス ドライバーは、要求をサポートしていません。

STATUS_PENDING 

保留中の要求です。

STATUS_UNSUCCESSFUL 

要求が正常に完了しませんでした。

### <a name="operation"></a>操作

操作は、要求ごとに固有です。


##  <a name="irpmjqueryinformation"></a>IRP_MJ_QUERY_INFORMATION
[IRP_MJ_QUERY_INFORMATION](https://msdn.microsoft.com/library/windows/hardware/ff550788)要求は、並列のデバイスを表すファイルに関する情報を取得します。

### <a name="when-sent"></a>送信時
クライアントは、ファイル サイズまたはファイル ポインターの現在のバイト オフセットを決定するクエリ情報の要求を送信します。

### <a name="input-parameters"></a>入力パラメーター
**Parameters.QueryFile.FileInformationClass**に設定されているメンバー **FileStandardInformation**または**FilePositionInformation**します。


**FileStandardInformation**要求。
 
**AssociatedIrp.SystemBuffer**へのポインターを[FILE_STANDARD_INFORMATION](https://msdn.microsoft.com/library/windows/hardware/ff545855)ファイル情報の出力をクライアントによって割り当てられる構造体。

**Parameters.QueryFile.Length**メンバーがバイト単位のサイズの設定、 **FILE_STANDARD_INFORMATION**構造体。

**FilePositionInformation**要求。 

**AssociatedIrp.SystemBuffer**を指す、 [FILE_POSITION_INFORMATION](https://msdn.microsoft.com/library/windows/hardware/ff545848)ファイル情報の出力をクライアントによって割り当てられる構造体。

**Parameters.SetFile.Length**メンバーがバイト単位のサイズの設定、 **FILE_POSITION_INFORMATION**構造体。

### <a name="output-parameters"></a>出力パラメーター
**AssociatedIrp.SystemBuffer**要求された情報を指します。

**FileStandardInformation**要求の種類。 

次のメンバーを設定、 **FILE_STANDARD_INFORMATION**構造体。

* **AllocationSize.QuadPart**を 0 に設定します。
* **EndOfFile**の値に設定されている、 **AllocationSize**メンバー。
* **NumberOfLinks** 0 に設定されます。
* **表示されます**に設定されている**FALSE**します。
* **ディレクトリ**に設定されている**FALSE**します。

**FilePositionInformation**要求の種類。
 
セット、 **CurrentByteOffset.QuadPart**のメンバー、 **FILE_POSITION_INFORMATION**構造体をゼロにします。

### <a name="io-status-block"></a>I/O ステータス ブロック
要求が成功した場合、**情報**メンバー要求の種類に関連付けられている構造体のバイト単位のサイズに設定されます。 それ以外の場合、**情報**メンバーが 0 に設定されます。

**状態**メンバーの状態値は次のいずれかに設定されます。


STATUS_SUCCESS 

要求は正常に完了しました。

STATUS_BUFFER_TOO_SMALL 

入力パラメーターで指定された構造体のバイト単位のサイズは、要求の種類に関連付けられている構造体のバイト単位のサイズより小さい。

STATUS_DEVICE_REMOVED 

デバイスが削除されました。

STATUS_INVALID_PARAMETER 

指定した型の情報が無効です。

### <a name="operation"></a>操作
パラレル ポートのシステム提供のバス ドライバーには、次の情報の種類のクエリがサポートされています。

* **FileStandardInformation**
* **FilePositionInformation**


##  <a name="irpmjread"></a>IRP_MJ_READ
[IRP_MJ_READ](https://msdn.microsoft.com/library/windows/hardware/ff550794)要求は、並列のデバイスから入力データを取得します。

### <a name="when-sent"></a>送信時
クライアントを使用して、 [IRP_MJ_READ](https://msdn.microsoft.com/library/windows/hardware/ff550794)並列デバイスからの入力を取得する要求。

### <a name="input-parameters"></a>入力パラメーター
**Parameters.Read.Length**並列のデバイスから読み取るバイト数へのポインターします。

### <a name="output-parameters"></a>出力パラメーター
**AssociatedIrp.SystemBuffer**読み取りデータのクライアントによって割り当てられる読み取りバッファーへのポインターします。 バッファーは、要求されたバイト数を保持するために十分な大きさである必要があります。

### <a name="io-status-block"></a>I/O ステータス ブロック
**情報**メンバーの並列のデバイスから実際に読み取られたバイト数に設定されます。

**状態**メンバーの状態値は次のいずれかに設定されます。


STATUS_SUCCESS
 
要求は正常に完了しました。

STATUS_DELETE_PENDING 

デバイスが削除中です。

STATUS_CANCELLED 

要求が取り消されました。

STATUS_PENDING 

要求は、並列のデバイス用の作業キューにキューに配置します。

STATUS_INVALID_PARAMETER 

**Parameters.Write.ByteOffset**メンバーは 0 ではありません。 読み取りし、書き込み要求の使用にこのメンバー両方ことに注意してください。

STATUS_DEVICE_REMOVED 

デバイスが削除されました。

### <a name="operation"></a>操作
パラレル ポートのシステム提供のバス ドライバーでは、並列のデバイスの読み取りのプロトコルを使用します。 既定では、プロトコルは NIBBLE_MODE を読み取る。 クライアントを使用して読み取りのプロトコルをネゴシエートすることができます、 [IOCTL_IEEE1284_NEGOTIATE](https://msdn.microsoft.com/library/windows/hardware/ff543978)要求。

パラレル ポート バス ドライバーは、読み取り要求のキャンセル ルーチンの設定、読み取り要求を保留をマークし、作業キューに読み取り要求をキューします。 読み取り要求は、読み取り要求が完了したか、クライアントによって取り消されましたまでキャンセル可能な状態での作業キューに保持されます。

詳細については、[並列デバイスの読み書き](https://msdn.microsoft.com/windows/hardware/drivers/parports/reading-and-writing-a-parallel-device)を参照してください。


##  <a name="irpmjwrite"></a>IRP_MJ_WRITE
[IRP_MJ_WRITE](https://msdn.microsoft.com/library/windows/hardware/ff550819)要求は、並列のデバイスに出力データを転送します。

### <a name="when-sent"></a>送信時
クライアントを使用して、 [IRP_MJ_WRITE](https://msdn.microsoft.com/library/windows/hardware/ff550819)並列デバイスに出力データを転送するときに要求します。

### <a name="input-parameters"></a>入力パラメーター
**AssociatedIrp.SystemBuffer**のクライアントによって割り当てられる書き込みバッファーへのポインターがデータを書き込みます。 バッファーは、要求された並列のデバイスに書き込むバイト数を保持するために十分な大きさである必要があります。

**Parameters.Write.Length**並列のデバイスに書き込むバイト数へのポインターします。

### <a name="output-parameters"></a>出力パラメーター
なし。

### <a name="io-status-block"></a>I/O ステータス ブロック
**情報**メンバーの並列のデバイスに実際に書き込まれたバイト数に設定されます。

**状態**メンバーは、次の値のいずれかに設定されます。

STATUS_SUCCESS
 
要求は正常に完了しました。

STATUS_DELETE_PENDING 

デバイスが削除中です。

STATUS_CANCELLED 

要求が取り消されました。

STATUS_PENDING 

要求は、並列のデバイス用の作業キューにキューに配置します。

STATUS_INVALID_PARAMETER 

**Parameters.Write.ByteOffset**メンバーは 0 ではありません。

STATUS_DEVICE_REMOVED 

デバイスが削除されました。

### <a name="operation"></a>操作
パラレル ポートのシステム提供のバス ドライバーでは、並列のデバイスに設定されている書き込みプロトコルを使用してデータを転送します。 既定の書き込みプロトコルは、セントロニクスです。 クライアントを使用して書き込みプロトコルをネゴシエートすることができます、 [IOCTL_IEEE1284_NEGOTIATE](https://msdn.microsoft.com/library/windows/hardware/ff543978)要求。 

パラレル ポート バス ドライバー、書き込み要求のキャンセル ルーチンを設定するには、書き込み要求、保留中としてマークおよび作業キューに書き込み要求のキューします。 書き込み要求は、要求が完了またはキャンセルされるまでにキャンセルできる状態に保持されます。

詳細については、[並列デバイスの読み書き](https://msdn.microsoft.com/windows/hardware/drivers/parports/reading-and-writing-a-parallel-device)を参照してください。

## <a name="related-topics"></a>関連トピック

[並列のデバイスのデバイスのコントロール要求](https://msdn.microsoft.com/library/windows/hardware/ff543945)します。

[FILE_POSITION_INFORMATION](https://msdn.microsoft.com/library/windows/hardware/ff545848) [FILE_STANDARD_INFORMATION](https://msdn.microsoft.com/library/windows/hardware/ff545855)

[起動と使用の並列のデバイス](https://msdn.microsoft.com/windows/hardware/drivers/parports/opening-and-using-a-parallel-device)

[パラレル ポートに接続されている並列のデバイスの動作](https://msdn.microsoft.com/windows/hardware/drivers/parports/operating-a-parallel-device-attached-to-a-parallel-port.md)

[並列デバイス コールバック ルーチン](https://msdn.microsoft.com/library/windows/hardware/ff544275)

[並列のデバイスの読み取りと書き込み](https://msdn.microsoft.com/windows/hardware/drivers/parports/reading-and-writing-a-parallel-device)

