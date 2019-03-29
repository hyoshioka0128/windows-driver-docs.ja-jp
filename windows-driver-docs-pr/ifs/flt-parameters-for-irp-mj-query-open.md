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
ms.openlocfilehash: a60d847786a5d3a90e4852dbb2b690a4b11a4ed0
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56571876"
---
# <a name="fltparameters-for-irpmjqueryopen-union"></a>FLT\_IRP_MJ_QUERY_OPEN 共用体のパラメーター


次の共用体のコンポーネントが使用されるときに、 **MajorFunction**のフィールド、 [ **FLT\_IO\_パラメーター\_ブロック**](https://msdn.microsoft.com/library/windows/hardware/ff544638)操作の構造は、IRP_MJ_QUERY_OPEN です。

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


[ **FLT\_パラメーター** ](https://msdn.microsoft.com/library/windows/hardware/ff544673) IRP_MJ_QUERY_OPEN 操作のための構造体のパラメーターを格納する、 **QueryOpen**コールバックによって表される操作データ ([**FLT\_コールバック\_データ**](https://msdn.microsoft.com/library/windows/hardware/ff544620)) 構造体。 FLT に含まれている\_IO\_パラメーター\_ブロック構造体。

IRP_MJ_QUERY_OPEN は、ファイル システム (FSFilter) コールバック操作です。

FSFilter コールバック操作の詳細については、参照のエントリを参照してください。 [ **FsRtlRegisterFileSystemFilterCallbacks**](https://msdn.microsoft.com/library/windows/hardware/ff547172)します。

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


[**FLT\_コールバック\_データ**](https://msdn.microsoft.com/library/windows/hardware/ff544620)

[**FLT\_IO\_PARAMETER\_BLOCK**](https://msdn.microsoft.com/library/windows/hardware/ff544638)

[**FLT\_IS\_FASTIO\_OPERATION**](https://msdn.microsoft.com/library/windows/hardware/ff544645)

[**FLT\_IS\_FS\_FILTER\_OPERATION**](https://msdn.microsoft.com/library/windows/hardware/ff544648)

[**FLT\_IS\_IRP\_OPERATION**](https://msdn.microsoft.com/library/windows/hardware/ff544654)

[**FLT\_PARAMETERS**](https://msdn.microsoft.com/library/windows/hardware/ff544673)

[**FsRtlRegisterFileSystemFilterCallbacks**](https://msdn.microsoft.com/library/windows/hardware/ff547172)
