---
title: IRP_MJ_DIRECTORY_CONTROL (IFS)
description: IRP_MJ_DIRECTORY_CONTROL
ms.assetid: cb1bed36-bcb5-419b-87ca-6d9107ece6d1
keywords:
- インストール可能なファイルシステムドライバーの IRP_MJ_DIRECTORY_CONTROL
topic_type:
- apiref
api_name:
- IRP_MJ_DIRECTORY_CONTROL
api_type:
- NA
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7310b8f2946eda9847d0e8872e7592e4628c8e11
ms.sourcegitcommit: df50dc10210c124f2c7fb173d6e4fb796f56e5bd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/22/2020
ms.locfileid: "86949728"
---
# <a name="irp_mj_directory_control-ifs"></a>IRP_MJ_DIRECTORY_CONTROL (IFS)

## <a name="when-sent"></a>送信時

IRP_MJ_DIRECTORY_CONTROL 要求は、i/o マネージャーおよびその他のカーネルモードドライバーによって送信されます。 たとえば、ユーザーモードアプリケーションが**ReaddirectoryFindNextVolumeMountPoint w**や**FindNextVolumeMountPoint**などの Microsoft Win32 関数を呼び出したときや、カーネルモードコンポーネントが[**zwquerydirectoryfile**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-zwquerydirectoryfile)を呼び出したときなどに送信できます。

## <a name="operation-file-system-drivers"></a>操作: ファイルシステムドライバー

ファイルシステムドライバーは、マイナー関数のコードを確認して、どのディレクトリ制御操作が要求されているかを判断する必要があります。 有効なマイナー関数コードを次に示します。

| 期間 | 説明 |
| ---- | ----------- |
| IRP_MN_NOTIFY_CHANGE_DIRECTORY | ディレクトリへの変更の通知要求を示します。 通常、この要求をすぐに満たすのではなく、ファイルシステムドライバーが IRP をプライベートキューに保持します。 ディレクトリに変更が行われると、ファイルシステムドライバーは通知を実行し、デキューを実行して IRP を完了します。 |
| IRP_MN_QUERY_DIRECTORY | ディレクトリクエリ要求を示します。 照会できる情報の種類はファイルシステムによって異なりますが、一般的には次のものが含まれます。 FileFileIdFullDirectoryInformation Directoryinformation、FileDirectoryInformation、Filebothdirectoryinformation、FileIdBothDirectoryInformation、、FileNamesInformation、FileObjectIdInformation、FileReparsePointInformation |

> [!NOTE]
> FileQuotaInformation information クラスは互換性のために残されています。 代わりに[**IRP_MJ_QUERY_QUOTA**](irp-mj-query-quota.md)を使用する必要があります。

要求された操作を実行すると、ファイルシステムドライバーが IRP を完了する必要があります。

## <a name="operation-file-system-filter-drivers"></a>操作: ファイルシステムフィルタードライバー

フィルタードライバーは、この IRP をスタック上の次の下位のドライバーに渡す必要があります。

## <a name="parameters"></a>パラメーター

ファイルシステムまたはフィルタードライバーは、指定された IRP で[**Iogetlocation entiを**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iogetcurrentirpstacklocation)呼び出して、irp 内の独自の[**スタックの場所**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_io_stack_location)へのポインターを取得します。次の一覧には、 *irpsp*として示されています。 (IRP は、 *irp*として表示されます)。ドライバーは、「ディレクトリ制御要求の処理」で、IRP の次のメンバーと IRP スタックの場所に設定されている情報を使用できます。

*DeviceObject*  
ターゲットデバイスオブジェクトへのポインター。

*Irp >IoStatus*  
最終的な完了ステータスと要求された操作に関する情報を受け取る[**IO_STATUS_BLOCK**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_io_status_block)構造体へのポインター。

*Irp->UserBuffer*  
ディレクトリの内容に関する要求された情報を受け取る、呼び出し元から提供される出力バッファーへのポインター。

*IrpSp->FileObject*  
*DeviceObject*に関連付けられているファイルオブジェクトへのポインター。

*Irpsp->FileObject*パラメーターには、FILE_OBJECT 構造である、関連する**fileobject**フィールドへのポインターが含まれています。 FILE_OBJECT 構造体**の、IRP_MJ_DIRECTORY_CONTROL**の処理中には無効なので、使用することはできません。

*IrpSp->フラグ*  
IRP_MN_QUERY_DIRECTORY には、次のフラグを設定できます。

| フラグ | 意味 |
| ---- | ------- |
| SL_INDEX_SPECIFIED | *Irpsp->Parameters. QueryDirectory. FileIndex*によってインデックスが指定されているディレクトリのエントリでスキャンを開始します。 |
| SL_RESTART_SCAN | ディレクトリの最初のエントリでスキャンを開始します。 このフラグが設定されていない場合は、以前の IRP_MN_QUERY_DIRECTORY 要求からスキャンを再開します。 |
| SL_RETURN_SINGLE_ENTRY | 最初に見つかったエントリだけを返します。 |
| SL_RETURN_ON_DISK_ENTRIES_ONLY | ディレクトリの仮想化またはジャストインタイム拡張を実行するすべてのフィルターに対して、要求をファイルシステムに渡し、現在ディスク上にあるエントリを返すように指示します。 |

IRP_MN_NOTIFY_CHANGE_DIRECTORY には、次のフラグを設定できます。

| フラグ | 意味 |
| ---- | ------- |
| SL_WATCH_TREE | このディレクトリのすべてのサブディレクトリも監視する必要がある場合は、 **TRUE**に設定します。 ディレクトリ自体だけを監視する場合は、 **FALSE**に設定します。

*IrpSp->MajorFunction*  
IRP_MJ_DIRECTORY_CONTROL を指定します。

*IrpSp->MinorFunction*  
次のいずれか:

- IRP_MN_NOTIFY_CHANGE_DIRECTORY
- IRP_MN_QUERY_DIRECTORY

*IrpSp->Parameters. NotifyDirectory. このフィルター*  
詳細については、 [**Fsrtlnotifyfullchangedirectory**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-_fsrtl_advanced_fcb_header-fsrtlnotifyfullchangedirectory)への参照*フィルター*パラメーターの説明を参照してください。

*IrpSp->Parameters. NotifyDirectory. Length*  
*Irp >UserBuffer*が指すバッファーの長さ (バイト単位)。

*IrpSp->Parameters. QueryDirectory. FileIndex*  
ディレクトリスキャンを開始するファイルのインデックス。 SL_INDEX_SPECIFIED フラグが設定されていない場合は無視されます。 このパラメーターは、どの Win32 関数またはカーネルモードサポートルーチンでも指定できません。 現在、このファイルは、32ビットの NT ベースのプラットフォームのみに存在する NT 仮想 DOS コンピューター (NTVDM) によってのみ使用されます。 ファイルインデックスは NTFS などのファイルシステムに対して定義されていないことに注意してください。これは、親ディレクトリ内のファイルの位置が固定されておらず、並べ替え順序を維持するためにいつでも変更できることに注意してください。

*IrpSp->Parameters. QueryDirectory. FileInformationClass*  
次に示す値のいずれかを指定します。

| 値 | 意味 |
| ----- | ------- |
| **ファイルのディレクトリ情報 (& i)** | 各ファイルの[**FILE_BOTH_DIR_INFORMATION**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/ns-ntifs-_file_both_dir_information)構造体を返します。 |
| **FileDirectoryInformation** | 各ファイルの[**FILE_DIRECTORY_INFORMATION**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/ns-ntifs-_file_directory_information)構造体を返します。 |
| **FileFullDirectoryInformation** | 各ファイルの[**FILE_FULL_DIR_INFORMATION**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/ns-ntifs-_file_full_dir_information)"構造体を返します。 |
| **FileIdBothDirectoryInformation** | 各ファイルの[**FILE_ID_BOTH_DIR_INFORMATION**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/ns-ntifs-_file_id_both_dir_information)構造体を返します。 |
| **FileIdFullDirectoryInformation** | 各ファイルの[**FILE_ID_FULL_DIR_INFORMATION**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/ns-ntifs-_file_id_full_dir_information)構造体を返します。 |
| **FileNamesInformation** | 各ファイルの[**FILE_NAMES_INFORMATION**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/ns-ntifs-_file_names_information)構造体を返します。 |
| **FileObjectIdInformation** | 各ファイルの[**FILE_OBJECTID_INFORMATION**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/ns-ntifs-_file_objectid_information)構造体を返します。 |
| **FileQuotaInformation** | 互換性のために残されています。 代わりに[IRP_MJ_QUERY_QUOTA](irp-mj-query-quota.md)を使用してください。 |
| **FileReparsePointInformation** | ディレクトリの1つの[**FILE_REPARSE_POINT_INFORMATION**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/ns-ntifs-_file_reparse_point_information)構造体を返します。 |

*IrpSp->Parameters. QueryDirectory. FileName*  
指定したディレクトリ内のファイルの名前 (省略可能)。

*IrpSp->Parameters. QueryDirectory. Length*  
*Irp >UserBuffer*が指すバッファーの長さ (バイト単位)。

## <a name="see-also"></a>関連項目

[**FILE_BOTH_DIR_INFORMATION**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/ns-ntifs-_file_both_dir_information)

[**FILE_DIRECTORY_INFORMATION**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/ns-ntifs-_file_directory_information)

[**FILE_FULL_DIR_INFORMATION**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/ns-ntifs-_file_full_dir_information)

[**FILE_ID_BOTH_DIR_INFORMATION**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/ns-ntifs-_file_id_both_dir_information)

[**FILE_ID_FULL_DIR_INFORMATION**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/ns-ntifs-_file_id_full_dir_information)

[**FILE_NAMES_INFORMATION**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/ns-ntifs-_file_names_information)

[**FILE_OBJECTID_INFORMATION**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/ns-ntifs-_file_objectid_information)

[**FILE_REPARSE_POINT_INFORMATION**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/ns-ntifs-_file_reparse_point_information)

[**FsRtlNotifyFullChangeDirectory**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-_fsrtl_advanced_fcb_header-fsrtlnotifyfullchangedirectory)

[**IO_STACK_LOCATION**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_io_stack_location)

[**IO_STATUS_BLOCK**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_io_status_block)

[**Iogetlocation Entiの場所**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iogetcurrentirpstacklocation)

[**IRP**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_irp)

[**IRP_MJ_QUERY_QUOTA**](irp-mj-query-quota.md)

[**ZwQueryDirectoryFile**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-zwquerydirectoryfile)
