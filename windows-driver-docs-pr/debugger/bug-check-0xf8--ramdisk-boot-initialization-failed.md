---
title: バグ チェック 0xF8 RAMDISK_BOOT_INITIALIZATION_FAILED
description: RAMDISK_BOOT_INITIALIZATION_FAILED のバグ チェックでは、0x000000F8 の値を持ちます。 これは、RAM ディスクからの起動を試みているときに初期化エラーが発生したことを示します。
ms.assetid: 73b053af-6ecb-48a3-b09d-e28d39390d11
keywords:
- バグ チェック 0xF8 RAMDISK_BOOT_INITIALIZATION_FAILED
- RAMDISK_BOOT_INITIALIZATION_FAILED
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- RAMDISK_BOOT_INITIALIZATION_FAILED
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: a5e99730a62ccf00c7c275e4d6b3326af3076d0a
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67367061"
---
# <a name="bug-check-0xf8-ramdiskbootinitializationfailed"></a>バグ チェック 0xF8:RAMDISK\_ブート\_初期化\_失敗


RAMDISK\_ブート\_初期化\_失敗のバグ チェックが 0x000000F8 の値を持ちます。 これは、RAM ディスクからの起動を試みているときに初期化エラーが発生したことを示します。

> [!IMPORTANT]
> このトピックはプログラマーを対象としています。 コンピューターを使用しているときに、エラー コードがブルー スクリーンが受信した顧客の場合を参照してください。[トラブルシューティング ブルー スクリーン エラー](https://support.microsoft.com/help/14238/windows-10-troubleshoot-blue-screen-errors)します。


## <a name="ramdiskbootinitializationfailed-parameters"></a>RAMDISK\_ブート\_初期化\_FAILED パラメーター


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
<td align="left"><p>エラーの原因を示します。</p>
<p><strong>1:</strong>ローダーのメモリの一覧で、LoaderXIPRom 記述子が見つかりませんでした。</p>
<p><strong>2:</strong>RAM ディスク ドライバー (ramdisk.sys または \Device\Ramdisk) を開けません。</p>
<p><strong>3:</strong>FSCTL_CREATE_RAM_DISK に失敗しました。</p>
<p><strong>4:</strong>バイナリの GUID を GUID 文字列を作成できません。</p>
<p><strong>5:</strong>RAM ディスク デバイスへのシンボリック リンクを作成できません。</p></td>
</tr>
<tr class="even">
<td align="left"><p>2</p></td>
<td align="left"><p>NTSTATUS コード</p></td>
</tr>
<tr class="odd">
<td align="left"><p>3</p></td>
<td align="left"><p>0</p></td>
</tr>
<tr class="even">
<td align="left"><p>4</p></td>
<td align="left"><p>0</p></td>
</tr>
</tbody>
</table>

 

 

 




