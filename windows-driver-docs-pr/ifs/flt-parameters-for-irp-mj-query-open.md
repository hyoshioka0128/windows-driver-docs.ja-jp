---
title: IRP_MJ_QUERY_OPEN 共用体の FLT_PARAMETERS
description: 操作の FLT_IO_PARAMETER_BLOCK 構造体の MajorFunction フィールドが IRP_MJ_QUERY_OPEN の場合、次の共用体コンポーネントが使用されます。
ms.assetid: 5B78E1D8-F724-404D-8750-3D52BB9B4910
keywords:
- IRP_MJ_QUERY_OPEN union インストール可能ファイルシステムドライバーの FLT_PARAMETERS
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
ms.date: 10/12/2018
ms.localizationpriority: medium
ms.openlocfilehash: d05c3efd152226ba6158ffa4318dc5a336e41e0e
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72841363"
---
# <a name="flt_parameters-for-irp_mj_query_open-union"></a>IRP_MJ_QUERY_OPEN union の FLT\_パラメーター


操作の[**FLT\_IO\_パラメーター\_BLOCK**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/ns-fltkernel-_flt_io_parameter_block)構造体の**MAJORFUNCTION**フィールドが IRP_MJ_QUERY_OPEN の場合には、次の共用体コンポーネントが使用されます。

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

<a name="members"></a>Members
-------

**Irp**  
* この操作に関連付けられている IRP へのポインター。 

**FileInformation**  
* ルーチンがファイルオブジェクトに関する要求された情報を書き込む、呼び出し元が割り当てたバッファーへのポインター。 *Fileinformationclass*メンバーは、呼び出し元が要求する情報の種類を指定します。 

**長さ**
*  **Fileinformation**が指すバッファーのサイズ (バイト単位)。

**FileInformationClass**
* FileInformation が指すバッファー内のファイルについて返される情報の種類を指定します。 デバイスと中間ドライバーでは、次のいずれかの[**FILE_INFORMATION_CLASS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ne-wdm-_file_information_class)値を指定できます。 その他の値を指定すると、呼び出しは失敗し、PreQueryOpen/PostQueryOpen 呼び出しに渡すことはできません。 

| FILE_INFORMATION_CLASS 値 | 返される情報の種類 |
| --- | --- |
| FileStatInformation | [**FILE_STAT_INFORMATION**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/ns-ntifs-_file_stat_information)構造体。 この構造体には、アクセスマスクが含まれています。 アクセスマスクの詳細については、「 [ACCESS_MASK](https://docs.microsoft.com/windows-hardware/drivers/kernel/access-mask)」を参照してください。 
| FileStatLxInformation | [**FILE_STAT_LX_INFORMATION**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/ns-ntifs-_file_stat_lx_information)構造体。 この構造体には、アクセスマスクが含まれています。 アクセスマスクの詳細については、「 [ACCESS_MASK](https://docs.microsoft.com/windows-hardware/drivers/kernel/access-mask)」を参照してください。 
| FileCaseSensitiveInformation | [FILE_CASE_SENSITIVE_INFORMATION](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/ns-ntifs-_file_stat_information)構造体。 |

## <a name="remarks"></a>注釈


IRP_MJ_QUERY_OPEN 操作の[**FLT\_parameters**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/ns-fltkernel-_flt_parameters)構造体には、コールバックデータ ([**FLT\_callback\_data**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/ns-fltkernel-_flt_callback_data)) 構造体によって表される**queryopen**操作のパラメーターが含まれています。 これは、FLT\_IO\_パラメーター\_ブロック構造体に含まれています。

IRP_MJ_QUERY_OPEN は、ファイルシステム (FSFilter) コールバック操作です。

FSFilter のコールバック操作の詳細については、 [**Fsrtlregisterfilesystemfiltercallbacks**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-fsrtlregisterfilesystemfiltercallbacks)のリファレンスエントリを参照してください。

## <a name="requirements"></a>要件


<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p>バージョン</p></td>
<td align="left"><p>Windows 10 バージョン1703以降のバージョンの Windows オペレーティングシステムで使用できます。</p></td>
</tr>
<tr class="even">
<td align="left"><p>Header</p></td>
<td align="left">Fltkernel .h (Fltkernel. h を含む)</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>関連項目


[**FLT\_コールバック\_データ**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/ns-fltkernel-_flt_callback_data)

[**FLT\_IO\_パラメーター\_ブロック**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/ns-fltkernel-_flt_io_parameter_block)

[**FLT\_は\_高速な操作\_** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/index)

[**FLT\_は\_FS\_フィルターの\_操作です。** ](https://docs.microsoft.com/previous-versions/ff544648(v=vs.85))

[**FLT\_は\_IRP\_操作です**](https://docs.microsoft.com/previous-versions/ff544654(v=vs.85))

[**FLT\_パラメーター**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/ns-fltkernel-_flt_parameters)

[**FsRtlRegisterFileSystemFilterCallbacks バック**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-fsrtlregisterfilesystemfiltercallbacks)
