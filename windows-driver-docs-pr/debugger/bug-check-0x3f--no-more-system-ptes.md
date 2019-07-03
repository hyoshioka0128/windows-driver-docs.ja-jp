---
title: Bug Check 0x3F NO_MORE_SYSTEM_PTES
description: NO_MORE_SYSTEM_PTES のバグ チェックでは、0x0000003F の値を持ちます。 これは、多くの I/O 操作が実行されるシステムの結果です。
ms.assetid: b8164ec3-87c3-4629-ab70-6addbf368b76
keywords:
- Bug Check 0x3F NO_MORE_SYSTEM_PTES
- NO_MORE_SYSTEM_PTES
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- NO_MORE_SYSTEM_PTES
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: b1f59518adf71538f46351cecb1dc3b85d31aaef
ms.sourcegitcommit: d03b44343cd32b3653d0471afcdd3d35cb800c0d
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/02/2019
ms.locfileid: "67519470"
---
# <a name="bug-check-0x3f-nomoresystemptes"></a>バグ チェック 0x3F:いいえ\_詳細\_システム\_PTE


いいえ、\_詳細\_システム\_PTE バグ チェックが 0x0000003F の値を持ちます。 これは、多くの I/O 操作が実行されるシステムの結果です。 これは、断片化されたシステム ページ テーブル エントリ (PTE) にもたらされました。

> [!IMPORTANT]
> このトピックはプログラマーを対象としています。 コンピューターを使用しているときに、エラー コードがブルー スクリーンが受信した顧客の場合を参照してください。[トラブルシューティング ブルー スクリーン エラー](https://www.windows.com/stopcode)します。


## <a name="nomoresystemptes-parameters"></a>いいえ\_詳細\_システム\_PTE パラメーター


<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">パラメーター</th>
<th align="left">説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>1</p></td>
<td align="left"><p><strong>0:</strong>システム PTE 型の拡張</p>
<p><strong>1:</strong>非ページ プールの拡張 PTE 型</p></td>
</tr>
<tr class="even">
<td align="left"><p>2</p></td>
<td align="left"><p>メモリの要求のサイズ</p></td>
</tr>
<tr class="odd">
<td align="left"><p>3</p></td>
<td align="left"><p>合計空きシステム Pte</p></td>
</tr>
<tr class="even">
<td align="left"><p>4</p></td>
<td align="left"><p>システム Pte を合計します。</p></td>
</tr>
</tbody>
</table>

 

<a name="cause"></a>原因
-----

ほぼすべての場合、システムが実際に Pte 外です。 代わりに、ドライバーには、メモリの大きなブロックが要求されたが、この要求を満たすための十分なサイズの連続したブロックはありません。

多くの場合、ビデオ ドライバーには、大量の成功する必要がありますカーネル メモリが割り当てられます。 一部のバックアップ プログラムの同じ操作を行います。

<a name="resolution"></a>解決方法
----------

**考えられる回避:** システム Pte の合計数を増やすにレジストリを変更します。 これは解決しません。 最近インストールされたソフトウェアを削除、特にユーティリティ、またはディスク処理を要するアプリケーションをバックアップします。

**この問題をデバッグするには。** バグ チェック 0x3F をデバッグするは、次のメソッドを使用できます。

最初に、スタック トレースを取得し、使用して、 [ **! sysptes 3** ](-sysptes.md)拡張機能コマンド。

**HKEY\_ローカル\_マシン\\システム\\CurrentControlSet\\コントロール\\セッション マネージャー\\メモリ管理\\TrackPtes** DWORD 1 に等しくなり、再起動します。 これにより、スタック トレースを保存するシステムです。

これにより、PTE 所有者に関する詳細な情報を表示することができます。 次に、例を示します。

```dbgcmd
0: kd> !sysptes 4

0x2c47 System PTEs allocated to mapping locked pages

VA       MDL     PageCount  Caller/CallersCaller
f0e5db48 eb6ceef0        1 ntkrpamp!MmMapLockedPages+0x15/ntkrpamp!IopfCallDriver+0x35
f0c3fe48 eb634bf0        1 netbt!NbtTdiAssociateConnection+0x1f/netbt!DelayedNbtProcessConnect+0x17c
f0db38e8 eb65b880        1 mrxsmb!SmbMmAllocateSessionEntry+0x89/mrxsmb!SmbCepInitializeExchange+0xda
f8312568 eb6df880        1 rdbss!RxCreateFromNetRoot+0x3d7/rdbss!RxCreateFromNetRoot+0x93
f8363908 eb685880        1 mrxsmb!SmbMmAllocateSessionEntry+0x89/mrxsmb!SmbCepInitializeExchange+0xda
f0c54248 eb640880        1 rdbss!RxCreateFromNetRoot+0x3d7/rdbss!RxCreateFromNetRoot+0x93
f0ddf448 eb5f3160        1 mrxsmb!MrxSmbUnalignedDirEntryCopyTail+0x387/mrxsmb!MRxSmbCoreInformation+0x36
f150bc08 eb6367b0        1 mrxsmb!MrxSmbUnalignedDirEntryCopyTail+0x387/mrxsmb!MRxSmbCoreInformation+0x36
f1392308 eb6fba70        1 netbt!NbtTdiOpenAddress+0x1fb/netbt!DelayedNbtProcessConnect+0x17c
eb1bee64 edac5000      200 VIDEOPRT!pVideoPortGetDeviceBase+0x118/VIDEOPRT!VideoPortMapMemory+0x45
f139b5a8 edd4b000       12 rdbss!FsRtlCopyWrite2+0x34/rdbss!RxDriverEntry+0x149
eb41f400 ede92000       20 VIDEOPRT!pVideoPortGetDeviceBase+0x139/VIDEOPRT!VideoPortGetDeviceBase+0x1b
eb41f198 edf2a000       20 NDIS!NdisReadNetworkAddress+0x3a/NDIS!NdisFreeSharedMemory+0x58
eb41f1e4 eb110000       10 VIDEOPRT!pVideoPortGetDeviceBase+0x139/VIDEOPRT!VideoPortGetDeviceBase+0x1b
......
```

不足した場合、システム Pte 後でもう一度、 **TrackPtes**レジストリ値が設定されている、 [**バグ チェック 0xD8** ](bug-check-0xd8--driver-used-excessive-ptes.md) (ドライバー\_使用\_が多すぎます。\_PTE) 0x3F の代わりに発行されます。 このエラーの原因で、ドライバーの名前がも表示されます。

 

 




