---
title: IRP_MJ_DIRECTORY_CONTROL 共用体の FLT_PARAMETERS
description: 操作の FLT\_IO\_パラメーター\_ブロック構造の MajorFunction フィールドが IRP\_MJ\_DIRECTORY\_コントロールである場合に使用される共用体コンポーネント。
ms.assetid: 3dadd64b-7e93-4c75-808d-2f26edb3ebd7
keywords:
- IRP_MJ_DIRECTORY_CONTROL union インストール可能ファイルシステムドライバーの FLT_PARAMETERS
- FLT_PARAMETERS union にインストール可能なファイルシステムドライバー
- PFLT_PARAMETERS union ポインターのインストール可能なファイルシステムドライバー
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
ms.openlocfilehash: c2c5c2cae4f514acc62514a50cc27a2551428132
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72841384"
---
# <a name="flt_parameters-for-irp_mj_directory_control-union"></a>IRP\_MJ\_DIRECTORY\_コントロール共用体の FLT\_パラメーター


操作の[**FLT\_IO\_パラメーター\_ブロック**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/ns-fltkernel-_flt_io_parameter_block)構造の**MajorFunction**フィールドが[**IRP\_MJ\_DIRECTORY\_コントロール**](irp-mj-directory-control.md)である場合に使用される共用体コンポーネント。

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
IRP\_に使用されるユニオンコンポーネント\_クエリ\_DIRECTORY 操作に使用されます。

**長さ**  
**Querydirectory. DirectoryBuffer**メンバーが指すバッファーの長さ (バイト単位)。

**/Db**  
指定したディレクトリ内のファイルの名前を含む[**UNICODE\_文字列**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfwdm/ns-wudfwdm-_unicode_string)構造体へのポインター。

**FileInformationClass**  
次に示す値のいずれかを指定します。

| Value                          | 意味                                                                                                                   |
|--------------------------------|---------------------------------------------------------------------------------------------------------------------------|
| ファイルのディレクトリ情報 (& i)   | 各ファイルの[ **\_DIR\_情報構造の両方\_ファイル**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/ns-ntifs-_file_both_dir_information)を返します。                      |
| FileDirectoryInformation       | 各ファイルの[**ファイル\_ディレクトリ\_情報**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/ns-ntifs-_file_directory_information)構造体を返します。                     |
| FileFullDirectoryInformation   | 各ファイルについて、[**ファイル\_完全\_DIR\_情報**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/ns-ntifs-_file_full_dir_information)構造体を返します。                      |
| FileIdBothDirectoryInformation | ファイル\_ID を返します。ファイルごとに[ **\_DIR\_情報構造の両方\_** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/ns-ntifs-_file_id_both_dir_information)ます。               |
| FileIdFullDirectoryInformation | ファイル\_ID を返します。ファイルは、各ファイルの[**完全\_DIR\_情報構造\_** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/ns-ntifs-_file_id_full_dir_information)ます。               |
| FileNamesInformation           | ファイル[ **\_名前\_情報**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/ns-ntifs-_file_names_information)構造体を返します。                             |
| FileObjectIdInformation        | 各ファイルの[**OBJECTID\_情報構造\_ファイル**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/ns-ntifs-_file_objectid_information)を返します。                       |
| FileReparsePointInformation    | ディレクトリの1つの[**ファイル\_再解析\_ポイント\_情報**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/ns-ntifs-_file_reparse_point_information)構造を返します。 |

 

**FileIndex**  
ディレクトリスキャンが開始されるファイルのインデックス。 SL\_インデックス\_指定したフラグが設定されていない場合は無視されます。 このパラメーターは、どの Win32 関数またはカーネルモードサポートルーチンでも指定できません。 現時点では、32ビットの NT ベースのオペレーティングシステムのみに存在する NT 仮想 DOS コンピューター (NTVDM) によってのみ使用されています。 ファイルインデックスは NTFS などのファイルシステムに対して定義されていないことに注意してください。これは、親ディレクトリ内のファイルの位置が固定されておらず、並べ替え順序を維持するためにいつでも変更できることに注意してください。

**DirectoryBuffer**  
ディレクトリの内容に関する要求された情報を受け取る、呼び出し元から提供される出力バッファーへのポインター。

**MdlAddress**  
**Querydirectory. DirectoryBuffer**メンバーが指すバッファーを記述するメモリ記述子リスト (MDL) のアドレス。 このメンバーは省略可能であり、 **NULL**にすることができます。

**NotifyDirectory**  
IRP\_を実行するために使用される共用体コンポーネント\_ディレクトリ操作を\_変更を通知\_ます。

**長さ**  
**Notifydirectory. DirectoryBuffer**メンバーが指すバッファーの長さ (バイト単位)。

**補完フィルター**  
通知リストの Irp を完了させる必要があるファイルまたはディレクトリに対する変更の種類を指定するフラグのビットマスク。 有効なフラグ値については、次に説明します。

| Flag                                | 意味                                                                        |
|-------------------------------------|--------------------------------------------------------------------------------|
| ファイル\_通知\_\_ファイルの\_名の変更    | このディレクトリでファイルが追加、削除、または名前が変更されました。                  |
| DIR\_NAME\_\_変更を通知\_ファイル     | サブディレクトリの作成、削除、または名前の変更が行われました。                          |
| \_名の変更を通知\_ファイル\_          | このディレクトリの名前は変更されました。                                             |
| \_属性\_変更を通知\_ファイル    | 最終アクセス時刻など、このファイルの属性の値が変更されました。 |
| ファイル\_通知\_\_サイズの変更          | このファイルのサイズが変更されました。                                                  |
| 最後\_書き込み\_変更を通知\_ファイル\_   | このファイルの最終更新時刻が変更されました。                                |
| 最後の\_アクセス\_変更を通知\_ファイル\_  | このファイルの最終アクセス時刻が変更されました。                                      |
| ファイル\_通知\_変更\_作成      | このファイルの作成時刻が変更されました。                                         |
| EA\_変更\_通知するファイル\_            | このファイルの拡張属性は変更されています。                            |
| セキュリティ\_\_の変更を通知するファイル\_      | このファイルのセキュリティ情報は変更されています。                                  |
| ストリーム\_名\_変更\_通知\_ファイル  | ファイルストリームがこのディレクトリで追加、削除、または名前変更されました。           |
| ストリーム\_サイズ\_\_変更を通知\_ファイル  | このファイルストリームのサイズが変更されました。                                           |
| ストリーム\_書き込み\_\_変更を通知\_ファイル | このファイルストリームのデータは変更されています。                                           |

 

**Spare1**  
現在使用されていません。

**Spare2**  
現在使用されていません。

**DirectoryBuffer**  
ディレクトリの内容に関する要求された情報を受け取る、呼び出し元から提供される出力バッファーへのポインター。

**MdlAddress**  
**Notifydirectory. directorybuffer**メンバーが指すバッファーを記述する MDL のアドレス。 このメンバーは省略可能であり、 **NULL**にすることができます。

<a name="remarks"></a>注釈
-------

IRP\_MJ\_DIRECTORY\_制御操作の[**FLT\_PARAMETERS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/ns-fltkernel-_flt_parameters)構造体には、コールバックデータで表される irp ベースのディレクトリ制御情報操作のパラメーターが含まれています ([**FLT\_コールバック\_データ**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/ns-fltkernel-_flt_callback_data)) 構造体。 これは、FLT\_IO\_パラメーター\_ブロック構造体に含まれています。

IRP\_MJ\_DIRECTORY\_CONTROL は、IRP ベースの操作です。

<a name="requirements"></a>要件
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p>Header</p></td>
<td align="left">Fltkernel .h (Fltkernel. h を含む)</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>関連項目


[**ファイル\_\_DIR\_の両方の情報**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/ns-ntifs-_file_both_dir_information)

[**ファイル\_ディレクトリ\_情報**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/ns-ntifs-_file_directory_information)

[**ファイル\_完全\_DIR\_情報**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/ns-ntifs-_file_full_dir_information)

[**ファイル\_ID\_\_の両方のディレクトリ\_情報**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/ns-ntifs-_file_id_both_dir_information)

[**ファイル\_ID\_完全\_ディレクトリの\_情報**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/ns-ntifs-_file_id_full_dir_information)

[**ファイル\_名\_情報**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/ns-ntifs-_file_names_information)

[**ファイル\_OBJECTID\_情報**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/ns-ntifs-_file_objectid_information)

[**ファイル\_再解析\_ポイント\_情報**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/ns-ntifs-_file_reparse_point_information)

[**FLT\_コールバック\_データ**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/ns-fltkernel-_flt_callback_data)

[**FLT\_IO\_パラメーター\_ブロック**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/ns-fltkernel-_flt_io_parameter_block)

[**FLT\_は\_高速な操作\_** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/index)

[**FLT\_は\_FS\_フィルターの\_操作です。** ](https://docs.microsoft.com/previous-versions/ff544648(v=vs.85))

[**FLT\_は\_IRP\_操作です**](https://docs.microsoft.com/previous-versions/ff544654(v=vs.85))

[**FLT\_パラメーター**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/ns-fltkernel-_flt_parameters)

[**FltNotifyFilterChangeDirectory**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltnotifyfilterchangedirectory)

[**FsRtlNotifyFilterChangeDirectory**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-_fsrtl_advanced_fcb_header-fsrtlnotifyfilterchangedirectory)

[**FsRtlNotifyFilterReportChange**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-_fsrtl_advanced_fcb_header-fsrtlnotifyfilterreportchange)

[**FsRtlNotifyFullChangeDirectory**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-_fsrtl_advanced_fcb_header-fsrtlnotifyfullchangedirectory)

[**FsRtlNotifyFullReportChange**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-_fsrtl_advanced_fcb_header-fsrtlnotifyfullreportchange)

[**IRP\_MJ\_DIRECTORY\_コントロール**](irp-mj-directory-control.md)

[**ZwQueryDirectoryFile**](https://msdn.microsoft.com/library/windows/hardware/ff567047)

 

 






