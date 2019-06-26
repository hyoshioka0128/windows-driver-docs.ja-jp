---
title: デュアル\_OPLOCK\_キー\_ECP\_CONTEXT 構造体
description: デュアル\_OPLOCK\_キー\_ECP\_CONTEXT 構造体には、余分なが含まれています。 デュアル oplock キーのパラメーターのコンテキストを作成します。 この構造体では、ターゲットと親のファイル オブジェクトの両方の Oplock のキーを設定できます。
ms.assetid: 7E337D2F-7292-4D18-B750-8361A83C8B1F
keywords:
- DUAL_OPLOCK_KEY_ECP_CONTEXT 構造インストール可能なファイル システム ドライバー
- PDUAL_OPLOCK_KEY_ECP_CONTEXT 構造体ポインター インストール可能なファイル システム ドライバー
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
ms.openlocfilehash: ad5182048de61499d8e8bb36fe41a87af6761fb1
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67386093"
---
# <a name="dualoplockkeyecpcontext-structure"></a>デュアル\_OPLOCK\_キー\_ECP\_CONTEXT 構造体


**デュアル\_OPLOCK\_キー\_ECP\_コンテキスト**構造に含まれる追加のパラメーターのコンテキストをデュアル oplock キーを作成します。 この構造体では、ターゲットと親のファイル オブジェクトの両方の Oplock のキーを設定できます。

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
A **GUID** oplock の親のキー値を表します。

**TargetOplockKey**  
A **GUID**ターゲット oplock のキー値を表します。

**ParentOplockKeySet**  
場合に TRUE に設定**ParentOplockKey**親の oplock のキーの有効な GUID が含まれています。

**TargetOplockKeySet**  
場合に TRUE に設定**TargetOplockKey** oplock の対象のキーの有効な GUID が含まれています。

<a name="remarks"></a>注釈
-------

**デュアル\_OPLOCK\_キー\_ECP\_コンテキスト**構造体には、ファイルとディレクトリの oplock の要求を許可するデュアル oplock キーが提供されます。 ように、 [ **OPLOCK\_キー\_ECP\_コンテキスト**](oplock-key-ecp-context.md)構造、**デュアル\_OPLOCK\_キー\_ECP\_コンテキスト**余分な設定は、パラメーター リストの作成 ([**ECP\_一覧**](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff540148(v=vs.85)))の処理中に後で、ファイルオブジェクトに関連付けられていると[**IRP\_MJ\_作成**](irp-mj-create.md)によってファイル システムまたはファイル システム フィルター ドライバー。

値**GUID\_ECP\_デュアル\_OPLOCK\_キー**などサポート ルーチンを呼び出すときに使用が[ **FsRtlAllocateExtraCreateParameter**](https://msdn.microsoft.com/library/windows/hardware/ff545609)、 [ **FsRtlInitializeExtraCreateParameter**](https://msdn.microsoft.com/library/windows/hardware/ff546113)、または[ **FltRemoveExtraCreateParameter**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fltkernel/nf-fltkernel-fltremoveextracreateparameter)します。

<a name="requirements"></a>必要条件
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p>バージョン</p></td>
<td align="left"><p>この構造体では、Windows 8 以降で使用できます。</p></td>
</tr>
<tr class="even">
<td align="left"><p>Header</p></td>
<td align="left">Ntifs.h (Ntifs.h を含む)</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>関連項目


[**ECP\_一覧**](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff540148(v=vs.85))

[**IO\_DRIVER\_CREATE\_CONTEXT**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddk/ns-ntddk-_io_driver_create_context)

[**IoCreateFileEx**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddk/nf-ntddk-iocreatefileex)

[**IRP\_MJ\_CREATE**](irp-mj-create.md)

[**OPLOCK\_KEY\_ECP\_CONTEXT**](oplock-key-ecp-context.md)

[Oplock のセマンティクス](https://docs.microsoft.com/windows-hardware/drivers/ifs/oplock-semantics)

 

 






