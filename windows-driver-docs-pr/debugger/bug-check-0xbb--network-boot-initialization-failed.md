---
title: バグ チェック 0 xbb です NETWORK_BOOT_INITIALIZATION_FAILED
description: NETWORK_BOOT_INITIALIZATION_FAILED のバグ チェックでは、0x000000BB の値を持ちます。 これは、Windows が正常にネットワークから起動に失敗したことを示します。
ms.assetid: 1cc86ca0-437d-4a26-90ed-76f122c522ef
keywords:
- バグ チェック 0 xbb です NETWORK_BOOT_INITIALIZATION_FAILED
- NETWORK_BOOT_INITIALIZATION_FAILED
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- NETWORK_BOOT_INITIALIZATION_FAILED
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: b7a5118b7c5c32b028a396caa9944fa6a9dcb66e
ms.sourcegitcommit: 55d7f63bb9e7668d65aa0999e65d18fabd44758e
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/08/2019
ms.locfileid: "59238849"
---
# <a name="bug-check-0xbb-networkbootinitializationfailed"></a>バグ チェック 0xBB:ネットワーク\_ブート\_初期化\_失敗


ネットワーク\_ブート\_初期化\_失敗のバグ チェックが 0x000000BB の値を持ちます。 これは、Windows が正常にネットワークから起動に失敗したことを示します。

> [!IMPORTANT]
> このトピックはプログラマーを対象としています。 コンピューターを使用しているときに、エラー コードがブルー スクリーンが受信した顧客の場合を参照してください。[トラブルシューティング ブルー スクリーン エラー](https://windows.microsoft.com/windows-10/troubleshoot-blue-screen-errors)します。


## <a name="networkbootinitializationfailed-parameters"></a>ネットワーク\_ブート\_初期化\_FAILED パラメーター


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
<td align="left"><p>失敗したネットワークの初期化の一部です。 設定可能な値は、次のとおりです。</p>
<p><strong>1:</strong>レジストリの更新に失敗しました。</p>
<p><strong>2:</strong>ネットワーク スタックの開始中に失敗しました。 Windows は Ioctl をリダイレクターとデータグラムの受信者に送信し、リダイレクターが準備できるまで待機します。 準備が一定期間内でない場合は、このエラーが発生します。</p>
<p><strong>3:</strong>DHCP の IOCTL に TCP 送信中に失敗しました。 これは、Windows がその IP アドレスのトランスポートに通知されます。</p></td>
</tr>
<tr class="even">
<td align="left"><p>2</p></td>
<td align="left"><p>エラー状態</p></td>
</tr>
<tr class="odd">
<td align="left"><p>3</p></td>
<td align="left"><p>予約済み</p></td>
</tr>
<tr class="even">
<td align="left"><p>4</p></td>
<td align="left"><p>予約済み</p></td>
</tr>
</tbody>
</table>

 

<a name="cause"></a>原因
-----

Windows は、ネットワークからブートと重要な機能は、I/O の初期化中に失敗した場合、このエラーが発生します。

 

 




