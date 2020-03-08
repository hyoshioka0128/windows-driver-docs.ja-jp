---
title: デュアル\_OPLOCK\_キー\_ECP\_コンテキスト構造
description: デュアル\_OPLOCK\_キー\_ECP\_コンテキスト構造には、デュアル OPLOCK キーの余分な create パラメーターコンテキストが含まれています。 ターゲットファイルオブジェクトと親ファイルオブジェクトの両方の oplock キーは、この構造体で設定できます。
ms.assetid: 7E337D2F-7292-4D18-B750-8361A83C8B1F
keywords:
- DUAL_OPLOCK_KEY_ECP_CONTEXT 構造のインストール可能なファイルシステムドライバー
- PDUAL_OPLOCK_KEY_ECP_CONTEXT 構造体ポインターのインストール可能なファイルシステムドライバー
topic_type:
- apiref
api_name:
- DUAL_OPLOCK_KEY_ECP_CONTEXT
api_location:
- ntifs.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1da2125d4bf4212d56095f16f7088613236d67db
ms.sourcegitcommit: 8c898615009705db7633649a51bef27a25d72b26
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/07/2020
ms.locfileid: "78910428"
---
# <a name="dual_oplock_key_ecp_context-structure"></a>デュアル\_OPLOCK\_キー\_ECP\_コンテキスト構造


**デュアル\_oplock\_キー\_ECP\_コンテキスト**構造には、デュアル OPLOCK キーの余分な create パラメーターコンテキストが含まれています。 ターゲットファイルオブジェクトと親ファイルオブジェクトの両方の oplock キーは、この構造体で設定できます。

<a name="syntax"></a>構文
------

```ManagedCPlusPlus
typedef struct _DUAL_OPLOCK_KEY_ECP_CONTEXT {
  GUID    ParentOplockKey;
  GUID    TargetOplockKey;
  BOOLEAN ParentOplockKeySet;
  BOOLEAN TargetOplockKeySet;
} DUAL_OPLOCK_KEY_ECP_CONTEXT, *PDUAL_OPLOCK_KEY_ECP_CONTEXT;
```

<a name="members"></a>Members
-------

**ParentOplockKey**  
親 oplock キー値を表す**GUID** 。

**TargetOplockKey**  
ターゲット oplock キー値を表す**GUID** 。

**ParentOplockKeySet**  
**ParentOplockKey**に親の oplock キーの有効な GUID が含まれている場合は TRUE に設定します。

**TargetOplockKeySet**  
**TargetOplockKey**にターゲットの oplock キーの有効な GUID が含まれている場合は TRUE に設定します。

<a name="remarks"></a>コメント
-------

**デュアル\_OPLOCK\_キー\_ECP\_コンテキスト**構造は、ファイルとディレクトリに対する oplock 要求を許可するためのデュアル OPLOCK キーを提供します。 [**OPLOCK\_キー\_ecp\_コンテキスト**](oplock-key-ecp-context.md)構造、**デュアル\_OPLOCK\_キー\_ECP\_コンテキスト**は、追加のパラメーターリスト ([**ecp\_リスト**](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff540148(v=vs.85))) で設定され、後で[**IRP\_MJ**](irp-mj-create.md)の処理中にファイルオブジェクトに関連付けられます。これは、ファイルシステムまたはファイルシステムフィルタードライバーによって作成されます。\_

[**FsRtlAllocateExtraCreateParameter**](https://msdn.microsoft.com/library/windows/hardware/ff545609)、 [**FsRtlInitializeExtraCreateParameter**](https://msdn.microsoft.com/library/windows/hardware/ff546113)、 [**FltRemoveExtraCreateParameter**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltremoveextracreateparameter)などのサポートルーチンを呼び出すときには、値**GUID\_ECP\_2\_OPLOCK\_キー**が使用されます。

<a name="requirements"></a>要件
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p>バージョン</p></td>
<td align="left"><p>この構造体は、Windows 8 以降で使用できます。</p></td>
</tr>
<tr class="even">
<td align="left"><p>ヘッダー</p></td>
<td align="left">Ntifs (Ntifs を含む)</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>参照


[**ECP\_一覧**](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff540148(v=vs.85))

[ **\_コンテキストを作成\_IO\_ドライバー**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddk/ns-ntddk-_io_driver_create_context)

[**IoCreateFileEx**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddk/nf-ntddk-iocreatefileex)

[**IRP\_MJ\_作成**](irp-mj-create.md)

[ **\_キー\_ECP\_コンテキストの OPLOCK**](oplock-key-ecp-context.md)


 

 






