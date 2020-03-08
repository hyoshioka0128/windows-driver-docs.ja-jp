---
title: OPLOCK_KEY_ECP_CONTEXT 構造体
description: OPLOCK_KEY_ECP_CONTEXT 構造体は、OPLOCK キーをファイルにアタッチするために使用されます。
ms.assetid: 029dd105-162a-4674-a3d5-b54a91fa4be2
keywords:
- OPLOCK_KEY_ECP_CONTEXT 構造のインストール可能なファイルシステムドライバー
- POPLOCK_KEY_ECP_CONTEXT 構造体ポインターのインストール可能なファイルシステムドライバー
topic_type:
- apiref
api_name:
- OPLOCK_KEY_ECP_CONTEXT
api_location:
- ntifs.h
api_type:
- HeaderDef
ms.date: 11/08/2019
ms.localizationpriority: medium
ms.openlocfilehash: b55abb049cb8f4a28e73acc8aee2b88303d16812
ms.sourcegitcommit: 8c898615009705db7633649a51bef27a25d72b26
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/07/2020
ms.locfileid: "78910475"
---
# <a name="oplock_key_ecp_context-structure"></a>OPLOCK_KEY_ECP_CONTEXT 構造体

OPLOCK_KEY_ECP_CONTEXT 構造体は、OPLOCK キーをファイルにアタッチするために使用されます。 この構造は、Windows 8 以降のバージョンでは廃止されています。フィルターでは、代わりに[DUAL_OP_LOCK_KEY_ECP_CONTEXT](https://docs.microsoft.com/windows-hardware/drivers/ifs/dual-oplock-key-ecp-context)を使用する必要があります。

## <a name="syntax"></a>構文

```ManagedCPlusPlus
typedef struct _OPLOCK_KEY_ECP_CONTEXT {
  GUID  OplockKey;
  ULONG Reserved;
} OPLOCK_KEY_ECP_CONTEXT, *POPLOCK_KEY_ECP_CONTEXT;
```

## <a name="members"></a>Members

**OplockKey**  
Oplock キーの GUID。 この GUID は、異なるハンドル間で共有され、同じクライアントキャッシュに属するものとして識別されます。 2つのハンドルが同じ oplock キーを共有する場合、1つのハンドルに対して実行される要求は、もう一方のハンドルの未解決の oplock を解除しません。

**確保**  
予約済み。 を0に設定する必要があります。

## <a name="remarks"></a>コメント

ファイルの作成時に ECPs を使用して追加情報をファイルに関連付ける方法については、「 [IRP_MJ_CREATE 操作での追加の作成パラメーターの使用](https://docs.microsoft.com/windows-hardware/drivers/ifs/using-extra-create-parameters-with-an-irp-mj-create-operation)」を参照してください。

ミニフィルターでは、前から ECP が出てきたときに、OPLOCK_KEY_ECP_CONTEXT 構造の内容を変更することはできません。 このキーを使用して、oplock キー ECP に関する情報のみを取得する必要があります。 この問題の詳細については、「[システム定義の ECPs](https://docs.microsoft.com/windows-hardware/drivers/ifs/system-defined-ecps)」を参照してください。

Oplock キーを使用すると、アプリケーション独自の oplock を中断することなく、同じストリームに対して複数のハンドルを開くことができます。 Oplock が解除されるのは、アプリケーションが共有違反 (STATUS_SHARING_VIOLATION) を受信した後です。

Oplock は、ストリームが開かれるときにストリームハンドルで許可されます。 このようなストリームハンドルは、oplock キーに関連付けることができます。 呼び出し元は、 [**IoCreateFileEx**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddk/nf-ntddk-iocreatefileex)ルーチンに oplock キーを明示的に指定して、ストリームハンドルを作成できます。 呼び出し元がハンドルを作成するときに、呼び出し元が oplock キーを明示的に指定していない場合、オペレーティングシステムはハンドルのキーが他のハンドルの他のキーと異なるようにハンドルに関連付けられた一意の oplock キーとしてハンドルを扱います。 Oplock が許可されたハンドル以外のハンドルでファイル操作を受信し、oplock のハンドルに関連付けられている oplock キーが操作のハンドルに関連付けられているキーと異なる場合、その操作は、現在 oplock が許可されている場合、oplock は解除されます。 Oplock は、互換性のない操作を実行しているプロセスまたはスレッドの場合でも中断されます。 たとえば、排他的 oplock が付与されているストリームをプロセスが開き、同じプロセスが別の (またはない) oplock キーを使用して同じストリームを再び開く場合、排他的な oplock は直ちに解除されます。

Oplock キーは、ハンドルが作成されるときにハンドルに関連付けられます。 Oplock が付与されていない場合でも、ハンドルを oplock キーに関連付けることができます。

Oplock キーと oplock キーの詳細については、「 [Oplock セマンティクスの概要](https://docs.microsoft.com/windows-hardware/drivers/ifs/oplock-overview)」を参照してください。

## <a name="requirements"></a>要件

|   |   |
| - | - |
| バージョン | この構造体は Windows 7 以降で使用でき、Windows 8 以降のバージョンでは廃止されています。 |
| ヘッダー | *Ntifs* (Ntifs または Ntddk を含む) |

## <a name="see-also"></a>参照

[DUAL_OP_LOCK_KEY_ECP_CONTEXT](https://docs.microsoft.com/windows-hardware/drivers/ifs/dual-oplock-key-ecp-context)

[**IoCreateFileEx**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddk/nf-ntddk-iocreatefileex)
