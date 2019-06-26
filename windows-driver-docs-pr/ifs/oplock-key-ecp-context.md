---
title: OPLOCK\_キー\_ECP\_CONTEXT 構造体
description: OPLOCK\_キー\_ECP\_コンテキストの構造を使用して、oplock のキーをファイルにアタッチします。
ms.assetid: 029dd105-162a-4674-a3d5-b54a91fa4be2
keywords:
- OPLOCK_KEY_ECP_CONTEXT 構造インストール可能なファイル システム ドライバー
- POPLOCK_KEY_ECP_CONTEXT 構造体ポインター インストール可能なファイル システム ドライバー
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
ms.openlocfilehash: 66e9a5a51f8e9688822d47f04e14195da4533a81
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67386067"
---
# <a name="oplockkeyecpcontext-structure"></a>OPLOCK\_キー\_ECP\_CONTEXT 構造体


OPLOCK\_キー\_ECP\_コンテキストの構造を使用して、oplock のキーをファイルにアタッチします。

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
Oplock キーの GUID です。 この GUID は、別のハンドルの間で共有され、同じクライアント キャッシュに属していることを示します。 2 つのハンドルは、同じ oplock キーを共有するときに 1 つのハンドルで実行される要求では、ハンドルが他には、未処理の oplock が壊れない。

**Reserved**  
予約済み。 0 に設定する必要があります。

<a name="remarks"></a>注釈
-------

ECPs を使用して、ファイルが作成されると、ファイルと追加情報を関連付ける方法については、次を参照してください。 [IRP の余分な作成のパラメーターを使用して\_MJ\_作成操作](https://docs.microsoft.com/windows-hardware/drivers/ifs/using-extra-create-parameters-with-an-irp-mj-create-operation)します。

OPLOCK\_キー\_ECP\_CONTEXT 構造は読み取り専用です。 これを使用して、oplock キー ECP をのみに関する情報を取得する必要があります。 この問題の詳細については、次を参照してください。[ベンダー ECPs](https://docs.microsoft.com/windows-hardware/drivers/ifs/system-defined-ecps)します。

Oplock キーにより、アプリケーションの oplock を損なうことがなく、同じストリームに複数のハンドルを開くためのアプリケーションです。 アプリケーション受信共有違反が発生した後にのみ、oplock が発生した (ステータス\_共有\_違反)。

ストリームを開いたときに、ストリームのハンドルでの各 Oplock が付与されます。 このようなストリームのハンドル oplock キーで関連付けることができます。 呼び出し元は、oplock のキーを明示的に指定できます、 [ **IoCreateFileEx** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddk/nf-ntddk-iocreatefileex)ルーチンをストリームのハンドルを作成します。 呼び出し元は、oplock のキーが、呼び出し元が、ハンドルを作成するときに明示的に指定していない、オペレーティング システムはハンドルのキーは、他のいずれかのハンドルの他の任意のキーと異なるように、ハンドルに関連付けられた一意の oplock のキーを持つものとしてハンドルを扱います。 Oplock が許可されたもの以外のハンドルでファイルの操作を受信した、操作のハンドルに関連付けられているキーからとは異なる oplock のハンドルに関連付けられている oplock キーとその操作と互換性がありません、現在 oplock を与え、し、その oplock は解除されます。 プロセスまたは互換性のない操作を実行するスレッドが同じである場合でも、oplock が解除されます。 たとえば、プロセスが排他的 oplock が付与されますストリームを開き、同じ処理し、同じストリームがもう一度開きます、異なる (またはなし) を使用して、oplock キー排他 oplock が壊れているすぐにします。

ハンドルが作成されたときに、Oplock のキーがハンドルに関連付けられます。 各 oplock が付与されていない場合でも、oplock のキーを持つハンドルを関連付けることができます。

各 oplock と oplock のキーの詳細については、次を参照してください。 [Oplock セマンティクス概要](https://docs.microsoft.com/windows-hardware/drivers/ifs/overview)します。

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
<td align="left"><p>この構造体は、Windows 7 以降から使用できます。</p></td>
</tr>
<tr class="even">
<td align="left"><p>Header</p></td>
<td align="left">Ntifs.h (Ntifs.h または Ntddk.h を含む)</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>関連項目


[**IoCreateFileEx**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddk/nf-ntddk-iocreatefileex)

 

 






