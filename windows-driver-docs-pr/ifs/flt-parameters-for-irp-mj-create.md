---
title: IRP_MJ_CREATE 共用体の FLT_PARAMETERS
description: 次の共用体コンポーネントは、FLT\_IO\_パラメーター\_のブロック構造体で、操作のブロック構造が IRP\_MJ\_CREATE になっている場合に使用されます。
ms.assetid: aa223d51-7d13-4244-bad5-db14f1fb0d2c
keywords:
- IRP_MJ_CREATE union インストール可能ファイルシステムドライバーの FLT_PARAMETERS
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
ms.openlocfilehash: 278dab8a1626c3f8c40d5795679a02de8cc36f53
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72841388"
---
# <a name="flt_parameters-for-irp_mj_create-union"></a>IRP\_MJ の FLT\_パラメーター\_union の作成


次の共用体コンポーネントは、 [**FLT\_IO\_パラメーター\_のブロック**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/ns-fltkernel-_flt_io_parameter_block)構造体**で、操作**のブロック構造が[**IRP\_MJ\_CREATE**](irp-mj-create.md)になっている場合に使用されます。

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

<a name="members"></a>Members
-------

**生成**  
次のメンバーを含む構造体。

**SecurityContext**  
SecurityContext-&gt;AccessState

オブジェクトのサブジェクトコンテキスト、アクセスの種類、およびその他の必要なアクセスの種類を含む、[**アクセス\_状態**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_access_state)構造体へのポインター。

SecurityContext-&gt;DesiredAccess

ファイルに要求されたアクセス権を指定する[ **\_マスク**](https://docs.microsoft.com/windows-hardware/drivers/kernel/access-mask)構造体にアクセスします。 詳細については、 [**Fltcreatefile**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltcreatefile)の*DesiredAccess*パラメーターを参照してください。

**[オプション]**  
ファイルを作成または開くときに適用するオプション、およびファイルが既に存在する場合に実行するアクションを指定するフラグのビットマスク。 このメンバーの下位24ビットは、 [**Fltcreatefile**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltcreatefile)の*createoptions*パラメーターに対応しています。 上位8ビットは**Fltcreatefile**の*CreateDisposition*パラメーターに対応します。

**FileAttributes**  
ファイルを作成または開くときに適用される属性のビットマスク。 詳細については、 [**Fltcreatefile**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltcreatefile)の*fileattributes*パラメーターを参照してください。

**アクセスの許可**  
ファイルに要求された共有アクセス権のビットマスク。 このパラメーターがゼロの場合は、排他アクセスが要求されます。 詳細については、 [**Fltcreatefile**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltcreatefile)の "/"*アクセス*パラメーターを参照してください。

**EaLength**  
**EaBuffer**メンバーが指すバッファーの長さ (バイト単位)。 詳細については、 [**Fltcreatefile**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltcreatefile)の*EaLength*パラメーターを参照してください。

**EaBuffer**  
ファイルに適用される拡張属性 (EA) 情報を格納する、呼び出し元が指定した[**ファイル\_完全\_ea\_情報**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_file_full_ea_information)構造化バッファーを指すポインター。 詳細については、 [**Fltcreatefile**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltcreatefile)の*EaBuffer*パラメーターを参照してください。

**AllocationSize**  
必要に応じて、ファイルの初期割り当てサイズをバイト単位で指定します。 0以外の値は、ファイルが作成、上書き、または置き換えられない限り、無効です。 詳細については、 [**Fltcreatefile**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltcreatefile)の割り当て*サイズ*パラメーターを参照してください。

<a name="remarks"></a>注釈
-------

[**IRP\_MJ\_作成**](irp-mj-create.md)操作の[**FLT\_PARAMETERS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/ns-fltkernel-_flt_parameters)構造体は、コールバックデータ ([**FLT\_callback\_data**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/ns-fltkernel-_flt_callback_data)) 構造体によって表されます。 これは、 [**FLT\_IO\_パラメーター\_ブロック**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/ns-fltkernel-_flt_io_parameter_block)構造体に含まれています。

IRP\_MJ\_CREATE は、IRP ベースの操作です。

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


[**アクセス\_マスク**](https://docs.microsoft.com/windows-hardware/drivers/kernel/access-mask)

[ **\_の状態へのアクセス**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_access_state)

[**ファイル\_EA\_の完全\_情報**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_file_full_ea_information)

[**FLT\_コールバック\_データ**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/ns-fltkernel-_flt_callback_data)

[**FLT\_IO\_パラメーター\_ブロック**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/ns-fltkernel-_flt_io_parameter_block)

[**FLT\_は\_高速な操作\_** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/index)

[**FLT\_は\_FS\_フィルターの\_操作です。** ](https://docs.microsoft.com/previous-versions/ff544648(v=vs.85))

[**FLT\_は\_IRP\_操作です**](https://docs.microsoft.com/previous-versions/ff544654(v=vs.85))

[**FLT\_パラメーター**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/ns-fltkernel-_flt_parameters)

[**FltCreateFile**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltcreatefile)

[**IRP\_MJ\_作成**](irp-mj-create.md)

 

 






