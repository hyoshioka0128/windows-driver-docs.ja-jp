---
title: バグ チェック 0xD0 DRIVER_CORRUPTED_MMPOOL
description: DRIVER_CORRUPTED_MMPOOL のバグ チェックでは、0x000000D0 の値を持ちます。 これは、システムがプロセスが高すぎる IRQL で無効なメモリへのアクセスを試行したことを示します。
ms.assetid: fad53a11-d4db-4f2c-b03e-19c5db47975b
keywords:
- バグ チェック 0xD0 DRIVER_CORRUPTED_MMPOOL
- DRIVER_CORRUPTED_MMPOOL
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- DRIVER_CORRUPTED_MMPOOL
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: f0d87d85eebaf414ce7e6a4aa25afde823baf81c
ms.sourcegitcommit: d03b44343cd32b3653d0471afcdd3d35cb800c0d
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/02/2019
ms.locfileid: "67518889"
---
# <a name="bug-check-0xd0-drivercorruptedmmpool"></a>バグ チェック 0xD0:ドライバー\_破損した\_MMPOOL


ドライバー\_破損した\_MMPOOL バグ チェックが 0x000000D0 の値を持ちます。 これは、システムがプロセスが高すぎる IRQL で無効なメモリへのアクセスを試行したことを示します。

> [!IMPORTANT]
> このトピックはプログラマーを対象としています。 コンピューターを使用しているときに、エラー コードがブルー スクリーンが受信した顧客の場合を参照してください。[トラブルシューティング ブルー スクリーン エラー](https://www.windows.com/stopcode)します。


## <a name="drivercorruptedmmpool-parameters"></a>ドライバー\_破損した\_MMPOOL パラメーター


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
<td align="left"><p>参照されるメモリ</p></td>
</tr>
<tr class="even">
<td align="left"><p>2</p></td>
<td align="left"><p>IRQL の参照時に</p></td>
</tr>
<tr class="odd">
<td align="left"><p>3</p></td>
<td align="left"><p><strong>0:</strong>Read</p>
<p><strong>1:</strong>書き込み</p></td>
</tr>
<tr class="even">
<td align="left"><p>4</p></td>
<td align="left"><p>メモリ アドレス</p></td>
</tr>
</tbody>
</table>

 

<a name="cause"></a>原因
-----

ページング可能なメモリ (または、完全に無効なメモリ) にアクセスしようとする、カーネルの IRQL が高すぎる場合にします。 この問題の究極的な原因は、ほぼ間違いなく、システム プールが破損しているドライバーです。

ほとんどの場合、このバグ チェックの結果、ドライバーの破損を大規模に割り当てられた場合 (ページ\_サイズ以上)。 割り当てが少ないと、 [**バグ チェック 0xC5** ](bug-check-0xc5--driver-corrupted-expool.md) (ドライバー\_破損した\_EXPOOL)。

<a name="resolution"></a>解決方法
----------

最近、新しいソフトウェアをインストールした場合が正しくインストールされてかどうかを確認します。 製造元の web サイトで更新されたドライバーを確認します。

このエラーをデバッグするには、Driver Verifier の特別なプールのオプションを使用します。 エラーが発生したドライバーを明らかにこれが失敗した場合は、グローバル フラグ ユーティリティを使用して、特別なプールでプール タグを有効にします。

特別なプールについては、Windows ドライバー キットの Driver Verifier のセクションを参照してください。

代替の方法は、開きます、  **\\ \\HKEY\_ローカル\_マシン\\システム\\CurrentControlSet\\コントロール\\セッションManager\\メモリ管理**レジストリ キー。 このキーを作成または編集、 **ProtectNonPagedPool**値、され、DWORD 1 に設定します。 再起動します。 システムは、解放されたすべての非ページ プールをマップ解除されます。 これにより、プールの破損からドライバーを防ぎます。 (これは保護されません、プールから DMA のハードウェア、ただし。)

 

 




