---
title: OPLOCK\_キー\_ECP\_CONTEXT 構造体
description: Oplock\_キー\_ECP\_コンテキスト構造を使用して、oplock キーをファイルにアタッチします。
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
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: ad9d4dc68f3dadaf050230560cda08bea52d60b9
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72841046"
---
# <a name="oplock_key_ecp_context-structure"></a>OPLOCK\_キー\_ECP\_CONTEXT 構造体


Oplock\_キー\_ECP\_コンテキスト構造を使用して、oplock キーをファイルにアタッチします。

<a name="syntax"></a>構文
------

```ManagedCPlusPlus
typedef struct _OPLOCK_KEY_ECP_CONTEXT {
  GUID  OplockKey;
  ULONG Reserved;
} OPLOCK_KEY_ECP_CONTEXT, *POPLOCK_KEY_ECP_CONTEXT;
```

<a name="members"></a>Members
-------

**OplockKey**  
Oplock キーの GUID。 この GUID は、異なるハンドル間で共有され、同じクライアントキャッシュに属するものとして識別されます。 2つのハンドルが同じ oplock キーを共有する場合、1つのハンドルに対して実行される要求は、もう一方のハンドルの未解決の oplock を解除しません。

**確保**  
予約済み。 を0に設定する必要があります。

<a name="remarks"></a>注釈
-------

ファイルの作成時に ECPs を使用して追加情報をファイルに関連付ける方法の詳細については、「 [IRP\_MJ\_Create 操作で追加の作成パラメーターを使用](https://docs.microsoft.com/windows-hardware/drivers/ifs/using-extra-create-parameters-with-an-irp-mj-create-operation)する」を参照してください。

OPLOCK\_キー\_ECP\_コンテキスト構造は読み取り専用です。 このキーを使用して、oplock キー ECP に関する情報のみを取得する必要があります。 この問題の詳細については、「[システム定義の ECPs](https://docs.microsoft.com/windows-hardware/drivers/ifs/system-defined-ecps)」を参照してください。

Oplock キーを使用すると、アプリケーション独自の oplock を中断することなく、同じストリームに対して複数のハンドルを開くことができます。 Oplock の解除が発生するのは、アプリケーションが共有違反 (状態\_共有\_違反) を受け取った後です。

Oplock は、ストリームが開かれるときにストリームハンドルで許可されます。 このようなストリームハンドルは、oplock キーに関連付けることができます。 呼び出し元は、 [**IoCreateFileEx**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddk/nf-ntddk-iocreatefileex)ルーチンに oplock キーを明示的に指定して、ストリームハンドルを作成できます。 呼び出し元がハンドルを作成するときに、呼び出し元が oplock キーを明示的に指定していない場合、オペレーティングシステムはハンドルのキーが他のハンドルの他のキーと異なるようにハンドルに関連付けられた一意の oplock キーとしてハンドルを扱います。 Oplock が許可されたハンドル以外のハンドルでファイル操作を受信し、oplock のハンドルに関連付けられている oplock キーが操作のハンドルに関連付けられているキーと異なる場合、その操作は、現在 oplock が許可されている場合、oplock は解除されます。 Oplock は、互換性のない操作を実行しているプロセスまたはスレッドの場合でも中断されます。 たとえば、排他的 oplock が付与されているストリームをプロセスが開き、同じプロセスが別の (またはない) oplock キーを使用して同じストリームを再び開く場合、排他的な oplock は直ちに解除されます。

Oplock キーは、ハンドルが作成されるときにハンドルに関連付けられます。 Oplock が付与されていない場合でも、ハンドルを oplock キーに関連付けることができます。

Oplock キーと oplock キーの詳細については、「 [Oplock セマンティクスの概要](https://docs.microsoft.com/windows-hardware/drivers/ifs/overview)」を参照してください。

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
<td align="left"><p>この構造体は、Windows 7 以降で使用できます。</p></td>
</tr>
<tr class="even">
<td align="left"><p>Header</p></td>
<td align="left">Ntifs (Ntifs または Ntddk を含む)</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>関連項目


[**IoCreateFileEx**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddk/nf-ntddk-iocreatefileex)

 

 






