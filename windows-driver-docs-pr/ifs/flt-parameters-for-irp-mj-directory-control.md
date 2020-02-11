---
title: IRP_MJ_DIRECTORY_CONTROL 共用体の FLT_PARAMETERS
description: 操作の FLT_IO_PARAMETER_BLOCK 構造体の MajorFunction フィールドが IRP_MJ_DIRECTORY_CONTROL 場合に使用される共用体コンポーネント。
ms.assetid: 3dadd64b-7e93-4c75-808d-2f26edb3ebd7
keywords:
- IRP_MJ_DIRECTORY_CONTROL ユニオンインストール可能なファイルシステムドライバーの FLT_PARAMETERS
- ユニオンインストール可能なファイルシステムドライバーの FLT_PARAMETERS
- PFLT_PARAMETERS 共用体ポインターのインストール可能なファイルシステムドライバー
topic_type:
- apiref
api_name:
- FLT_PARAMETERS
api_location:
- fltkernel.h
api_type:
- HeaderDef
ms.date: 02/04/2020
ms.localizationpriority: medium
ms.openlocfilehash: 27f1b7e8a7369a6bbbd4218863c7290aa5c8001a
ms.sourcegitcommit: f64e64c9b2f15df154a5702e15e6a65243fc7f64
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/07/2020
ms.locfileid: "77072239"
---
# <a name="flt_parameters-for-irp_mj_directory_control-union"></a>IRP_MJ_DIRECTORY_CONTROL 共用体の FLT_PARAMETERS

操作の[**FLT_IO_PARAMETER_BLOCK**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/ns-fltkernel-_flt_io_parameter_block)構造体の**MajorFunction**フィールドが[**IRP_MJ_DIRECTORY_CONTROL**](irp-mj-directory-control.md)場合に使用される共用体コンポーネント。

## <a name="syntax"></a>構文

```ManagedCPlusPlus
typedef union _FLT_PARAMETERS {
  ...   ;
  union {
    struct {
      ULONG                   Length;
      PUNICODE_STRING         FileName;
      FILE_INFORMATION_CLASS  FileInformationClass;
      ULONG POINTER_ALIGNMENT FileIndex;
      PVOID                   DirectoryBuffer;
      PMDL                    MdlAddress;
    } QueryDirectory;
    struct {
      ULONG                   Length;
      ULONG POINTER_ALIGNMENT CompletionFilter;
      ULONG                   Spare1;
      ULONG POINTER_ALIGNMENT Spare2;
      PVOID                   DirectoryBuffer;
      PMDL                    MdlAddress;
    } NotifyDirectory;
  } DirectoryControl;
  ...   ;
} FLT_PARAMETERS, *PFLT_PARAMETERS;
```

## <a name="members"></a>Members

**DirectoryControl**  
次のメンバーを含む構造体。

**QueryDirectory**  
IRP_MN_QUERY_DIRECTORY 操作に使用される共用体コンポーネントです。

**長さ**  
**Querydirectory. DirectoryBuffer**メンバーが指すバッファーの長さ (バイト単位)。

**/Db**  
指定したディレクトリ内のファイルの名前を格納している[**UNICODE_STRING**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfwdm/ns-wudfwdm-_unicode_string)構造体へのポインター。

**FileInformationClass**  
次に示す値のいずれかを指定します。

| 値 | 意味 |
|-------|---------|
| ファイルのディレクトリ情報 (& i)   | 各ファイルの[**FILE_BOTH_DIR_INFORMATION**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/ns-ntifs-_file_both_dir_information)構造体を返します。                      |
| FileDirectoryInformation       | 各ファイルの[**FILE_DIRECTORY_INFORMATION**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/ns-ntifs-_file_directory_information)構造体を返します。                     |
| FileFullDirectoryInformation   | 各ファイルの[**FILE_FULL_DIR_INFORMATION**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/ns-ntifs-_file_full_dir_information)構造体を返します。                      |
| FileIdBothDirectoryInformation | 各ファイルの[**FILE_ID_BOTH_DIR_INFORMATION**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/ns-ntifs-_file_id_both_dir_information)構造体を返します。               |
| FileIdFullDirectoryInformation | 各ファイルの[**FILE_ID_FULL_DIR_INFORMATION**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/ns-ntifs-_file_id_full_dir_information)構造体を返します。               |
| FileNamesInformation           | 各ファイルの[**FILE_NAMES_INFORMATION**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/ns-ntifs-_file_names_information)構造体を返します。                             |
| FileObjectIdInformation        | 各ファイルの[**FILE_OBJECTID_INFORMATION**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/ns-ntifs-_file_objectid_information)構造体を返します。                       |
| FileReparsePointInformation    | ディレクトリの1つの[**FILE_REPARSE_POINT_INFORMATION**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/ns-ntifs-_file_reparse_point_information)構造体を返します。 |

**FileIndex**  
ディレクトリスキャンが開始されるファイルのインデックス。 SL_INDEX_SPECIFIED フラグが設定されていない場合は無視されます。 このパラメーターは、どの Win32 関数またはカーネルモードサポートルーチンでも指定できません。 現時点では、32ビットの NT ベースのオペレーティングシステムのみに存在する NT 仮想 DOS コンピューター (NTVDM) によってのみ使用されています。 ファイルインデックスは NTFS などのファイルシステムに対して定義されていないことに注意してください。これは、親ディレクトリ内のファイルの位置が固定されておらず、並べ替え順序を維持するためにいつでも変更できることに注意してください。

**DirectoryBuffer**  
ディレクトリの内容に関する要求された情報を受け取る、呼び出し元から提供される出力バッファーへのポインター。 このメンバーは省略可能であり、MDL が**Querydirectory. MdlAddress**に指定されている場合は NULL にすることができます。 「**解説**」を参照してください。

**MdlAddress**  
**Querydirectory. DirectoryBuffer**メンバーが指すバッファーを記述するメモリ記述子リスト (MDL) のアドレス。 このメンバーは省略可能であり、 **Querydirectory. directorybuffer**にバッファーが指定されている場合は**NULL**にすることができます。 「**解説**」を参照してください。

**NotifyDirectory**  
IRP_MN_NOTIFY_CHANGE_DIRECTORY 操作に使用される共用体コンポーネントです。

**長さ**  
**Notifydirectory. DirectoryBuffer**メンバーが指すバッファーの長さ (バイト単位)。

**補完フィルター**  
通知リストの Irp を完了させる必要があるファイルまたはディレクトリに対する変更の種類を指定するフラグのビットマスク。 有効なフラグ値については、次に説明します。

| Flag | 意味  |
|------|----------|
| FILE_NOTIFY_CHANGE_FILE_NAME    | このディレクトリでファイルが追加、削除、または名前が変更されました。                  |
| FILE_NOTIFY_CHANGE_DIR_NAME     | サブディレクトリの作成、削除、または名前の変更が行われました。                          |
| FILE_NOTIFY_CHANGE_NAME          | このディレクトリの名前は変更されました。                                             |
| FILE_NOTIFY_CHANGE_ATTRIBUTES    | 最終アクセス時刻など、このファイルの属性の値が変更されました。 |
| FILE_NOTIFY_CHANGE_SIZE          | このファイルのサイズが変更されました。                                                  |
| FILE_NOTIFY_CHANGE_LAST_WRITE   | このファイルの最終更新時刻が変更されました。                                |
| FILE_NOTIFY_CHANGE_LAST_ACCESS  | このファイルの最終アクセス時刻が変更されました。                                      |
| FILE_NOTIFY_CHANGE_CREATION      | このファイルの作成時刻が変更されました。                                         |
| FILE_NOTIFY_CHANGE_EA            | このファイルの拡張属性は変更されています。                            |
| FILE_NOTIFY_CHANGE_SECURITY      | このファイルのセキュリティ情報は変更されています。                                  |
| FILE_NOTIFY_CHANGE_STREAM_NAME  | ファイルストリームがこのディレクトリで追加、削除、または名前変更されました。           |
| FILE_NOTIFY_CHANGE_STREAM_SIZE  | このファイルストリームのサイズが変更されました。                                           |
| FILE_NOTIFY_CHANGE_STREAM_WRITE | このファイルストリームのデータは変更されています。                                           |

**Spare1**  
現在使用されていません。

**Spare2**  
現在使用されていません。

**DirectoryBuffer**  
ディレクトリの内容に関する要求された情報を受け取る、呼び出し元から提供される出力バッファーへのポインター。 このメンバーは省略可能であり、MDL が**Notifydirectory. MdlAddress**に指定されている場合は NULL にすることができます。 「**解説**」を参照してください。

**MdlAddress**  
**Notifydirectory. directorybuffer**メンバーが指すバッファーを記述する MDL のアドレス。 このメンバーは省略可能であり、 **Notifydirectory. directorybuffer**にバッファーが指定されている場合は**NULL**にすることができます。 「**解説**」を参照してください。

## <a name="remarks"></a>コメント

IRP_MJ_DIRECTORY_CONTROL 操作の[**FLT_PARAMETERS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/ns-fltkernel-_flt_parameters)構造体には、コールバックデータ ([**FLT_CALLBACK_DATA**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/ns-fltkernel-_flt_callback_data)) 構造体によって表される、IRP ベースのディレクトリ制御情報操作のパラメーターが含まれています。 これは FLT_IO_PARAMETER_BLOCK 構造体に含まれています。

**Directorybuffer**と**mdladdress**の両方のバッファーを指定する場合は、ミニフィルターで MDL を使用することをお勧めします。 **Directorybuffer**が指すメモリは、呼び出しプロセスのコンテキスト内でアクセスされているユーザーモードアドレスである場合、またはカーネルモードアドレスの場合に有効です。

ミニフィルターによって**mdladdress**の値が変更された場合、事後操作コールバックの後、フィルターマネージャーは現在**mdladdress**に格納されている MDL を解放し、 **mdladdress**の前の値を復元します。

IRP_MJ_DIRECTORY_CONTROL は、IRP ベースの操作です。

## <a name="requirements"></a>要件

|   |   |
| - | - |
| ヘッダー | Fltkernel .h (Fltkernel. h を含む) |

## <a name="see-also"></a>参照

[**FILE_BOTH_DIR_INFORMATION**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/ns-ntifs-_file_both_dir_information)

[**FILE_DIRECTORY_INFORMATION**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/ns-ntifs-_file_directory_information)

[**FILE_FULL_DIR_INFORMATION**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/ns-ntifs-_file_full_dir_information)

[**FILE_ID_BOTH_DIR_INFORMATION**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/ns-ntifs-_file_id_both_dir_information)

[**FILE_ID_FULL_DIR_INFORMATION**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/ns-ntifs-_file_id_full_dir_information)

[**FILE_NAMES_INFORMATION**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/ns-ntifs-_file_names_information)

[**FILE_OBJECTID_INFORMATION**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/ns-ntifs-_file_objectid_information)

[**FILE_REPARSE_POINT_INFORMATION**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/ns-ntifs-_file_reparse_point_information)

[**FLT_CALLBACK_DATA**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/ns-fltkernel-_flt_callback_data)

[**FLT_IO_PARAMETER_BLOCK**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/ns-fltkernel-_flt_io_parameter_block)

[**FLT_IS_FASTIO_OPERATION**](https://docs.microsoft.com/windows-hardware/drivers/ddi/index)

[**FLT_IS_FS_FILTER_OPERATION**](https://docs.microsoft.com/previous-versions/ff544648(v=vs.85))

[**FLT_IS_IRP_OPERATION**](https://docs.microsoft.com/previous-versions/ff544654(v=vs.85))

[**FLT_PARAMETERS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/ns-fltkernel-_flt_parameters)

[**FltNotifyFilterChangeDirectory**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltnotifyfilterchangedirectory)

[**FsRtlNotifyFilterChangeDirectory**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-_fsrtl_advanced_fcb_header-fsrtlnotifyfilterchangedirectory)

[**FsRtlNotifyFilterReportChange**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-_fsrtl_advanced_fcb_header-fsrtlnotifyfilterreportchange)

[**FsRtlNotifyFullChangeDirectory**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-_fsrtl_advanced_fcb_header-fsrtlnotifyfullchangedirectory)

[**FsRtlNotifyFullReportChange**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-_fsrtl_advanced_fcb_header-fsrtlnotifyfullreportchange)

[**IRP_MJ_DIRECTORY_CONTROL**](irp-mj-directory-control.md)

[**ZwQueryDirectoryFile**](https://msdn.microsoft.com/library/windows/hardware/ff567047)
