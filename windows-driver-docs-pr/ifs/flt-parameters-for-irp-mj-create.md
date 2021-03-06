---
title: FLT_PARAMETERS irp_mj_create 用共用体
description: 次の共用体のコンポーネントが使用されるときに、FLT の MajorFunction フィールド\_IO\_パラメーター\_操作のブロック構造は IRP\_MJ\_作成。
ms.assetid: aa223d51-7d13-4244-bad5-db14f1fb0d2c
keywords:
- FLT_PARAMETERS irp_mj_create 用共用体インストール可能なファイル システム ドライバー
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
ms.openlocfilehash: 2b1ec07e063f906516e394124acaccc94f390a4d
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67386077"
---
# <a name="fltparameters-for-irpmjcreate-union"></a>FLT\_IRP のパラメーター\_MJ\_共用体の作成


次の共用体のコンポーネントが使用されるときに、 **MajorFunction**のフィールド、 [ **FLT\_IO\_パラメーター\_ブロック**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fltkernel/ns-fltkernel-_flt_io_parameter_block)操作は構造体[ **IRP\_MJ\_作成**](irp-mj-create.md)します。

<a name="syntax"></a>構文
------

```ManagedCPlusPlus
typedef union _FLT_PARAMETERS {
  ...    ;
  struct {
    PIO_SECURITY_CONTEXT     SecurityContext;
    ULONG                    Options;
    USHORT POINTER_ALIGNMENT FileAttributes;
    USHORT                   ShareAccess;
    USHORT POINTER_ALIGNMENT EaLength;
    PVOID                    EaBuffer;
    LARGE_INTEGER            AllocationSize;
  } Create;
  ...    ;
} FLT_PARAMETERS, *PFLT_PARAMETERS;
```

<a name="members"></a>メンバー
-------

**作成**  
次のメンバーを含む構造体。

**SecurityContext**  
SecurityContext-&gt;AccessState

ポインター、 [**アクセス\_状態**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/ns-wdm-_access_state)オブジェクトのサブジェクトのコンテキストを含んでいる構造体のアクセスが許可の種類、および残りの必要なアクセスの種類。

SecurityContext-&gt;DesiredAccess

[**アクセス\_マスク**](https://docs.microsoft.com/windows-hardware/drivers/kernel/access-mask)ファイルに対して要求されたアクセス権を指定する構造体。 詳細については、次を参照してください。、 *DesiredAccess*パラメーターを[ **FltCreateFile**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fltkernel/nf-fltkernel-fltcreatefile)します。

**[オプション]**  
作成またはファイルが既に存在する場合に実行されるアクションと同様に、ファイルを開くときに適用されるオプションを指定するフラグのビットマスク。 このメンバーの下位 24 ビットに対応しています、 *CreateOptions*パラメーターを[ **FltCreateFile**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fltkernel/nf-fltkernel-fltcreatefile)します。 上位の 8 ビットに対応しています、 *CreateDisposition*パラメーターを**FltCreateFile**します。

**FileAttributes**  
属性の作成またはファイルを開く際に適用するビット マスク。 詳細については、次を参照してください。、 *FileAttributes*パラメーターを[ **FltCreateFile**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fltkernel/nf-fltkernel-fltcreatefile)します。

**ShareAccess**  
ファイルに、要求は共有アクセス権限のビットマスクです。 このパラメーターが 0 の場合は、排他的アクセスが要求されています。 詳細については、次を参照してください。、 *ShareAccess*パラメーターを[ **FltCreateFile**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fltkernel/nf-fltkernel-fltcreatefile)します。

**EaLength**  
バッファーのバイト単位の長さを**EaBuffer**へのポインターします。 詳細については、次を参照してください。、 *EaLength*パラメーターを[ **FltCreateFile**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fltkernel/nf-fltkernel-fltcreatefile)します。

**EaBuffer**  
呼び出し元が指定へのポインター [**ファイル\_完全\_EA\_情報**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/ns-wdm-_file_full_ea_information)-に適用される拡張属性 (EA) の情報を格納している構造化されたバッファーファイルです。 詳細については、次を参照してください。、 *EaBuffer*パラメーターを[ **FltCreateFile**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fltkernel/nf-fltkernel-fltcreatefile)します。

**AllocationSize**  
必要に応じて、ファイルのバイト単位で初期割り当てサイズを指定します。 0 以外の値及ぼしませんしない限り、ファイルが作成されている、上書き、または置き換えできます。 詳細については、次を参照してください。、 *AllocationSize*パラメーターを[ **FltCreateFile**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fltkernel/nf-fltkernel-fltcreatefile)します。

<a name="remarks"></a>コメント
-------

[ **FLT\_パラメーター** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fltkernel/ns-fltkernel-_flt_parameters)用の構造、 [ **IRP\_MJ\_作成**](irp-mj-create.md)操作コールバック データによって表される ([**FLT\_コールバック\_データ**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fltkernel/ns-fltkernel-_flt_callback_data)) 構造体。 含まれている、 [ **FLT\_IO\_パラメーター\_ブロック**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fltkernel/ns-fltkernel-_flt_io_parameter_block)構造体。

IRP\_MJ\_作成は IRP ベースの操作。

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


[**アクセス\_マスク**](https://docs.microsoft.com/windows-hardware/drivers/kernel/access-mask)

[**アクセス\_状態**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/ns-wdm-_access_state)

[**ファイル\_完全\_EA\_情報**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/ns-wdm-_file_full_ea_information)

[**FLT\_コールバック\_データ**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fltkernel/ns-fltkernel-_flt_callback_data)

[**FLT\_IO\_PARAMETER\_BLOCK**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fltkernel/ns-fltkernel-_flt_io_parameter_block)

[**FLT\_IS\_FASTIO\_OPERATION**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/index)

[**FLT\_IS\_FS\_FILTER\_OPERATION**](https://docs.microsoft.com/previous-versions/ff544648(v=vs.85))

[**FLT\_IS\_IRP\_OPERATION**](https://docs.microsoft.com/previous-versions/ff544654(v=vs.85))

[**FLT\_PARAMETERS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fltkernel/ns-fltkernel-_flt_parameters)

[**FltCreateFile**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fltkernel/nf-fltkernel-fltcreatefile)

[**IRP\_MJ\_CREATE**](irp-mj-create.md)

 

 






