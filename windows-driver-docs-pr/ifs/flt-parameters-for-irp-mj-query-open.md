---
title: FLT_PARAMETERS IRP_MJ_QUERY_OPEN 共用体
description: 次の共用体のコンポーネントは、操作の FLT_IO_PARAMETER_BLOCK 構造の MajorFunction フィールドは IRP_MJ_QUERY_OPEN ときに使用されます。
ms.assetid: 5B78E1D8-F724-404D-8750-3D52BB9B4910
keywords:
- FLT_PARAMETERS IRP_MJ_QUERY_OPEN 共用体インストール可能なファイル システム ドライバー
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
ms.date: 10/12/2018
ms.localizationpriority: medium
ms.openlocfilehash: 0338b7e5191076f178f827c801f68d589e3d171d
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67365485"
---
# <a name="fltparameters-for-irpmjqueryopen-union"></a>FLT\_IRP_MJ_QUERY_OPEN 共用体のパラメーター


次の共用体のコンポーネントが使用されるときに、 **MajorFunction**のフィールド、 [ **FLT\_IO\_パラメーター\_ブロック**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fltkernel/ns-fltkernel-_flt_io_parameter_block)操作の構造は、IRP_MJ_QUERY_OPEN です。

<a name="syntax"></a>構文
------

```ManagedCPlusPlus
typedef union _FLT_PARAMETERS {
  ...    ;
  struct {
    PIRP                   Irp;
    PVOID                  FileInformation;
    PULONG                 Length;
    FILE_INFORMATION_CLASS FileInformationClass;
  } QueryOpen;
  ...    ;
} FLT_PARAMETERS, *PFLT_PARAMETERS;
```

<a name="members"></a>メンバー
-------

**Irp**  
* この操作に関連付けられた IRP へのポインター。 

**FileInformation**  
* ルーチンは、ファイル オブジェクトに関する要求された情報を書き込みます。 呼び出し元が割り当てたバッファーへのポインター。 *FileInformationClass*メンバーは、呼び出し元が要求する情報の種類を指定します。 

**Length**
*  指し示されるバッファーのバイト単位のサイズを**FileInformation**します。

**FileInformationClass**
* FileInformation が指すバッファーにあるファイルについて返される情報の種類を指定します。 デバイスと中間ドライバーは、次のいずれかで指定できます[ **FILE_INFORMATION_CLASS** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/ne-wdm-_file_information_class)値。 その他の値は、呼び出しを失敗が発生して、PreQueryOpen/PostQueryOpen 呼び出しに渡すことはできません。 

| FILE_INFORMATION_CLASS 値 | 返される情報の種類 |
| --- | --- |
| FileStatInformation | A [ **FILE_STAT_INFORMATION** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/ns-ntifs-_file_stat_information)構造体。 この構造体には、アクセス マスクが含まれています。 アクセス マスクの詳細については、次を参照してください。 [ACCESS_MASK](https://docs.microsoft.com/windows-hardware/drivers/kernel/access-mask)します。 
| FileStatLxInformation | A [ **FILE_STAT_LX_INFORMATION** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/ns-ntifs-_file_stat_lx_information)構造体。 この構造体には、アクセス マスクが含まれています。 アクセス マスクの詳細については、次を参照してください。 [ACCESS_MASK](https://docs.microsoft.com/windows-hardware/drivers/kernel/access-mask)します。 
| FileCaseSensitiveInformation | A [FILE_CASE_SENSITIVE_INFORMATION](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/ns-ntifs-_file_stat_information)構造体。 |

## <a name="remarks"></a>コメント


[ **FLT\_パラメーター** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fltkernel/ns-fltkernel-_flt_parameters) IRP_MJ_QUERY_OPEN 操作のための構造体のパラメーターを格納する、 **QueryOpen**コールバックによって表される操作データ ([**FLT\_コールバック\_データ**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fltkernel/ns-fltkernel-_flt_callback_data)) 構造体。 FLT に含まれている\_IO\_パラメーター\_ブロック構造体。

IRP_MJ_QUERY_OPEN は、ファイル システム (FSFilter) コールバック操作です。

FSFilter コールバック操作の詳細については、参照のエントリを参照してください。 [ **FsRtlRegisterFileSystemFilterCallbacks**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/nf-ntifs-fsrtlregisterfilesystemfiltercallbacks)します。

## <a name="requirements"></a>必要条件


<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p>バージョン</p></td>
<td align="left"><p>Windows 10、バージョン 1703 以降のバージョンの Windows オペレーティング システムで使用できます。</p></td>
</tr>
<tr class="even">
<td align="left"><p>Header</p></td>
<td align="left">Fltkernel.h (Fltkernel.h を含む)</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>関連項目


[**FLT\_コールバック\_データ**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fltkernel/ns-fltkernel-_flt_callback_data)

[**FLT\_IO\_PARAMETER\_BLOCK**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fltkernel/ns-fltkernel-_flt_io_parameter_block)

[**FLT\_IS\_FASTIO\_OPERATION**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/index)

[**FLT\_IS\_FS\_FILTER\_OPERATION**](https://docs.microsoft.com/previous-versions/ff544648(v=vs.85))

[**FLT\_IS\_IRP\_OPERATION**](https://docs.microsoft.com/previous-versions/ff544654(v=vs.85))

[**FLT\_PARAMETERS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fltkernel/ns-fltkernel-_flt_parameters)

[**FsRtlRegisterFileSystemFilterCallbacks**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/nf-ntifs-fsrtlregisterfilesystemfiltercallbacks)
