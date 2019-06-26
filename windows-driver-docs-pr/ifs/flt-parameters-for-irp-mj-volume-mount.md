---
title: FLT_PARAMETERS IRP_MJ_VOLUME_MOUNT 共用体
description: 次の共用体のコンポーネントが使用されるときに、FLT の MajorFunction フィールド\_IO\_パラメーター\_操作のブロック構造は IRP\_MJ\_ボリューム\_マウントします。
ms.assetid: 3fcc20da-b985-4d08-a0f7-9d95ddfb79d8
keywords:
- FLT_PARAMETERS IRP_MJ_VOLUME_MOUNT 共用体インストール可能なファイル システム ドライバー
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
ms.openlocfilehash: c6b45626d489b2014a41f887189f68a347141a44
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67384257"
---
# <a name="fltparameters-for-irpmjvolumemount-union"></a>FLT\_IRP のパラメーター\_MJ\_ボリューム\_マウント共用体


次の共用体のコンポーネントが使用されるときに、 **MajorFunction**のフィールド、 [ **FLT\_IO\_パラメーター\_ブロック**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fltkernel/ns-fltkernel-_flt_io_parameter_block)操作は IRP を構造体\_MJ\_ボリューム\_マウントします。

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

**DeviceType**  
新たにマウントされたボリュームのファイル システムのボリュームのデバイス オブジェクトのデバイスの種類。 次のいずれかです。

ファイル\_デバイス\_CD\_ROM\_ファイル\_システム

ファイル\_デバイス\_ディスク\_ファイル\_システム

ファイル\_デバイス\_ネットワーク\_ファイル\_システム

<a name="remarks"></a>注釈
-------

[ **FLT\_パラメーター** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fltkernel/ns-fltkernel-_flt_parameters) IRP の構造\_MJ\_ボリューム\_マウント操作には、ボリューム マウント操作のパラメーターが含まれています。コールバック データによって表される ([**FLT\_コールバック\_データ**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fltkernel/ns-fltkernel-_flt_callback_data)) 構造体。 FLT に含まれている\_IO\_パラメーター\_ブロック構造体。

IRP\_MJ\_ボリューム\_マウントが高速な I/O 操作。

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


[**FLT\_コールバック\_データ**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fltkernel/ns-fltkernel-_flt_callback_data)

[**FLT\_IO\_PARAMETER\_BLOCK**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fltkernel/ns-fltkernel-_flt_io_parameter_block)

[**FLT\_IS\_FASTIO\_OPERATION**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/index)

[**FLT\_IS\_FS\_FILTER\_OPERATION**](https://docs.microsoft.com/previous-versions/ff544648(v=vs.85))

[**FLT\_IS\_IRP\_OPERATION**](https://docs.microsoft.com/previous-versions/ff544654(v=vs.85))

[**FLT\_PARAMETERS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fltkernel/ns-fltkernel-_flt_parameters)

[**IRP\_MJ\_ファイル\_システム\_コントロール**](irp-mj-file-system-control.md)

 

 






