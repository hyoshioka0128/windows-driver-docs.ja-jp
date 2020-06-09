---
title: バグチェック 0xC5 DRIVER_CORRUPTED_EXPOOL
description: DRIVER_CORRUPTED_EXPOOL のバグチェックには、値0x000000C5 があります。 これは、システムが高すぎたプロセス IRQL で無効なメモリにアクセスしようとしたことを示します。
ms.assetid: e375e7d3-9cb1-474f-ade2-1bc65dd79864
keywords:
- バグチェック 0xC5 DRIVER_CORRUPTED_EXPOOL
- DRIVER_CORRUPTED_EXPOOL
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- DRIVER_CORRUPTED_EXPOOL
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 08a9d8ed31366747b6f3c4aa76210ad2c7df4ab9
ms.sourcegitcommit: dadc9ced1670d667e31eb0cb58d6a622f0f09c46
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/09/2020
ms.locfileid: "84534791"
---
# <a name="bug-check-0xc5-driver_corrupted_expool"></a>バグチェック 0xC5: ドライバーが破損した \_ \_ expool


ドライバーの \_ 破損した \_ expool バグチェックには、値0x000000C5 があります。 これは、システムが高すぎたプロセス IRQL で無効なメモリにアクセスしようとしたことを示します。

> [!IMPORTANT]
> このトピックはプログラマーを対象としています。 コンピューターの使用中にブルースクリーンのエラーコードが表示された顧客の場合は、「[ブルースクリーンエラーのトラブルシューティング](https://www.windows.com/stopcode)」を参照してください。


## <a name="driver_corrupted_expool-parameters"></a>ドライバーが破損した \_ \_ Expool パラメーター


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
<td align="left"><p>参照時の IRQL</p></td>
</tr>
<tr class="odd">
<td align="left"><p>3</p></td>
<td align="left"><p><strong>0:</strong>込ん</p>
<p><strong>1:</strong>企画</p></td>
</tr>
<tr class="even">
<td align="left"><p>4</p></td>
<td align="left"><p>参照されたメモリのアドレス</p></td>
</tr>
</tbody>
</table>

 

<a name="cause"></a>原因
-----

カーネルが、IRQL が高すぎるときに、ページング可能なメモリ (または完全に無効なメモリ) にアクセスしようとしました。 この問題の最終的な原因は、ほとんどの場合、システムプールが破損しているドライバーです。

ほとんどの場合、このバグチェックは、ドライバーが小さな割り当て (ページサイズ未満) を破損した場合に実行さ \_ れます。 割り当てが大きいと、[**バグチェック 0xD0**](bug-check-0xd0--driver-corrupted-mmpool.md) (ドライバーが \_ 破損 \_ した mmpool) になります。

<a name="resolution"></a>解像度
----------

! [デバッグ拡張機能の[**分析**](-analyze.md)] には、バグチェックに関する情報が表示され、根本原因を特定するのに役立ちます。 新しいソフトウェアを最近インストールした場合は、それが正しくインストールされているかどうかを確認します。 製造元の web サイトで更新されたドライバーを確認します。

このエラーをデバッグするには、Driver Verifier の special pool オプションを使用します。 このエラーの原因となったドライバーが明らかに失敗した場合は、グローバルフラグユーティリティを使用して、特別なプールタグを有効にします。

特別なプールの詳細については、『 Windows Driver Kit 』の「 [Driver Verifier](https://docs.microsoft.com/windows-hardware/drivers/devtest/driver-verifier) 」セクションを参照してください。

 

 




