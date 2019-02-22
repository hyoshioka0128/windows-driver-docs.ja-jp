---
title: バグ チェック 0xD2 BUGCODE_ID_DRIVER
description: BUGCODE_ID_DRIVER のバグ チェックでは、0x000000D2 の値を持ちます。 これは、NDIS ドライバーで問題が発生したことを示します。
ms.assetid: 697d128c-c79d-454a-a3e7-e9b85e3ab4bc
keywords:
- バグ チェック 0xD2 BUGCODE_ID_DRIVER
- BUGCODE_ID_DRIVER
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- BUGCODE_ID_DRIVER
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: d575ede17b41c115a383c67f325bdd56ce78d91b
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56528918"
---
# <a name="bug-check-0xd2-bugcodeiddriver"></a>バグ チェック 0xD2 の。BUGCODE\_ID\_ドライバー


BUGCODE\_ID\_ドライバーのバグ チェックが 0x000000D2 の値を持ちます。 これは、NDIS ドライバーで問題が発生したことを示します。

**重要な**プログラマ向けのトピックです。 コンピューターを使用しているときに、エラー コードがブルー スクリーンが受信した顧客の場合を参照してください。[トラブルシューティング ブルー スクリーン エラー](https://windows.microsoft.com/windows-10/troubleshoot-blue-screen-errors)します。

## <a name="bugcodeiddriver-parameters"></a>BUGCODE\_ID\_ドライバーのパラメーター


<table>
<colgroup>
<col width="20%" />
<col width="20%" />
<col width="20%" />
<col width="20%" />
<col width="20%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">パラメーター 1</th>
<th align="left">パラメータ 2</th>
<th align="left">3 番目のパラメーター</th>
<th align="left">パラメーター 4</th>
<th align="left">メッセージと原因</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>ミニポート ブロックのアドレス</p></td>
<td align="left"><p>要求されたバイト数</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>1</p></td>
<td align="left"><p><strong>発生した IRQL で共有メモリを割り当てています。</strong> ドライバーと呼ばれる<strong>NdisMAllocateSharedMemory</strong> IRQL で&gt;= DISPATCH_LEVEL します。</p></td>
</tr>
<tr class="even">
<td align="left"><p>ミニポート ブロックのアドレス</p></td>
<td align="left"><p><em>状態</em>に送信された値<strong>NdisMResetComplete</strong></p></td>
<td align="left"><p><em>AddressingReset</em>に送信された値<strong>NdisMResetComplete</strong></p></td>
<td align="left"><p>0</p></td>
<td align="left"><p><strong>リセットを完了して、いずれかが保留中ではありません。</strong> ドライバーと呼ばれる<strong>NdisMResetComplete</strong>、保留中のリセットがありませんでしたが。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>ミニポート ブロックのアドレス</p></td>
<td align="left"><p>解放されているアドレスを格納しているメモリ ページ</p></td>
<td align="left"><p>共有メモリのシグネチャのアドレス</p></td>
<td align="left"><p>解放されている仮想アドレス</p></td>
<td align="left"><p><strong>割り当てられていない共有メモリを解放します。</strong> ドライバーと呼ばれる<strong>NdisMFreeSharedMemory</strong>または<strong>NdisMFreeSharedMemoryAsync</strong> NDIS に配置されていないアドレスにメモリを共有します。</p></td>
</tr>
<tr class="even">
<td align="left"><p>ミニポート ブロックのアドレス</p></td>
<td align="left"><p>パケットの配列に正しく含まれるパケットのアドレス</p></td>
<td align="left"><p>パケットの配列のアドレス</p></td>
<td align="left"><p>配列内のパケットの数</p></td>
<td align="left"><p><strong>これが所有していないパケットを示すです。</strong> ミニポート&#39;s パケットの配列が破損しています。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>MiniBlock のアドレス</p></td>
<td align="left"><p>ドライバー オブジェクトのアドレス</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p><strong>NdisAddDevice:AddDevice</strong>という、 <strong>MiniBlock</strong>オンでない、 <strong>NdisMiniDriverList</strong>します。</p></td>
</tr>
<tr class="even">
<td align="left"><p>MiniBlock のアドレス</p></td>
<td align="left"><p>MiniBlock&#39;s 参照カウント</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p><strong>NdisMUnload:MiniBlock</strong>がアンロードを取得するが、まだが<strong>NdisMiniDriverList</strong>します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>ミニポート ブロックのアドレス</p></td>
<td align="left"><p>[メモリ] ページ</p></td>
<td align="left"><p>ラッパーのコンテキスト</p></td>
<td align="left"><p>共有メモリのシグネチャのアドレス</p></td>
<td align="left"><p><strong>共有メモリの割り当てを過去の上書きされました。</strong> NDIS 共有メモリ内に書き込まれるアドレスが見つかりませんでした。</p></td>
</tr>
</tbody>
</table>

 

このバグ チェックの次のインスタンスでは、パラメーターの意味は、メッセージとパラメーター 4 の値によって異なります。

<table>
<colgroup>
<col width="20%" />
<col width="20%" />
<col width="20%" />
<col width="20%" />
<col width="20%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">パラメーター 1</th>
<th align="left">パラメータ 2</th>
<th align="left">3 番目のパラメーター</th>
<th align="left">パラメーター 4</th>
<th align="left">メッセージと原因</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>ミニポート ブロックのアドレス</p></td>
<td align="left"><p>ミニポート割り込みのアドレス</p></td>
<td align="left"><p>ミニポート タイマー キューのアドレス</p></td>
<td align="left"><p>1</p></td>
<td align="left"><p><strong>割り込みの登録を解除せずアンロードします。</strong> ミニポート ドライバーでは、その割り込みの登録を解除せず、初期化できませんでした。</p></td>
</tr>
<tr class="even">
<td align="left"><p>ミニポート ブロックのアドレス</p></td>
<td align="left"><p>ミニポート タイマー キューのアドレス</p></td>
<td align="left"><p>ミニポート割り込みのアドレス</p></td>
<td align="left"><p>2</p></td>
<td align="left"><p><strong>割り込みの登録を解除せずアンロードします。</strong> ミニポート ドライバーは、その割り込みが停止処理中に登録解除できませんでした。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>ミニポート ブロックのアドレス</p></td>
<td align="left"><p>ミニポート割り込みのアドレス</p></td>
<td align="left"><p>ミニポート タイマー キューのアドレス</p></td>
<td align="left"><p>1</p></td>
<td align="left"><p><strong>タイマーの登録を解除せずにアンロードします。</strong> ミニポート ドライバーでは、正常にそのすべてのタイマーをキャンセルせず、初期化できませんでした。</p></td>
</tr>
<tr class="even">
<td align="left"><p>ミニポート ブロックのアドレス</p></td>
<td align="left"><p>ミニポート タイマー キューのアドレス</p></td>
<td align="left"><p>ミニポート割り込みのアドレス</p></td>
<td align="left"><p>2</p></td>
<td align="left"><p><strong>タイマーの登録を解除せずにアンロードします。</strong> ミニポート ドライバーは、正常にそのすべてのタイマーをキャンセルせずに停止されました。</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>注釈
-------

このバグ チェック コードは、Windows 2000 および Windows XP でのみ行われます。 対応するコードは、Windows Server 2003 以降では、 [**バグ チェック 0x7C** ](bug-check-0x7c--bugcode-ndis-driver.md) (BUGCODE\_NDIS\_ドライバー)。

、Windows のチェック ビルドのみで、**発生 IRQL で共有メモリの割り当て**と**待ちになって完了リセット時に 1 つは、** このバグ チェックのインスタンスが発生することができます。 バグの他のすべてのインスタンスでは、0xD2 のアサートは置き換えを確認します。 参照してください[、デバッガーに重大な](breaking-into-the-debugger.md)詳細についてはします。

 

 




