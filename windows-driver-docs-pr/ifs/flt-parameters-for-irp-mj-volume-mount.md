---
title: IRP_MJ_VOLUME_MOUNT 共用体の FLT_PARAMETERS
description: 次の共用体コンポーネントは、FLT\_IO\_パラメーター\_のブロック構造の MajorFunction フィールドが、操作に対する IRP\_MJ\_ボリューム\_マウントされている場合に使用されます。
ms.assetid: 3fcc20da-b985-4d08-a0f7-9d95ddfb79d8
keywords:
- IRP_MJ_VOLUME_MOUNT union インストール可能ファイルシステムドライバーの FLT_PARAMETERS
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
ms.openlocfilehash: dd5f9da26fd0557af4d0dc7ace12f1ee80d490a3
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72841341"
---
# <a name="flt_parameters-for-irp_mj_volume_mount-union"></a>IRP\_MJ\_ボリュームの FLT\_パラメーター\_マウント共用体


次の共用体コンポーネントは、 [**FLT\_IO\_パラメーター\_のブロック**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/ns-fltkernel-_flt_io_parameter_block)構造の**MajorFunction**フィールドが、操作に対する IRP\_MJ\_ボリューム\_マウントされている場合に使用されます。

<a name="syntax"></a>構文
------

```ManagedCPlusPlus
typedef union _FLT_PARAMETERS {
  ...    ;
  struct {
    ULONG DeviceType;
  } MountVolume;
  ...    ;
} FLT_PARAMETERS, *PFLT_PARAMETERS;
```

<a name="members"></a>Members
-------

**MountVolume**  
次のメンバーを含む構造体。

**(Devicetype**  
新しくマウントされたボリュームのファイルシステムのボリュームデバイスオブジェクトのデバイスの種類。 次のいずれかです。

ファイル\_デバイス\_CD\_ROM\_ファイル\_システム

ファイル\_デバイス\_ディスク\_ファイル\_システム

ファイル\_デバイス\_ネットワーク\_ファイル\_システム

<a name="remarks"></a>注釈
-------

IRP\_MJ\_VOLUME\_のマウント操作の[**FLT\_parameters**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/ns-fltkernel-_flt_parameters)構造体には、コールバックデータ ([**FLT\_callback\_data**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/ns-fltkernel-_flt_callback_data)) 構造によって表されるボリュームマウント操作のパラメーターが含まれています。 これは、FLT\_IO\_パラメーター\_ブロック構造体に含まれています。

IRP\_MJ\_ボリューム\_マウントは高速 i/o 操作です。

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


[**FLT\_コールバック\_データ**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/ns-fltkernel-_flt_callback_data)

[**FLT\_IO\_パラメーター\_ブロック**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/ns-fltkernel-_flt_io_parameter_block)

[**FLT\_は\_高速な操作\_** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/index)

[**FLT\_は\_FS\_フィルターの\_操作です。** ](https://docs.microsoft.com/previous-versions/ff544648(v=vs.85))

[**FLT\_は\_IRP\_操作です**](https://docs.microsoft.com/previous-versions/ff544654(v=vs.85))

[**FLT\_パラメーター**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/ns-fltkernel-_flt_parameters)

[**IRP\_MJ\_ファイル\_システム\_コントロール**](irp-mj-file-system-control.md)

 

 






