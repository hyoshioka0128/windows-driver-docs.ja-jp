---
title: FLT_PARAMETERS IRP_MJ_DIRECTORY_CONTROL 共用体
description: 共用体のコンポーネントで使用されるときに、FLT の MajorFunction フィールド\_IO\_パラメーター\_操作のブロック構造は IRP\_MJ\_ディレクトリ\_コントロール。
ms.assetid: 3dadd64b-7e93-4c75-808d-2f26edb3ebd7
keywords:
- FLT_PARAMETERS IRP_MJ_DIRECTORY_CONTROL 共用体インストール可能なファイル システム ドライバー
- FLT_PARAMETERS union インストール可能なファイル システム ドライバー
- PFLT_PARAMETERS 共用体ポインター インストール可能なファイル システム ドライバー
topic_type:
- apiref
api_name:
- FLT_PARAMETERS
api_location:
- fltkernel.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1b1e50d5bc0ed67929eb7dc482893707e44dc7ee
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67380354"
---
# <a name="fltparameters-for-irpmjdirectorycontrol-union"></a>FLT\_IRP のパラメーター\_MJ\_ディレクトリ\_コントロール共用体


共用体のコンポーネントで使用されるときに、 **MajorFunction**のフィールド、 [ **FLT\_IO\_パラメーター\_ブロック**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fltkernel/ns-fltkernel-_flt_io_parameter_block)用の構造、操作が[ **IRP\_MJ\_ディレクトリ\_コントロール**](irp-mj-directory-control.md)します。

<a name="syntax"></a>構文
------

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

<a name="members"></a>Members
-------

**DirectoryControl**  
次のメンバーを含む構造体。

**QueryDirectory**  
IRP に使用される共用体のコンポーネント\_MN\_クエリ\_ディレクトリ操作。

**長さ**  
バッファーのバイト単位の長さを**QueryDirectory.DirectoryBuffer**へのポインターします。

**FileName**  
ポインターを[ **UNICODE\_文字列**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfwdm/ns-wudfwdm-_unicode_string)指定されたディレクトリ内のファイルの名前を含む構造体。

**FileInformationClass**  
以下で説明する値のいずれかを指定します。

| Value                          | 説明                                                                                                                   |
|--------------------------------|---------------------------------------------------------------------------------------------------------------------------|
| FileBothDirectoryInformation   | 返す、 [**ファイル\_両方\_DIR\_情報**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/ns-ntifs-_file_both_dir_information)ファイルごとに構造体。                      |
| FileDirectoryInformation       | 返す、 [**ファイル\_ディレクトリ\_情報**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/ns-ntifs-_file_directory_information)ファイルごとに構造体。                     |
| FileFullDirectoryInformation   | 返す、 [**ファイル\_完全\_DIR\_情報**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/ns-ntifs-_file_full_dir_information)ファイルごとに構造体。                      |
| FileIdBothDirectoryInformation | 返す、 [**ファイル\_ID\_両方\_DIR\_情報**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/ns-ntifs-_file_id_both_dir_information)ファイルごとに構造体。               |
| FileIdFullDirectoryInformation | 返す、 [**ファイル\_ID\_完全\_DIR\_情報**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/ns-ntifs-_file_id_full_dir_information)ファイルごとに構造体。               |
| FileNamesInformation           | 返す、 [**ファイル\_名\_情報**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/ns-ntifs-_file_names_information)ファイルごとに構造体。                             |
| FileObjectIdInformation        | 返す、 [**ファイル\_OBJECTID\_情報**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/ns-ntifs-_file_objectid_information)ファイルごとに構造体。                       |
| FileReparsePointInformation    | 1 つを返す[**ファイル\_再解析\_ポイント\_情報**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/ns-ntifs-_file_reparse_point_information)ディレクトリの構造体。 |

 

**FileIndex**  
ファイル ディレクトリのスキャンが開始位置のインデックス。 場合は無視されます、SL\_インデックス\_指定されたフラグは設定されません。 このパラメーターは、任意の Win32 関数またはカーネル モードのサポート ルーチンでは指定できません。 現在、NT 仮想 DOS コンピューター (NTVDM) 32 ビット NT ベースのオペレーティング システムにのみ存在するによってのみ使用されます。 ファイルのインデックスは、NTFS を親ディレクトリ内のファイルの位置が固定されていないと、並べ替え順序を維持するために、いつでも変更できますなど、ファイル システムに対して定義されていないことに注意してください。

**DirectoryBuffer**  
ディレクトリの内容に関する要求された情報を受け取る呼び出し元が指定の出力バッファーへのポインター。

**MdlAddress**  
バッファーを記述したメモリ記述子一覧 (MDL) のアドレスを**QueryDirectory.DirectoryBuffer**へのポインターします。 このメンバーは省略可能とは、 **NULL**します。

**NotifyDirectory**  
IRP に使用される共用体のコンポーネント\_MN\_通知\_変更\_ディレクトリ操作。

**長さ**  
バッファーのバイト単位の長さを**NotifyDirectory.DirectoryBuffer**へのポインターします。

**CompletionFilter**  
ファイルまたはディレクトリが完了する通知の一覧で、Irp をへの変更の種類を指定するフラグのビットマスク。 可能なフラグの値の次のとおりです。

| Flag                                | 説明                                                                        |
|-------------------------------------|--------------------------------------------------------------------------------|
| ファイル\_通知\_変更\_ファイル\_名    | ファイルは、追加、削除、またはこのディレクトリの名前が変更されています。                  |
| ファイル\_通知\_変更\_DIR\_名     | サブディレクトリを作成、削除、または名前が変更されています。                          |
| ファイル\_通知\_変更\_名          | このディレクトリの名前が変更されました。                                             |
| ファイル\_通知\_変更\_属性    | 最終アクセス日時など、このファイルの属性の値が変更されました。 |
| ファイル\_通知\_変更\_サイズ          | このファイルのサイズが変更されました。                                                  |
| ファイル\_通知\_変更\_最後\_書き込み   | このファイルの最終変更時刻が変更されました。                                |
| ファイル\_通知\_変更\_最後\_アクセス  | このファイルの最終アクセス時刻が変更されました。                                      |
| ファイル\_通知\_変更\_の作成      | このファイルの作成時刻が変更されました。                                         |
| ファイル\_通知\_変更\_EA            | このファイルの拡張属性が変更されています。                            |
| ファイル\_通知\_変更\_セキュリティ      | このファイルのセキュリティ情報が変更されました。                                  |
| ファイル\_通知\_変更\_ストリーム\_名  | ファイル ストリームは、追加、削除、またはこのディレクトリの名前が変更されています。           |
| ファイル\_通知\_変更\_ストリーム\_サイズ  | このファイル ストリームのサイズが変更されました。                                           |
| ファイル\_通知\_変更\_ストリーム\_書き込み | このファイル ストリームのデータが変更されました。                                           |

 

**spare1**  
使用されていません。

**Spare2**  
使用されていません。

**DirectoryBuffer**  
ディレクトリの内容に関する要求された情報を受け取る呼び出し元が指定の出力バッファーへのポインター。

**MdlAddress**  
MDL バッファーを記述するアドレスを**NotifyDirectory.DirectoryBuffer**へのポインターします。 このメンバーは省略可能とは、 **NULL**します。

<a name="remarks"></a>注釈
-------

[ **FLT\_パラメーター** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fltkernel/ns-fltkernel-_flt_parameters) IRP の構造\_MJ\_ディレクトリ\_管理操作には、IRP ベースのパラメーターが含まれています。ディレクトリ制御情報操作のコールバック データによって表される ([**FLT\_コールバック\_データ**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fltkernel/ns-fltkernel-_flt_callback_data)) 構造体。 FLT に含まれている\_IO\_パラメーター\_ブロック構造体。

IRP\_MJ\_ディレクトリ\_コントロールが IRP ベースの操作。

<a name="requirements"></a>必要条件
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p>Header</p></td>
<td align="left">Fltkernel.h (Fltkernel.h を含む)</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>関連項目


[**ファイル\_両方\_DIR\_情報**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/ns-ntifs-_file_both_dir_information)

[**ファイル\_ディレクトリ\_情報**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/ns-ntifs-_file_directory_information)

[**ファイル\_完全\_DIR\_情報**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/ns-ntifs-_file_full_dir_information)

[**ファイル\_ID\_両方\_DIR\_情報**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/ns-ntifs-_file_id_both_dir_information)

[**ファイル\_ID\_完全\_DIR\_情報**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/ns-ntifs-_file_id_full_dir_information)

[**ファイル\_名\_情報**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/ns-ntifs-_file_names_information)

[**ファイル\_OBJECTID\_情報**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/ns-ntifs-_file_objectid_information)

[**ファイル\_再解析\_ポイント\_情報**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/ns-ntifs-_file_reparse_point_information)

[**FLT\_コールバック\_データ**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fltkernel/ns-fltkernel-_flt_callback_data)

[**FLT\_IO\_PARAMETER\_BLOCK**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fltkernel/ns-fltkernel-_flt_io_parameter_block)

[**FLT\_IS\_FASTIO\_OPERATION**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/index)

[**FLT\_IS\_FS\_FILTER\_OPERATION**](https://docs.microsoft.com/previous-versions/ff544648(v=vs.85))

[**FLT\_IS\_IRP\_OPERATION**](https://docs.microsoft.com/previous-versions/ff544654(v=vs.85))

[**FLT\_PARAMETERS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fltkernel/ns-fltkernel-_flt_parameters)

[**FltNotifyFilterChangeDirectory**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fltkernel/nf-fltkernel-fltnotifyfilterchangedirectory)

[**FsRtlNotifyFilterChangeDirectory**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/nf-ntifs-_fsrtl_advanced_fcb_header-fsrtlnotifyfilterchangedirectory)

[**FsRtlNotifyFilterReportChange**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/nf-ntifs-_fsrtl_advanced_fcb_header-fsrtlnotifyfilterreportchange)

[**FsRtlNotifyFullChangeDirectory**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/nf-ntifs-_fsrtl_advanced_fcb_header-fsrtlnotifyfullchangedirectory)

[**FsRtlNotifyFullReportChange**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/nf-ntifs-_fsrtl_advanced_fcb_header-fsrtlnotifyfullreportchange)

[**IRP\_MJ\_ディレクトリ\_コントロール**](irp-mj-directory-control.md)

[**ZwQueryDirectoryFile**](https://msdn.microsoft.com/library/windows/hardware/ff567047)

 

 






