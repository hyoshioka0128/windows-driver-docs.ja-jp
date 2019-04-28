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
ms.openlocfilehash: 68a729a2977356e243b4fe3ab6ddbb4455b8edde
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63365017"
---
# <a name="fltparameters-for-irpmjdirectorycontrol-union"></a>FLT\_IRP のパラメーター\_MJ\_ディレクトリ\_コントロール共用体


共用体のコンポーネントで使用されるときに、 **MajorFunction**のフィールド、 [ **FLT\_IO\_パラメーター\_ブロック**](https://msdn.microsoft.com/library/windows/hardware/ff544638)用の構造、操作が[ **IRP\_MJ\_ディレクトリ\_コントロール**](irp-mj-directory-control.md)します。

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

<a name="members"></a>メンバー
-------

**DirectoryControl**  
次のメンバーを含む構造体。

**QueryDirectory**  
IRP に使用される共用体のコンポーネント\_MN\_クエリ\_ディレクトリ操作。

**長さ**  
バッファーのバイト単位の長さを**QueryDirectory.DirectoryBuffer**へのポインターします。

**FileName**  
ポインターを[ **UNICODE\_文字列**](https://msdn.microsoft.com/library/windows/hardware/ff564879)指定されたディレクトリ内のファイルの名前を含む構造体。

**FileInformationClass**  
以下で説明する値のいずれかを指定します。

| 値                          | 説明                                                                                                                   |
|--------------------------------|---------------------------------------------------------------------------------------------------------------------------|
| FileBothDirectoryInformation   | 返す、 [**ファイル\_両方\_DIR\_情報**](https://msdn.microsoft.com/library/windows/hardware/ff540235)ファイルごとに構造体。                      |
| FileDirectoryInformation       | 返す、 [**ファイル\_ディレクトリ\_情報**](https://msdn.microsoft.com/library/windows/hardware/ff540248)ファイルごとに構造体。                     |
| FileFullDirectoryInformation   | 返す、 [**ファイル\_完全\_DIR\_情報**](https://msdn.microsoft.com/library/windows/hardware/ff540289)ファイルごとに構造体。                      |
| FileIdBothDirectoryInformation | 返す、 [**ファイル\_ID\_両方\_DIR\_情報**](https://msdn.microsoft.com/library/windows/hardware/ff540303)ファイルごとに構造体。               |
| FileIdFullDirectoryInformation | 返す、 [**ファイル\_ID\_完全\_DIR\_情報**](https://msdn.microsoft.com/library/windows/hardware/ff540310)ファイルごとに構造体。               |
| FileNamesInformation           | 返す、 [**ファイル\_名\_情報**](https://msdn.microsoft.com/library/windows/hardware/ff540329)ファイルごとに構造体。                             |
| FileObjectIdInformation        | 返す、 [**ファイル\_OBJECTID\_情報**](https://msdn.microsoft.com/library/windows/hardware/ff540335)ファイルごとに構造体。                       |
| FileReparsePointInformation    | 1 つを返す[**ファイル\_再解析\_ポイント\_情報**](https://msdn.microsoft.com/library/windows/hardware/ff540354)ディレクトリの構造体。 |

 

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

[ **FLT\_パラメーター** ](https://msdn.microsoft.com/library/windows/hardware/ff544673) IRP の構造\_MJ\_ディレクトリ\_管理操作には、IRP ベースのパラメーターが含まれています。ディレクトリ制御情報操作のコールバック データによって表される ([**FLT\_コールバック\_データ**](https://msdn.microsoft.com/library/windows/hardware/ff544620)) 構造体。 FLT に含まれている\_IO\_パラメーター\_ブロック構造体。

IRP\_MJ\_ディレクトリ\_コントロールが IRP ベースの操作。

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
<td align="left">Fltkernel.h (Fltkernel.h を含む)</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>関連項目


[**ファイル\_両方\_DIR\_情報**](https://msdn.microsoft.com/library/windows/hardware/ff540235)

[**ファイル\_ディレクトリ\_情報**](https://msdn.microsoft.com/library/windows/hardware/ff540248)

[**ファイル\_完全\_DIR\_情報**](https://msdn.microsoft.com/library/windows/hardware/ff540289)

[**ファイル\_ID\_両方\_DIR\_情報**](https://msdn.microsoft.com/library/windows/hardware/ff540303)

[**ファイル\_ID\_完全\_DIR\_情報**](https://msdn.microsoft.com/library/windows/hardware/ff540310)

[**ファイル\_名\_情報**](https://msdn.microsoft.com/library/windows/hardware/ff540329)

[**ファイル\_OBJECTID\_情報**](https://msdn.microsoft.com/library/windows/hardware/ff540335)

[**ファイル\_再解析\_ポイント\_情報**](https://msdn.microsoft.com/library/windows/hardware/ff540354)

[**FLT\_コールバック\_データ**](https://msdn.microsoft.com/library/windows/hardware/ff544620)

[**FLT\_IO\_PARAMETER\_BLOCK**](https://msdn.microsoft.com/library/windows/hardware/ff544638)

[**FLT\_IS\_FASTIO\_OPERATION**](https://msdn.microsoft.com/library/windows/hardware/ff544645)

[**FLT\_IS\_FS\_FILTER\_OPERATION**](https://msdn.microsoft.com/library/windows/hardware/ff544648)

[**FLT\_IS\_IRP\_OPERATION**](https://msdn.microsoft.com/library/windows/hardware/ff544654)

[**FLT\_PARAMETERS**](https://msdn.microsoft.com/library/windows/hardware/ff544673)

[**FltNotifyFilterChangeDirectory**](https://msdn.microsoft.com/library/windows/hardware/ff543377)

[**FsRtlNotifyFilterChangeDirectory**](https://msdn.microsoft.com/library/windows/hardware/ff547010)

[**FsRtlNotifyFilterReportChange**](https://msdn.microsoft.com/library/windows/hardware/ff547018)

[**FsRtlNotifyFullChangeDirectory**](https://msdn.microsoft.com/library/windows/hardware/ff547026)

[**FsRtlNotifyFullReportChange**](https://msdn.microsoft.com/library/windows/hardware/ff547041)

[**IRP\_MJ\_ディレクトリ\_コントロール**](irp-mj-directory-control.md)

[**ZwQueryDirectoryFile**](https://msdn.microsoft.com/library/windows/hardware/ff567047)

 

 






