---
title: バグチェック 0xD2 BUGCODE_ID_DRIVER
description: BUGCODE_ID_DRIVER バグチェックの値は0x000000D2 です。 これは、NDIS ドライバーで問題が発生したことを示します。
ms.assetid: 697d128c-c79d-454a-a3e7-e9b85e3ab4bc
keywords:
- バグチェック 0xD2 BUGCODE_ID_DRIVER
- BUGCODE_ID_DRIVER
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- BUGCODE_ID_DRIVER
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 4fae927262fcb092aab82033896302c73e2ba1e1
ms.sourcegitcommit: 3ec971f54122b77408433f7f1e59c467099fb4de
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/21/2020
ms.locfileid: "86873851"
---
# <a name="bug-check-0xd2-bugcode_id_driver"></a>バグチェック 0xD2: バグコード \_ ID \_ ドライバー


\_バグコード ID ドライバーのバグチェックには、 \_ 0x000000D2 の値が含まれています。 これは、NDIS ドライバーで問題が発生したことを示します。

> [!IMPORTANT]
> このトピックはプログラマーを対象としています。 コンピューターの使用中にブルースクリーンのエラーコードが表示された顧客の場合は、「[ブルースクリーンエラーのトラブルシューティング](https://www.windows.com/stopcode)」を参照してください。


## <a name="bugcode_id_driver-parameters"></a>バグコード \_ ID \_ ドライバーのパラメーター


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
<th align="left">パラメーター3</th>
<th align="left">パラメーター4</th>
<th align="left">メッセージと原因</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>ミニポートブロックのアドレス</p></td>
<td align="left"><p>要求されたバイト数</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>1</p></td>
<td align="left"><p><strong>発生した IRQL で共有メモリを割り当てています。</strong> IRQL = DISPATCH_LEVEL を持つ<strong>NdisMAllocateSharedMemory</strong>という名前のドライバー &gt; 。</p></td>
</tr>
<tr class="even">
<td align="left"><p>ミニポートブロックのアドレス</p></td>
<td align="left"><p><strong>NdisMResetComplete</strong>に送信された<em>状態</em>の値</p></td>
<td align="left"><p><strong>NdisMResetComplete</strong>に送信される<em>addressingreset</em>値</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p><strong>保留中のリセットを完了します。</strong> ドライバーは<strong>NdisMResetComplete</strong>を呼び出しましたが、リセットは保留されていませんでした。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>ミニポートブロックのアドレス</p></td>
<td align="left"><p>解放されているアドレスを含むメモリページ</p></td>
<td align="left"><p>共有メモリ署名のアドレス</p></td>
<td align="left"><p>仮想アドレスが解放されています</p></td>
<td align="left"><p><strong>割り当てられていない共有メモリを解放しています。</strong> <strong>NdisMFreeSharedMemory</strong>または<strong>NdisMFreeSharedMemoryAsync</strong>という名前のドライバーで、NDIS 共有メモリに存在しないアドレスが使用されています。</p></td>
</tr>
<tr class="even">
<td align="left"><p>ミニポートブロックのアドレス</p></td>
<td align="left"><p>パケット配列に誤って含まれているパケットのアドレス</p></td>
<td align="left"><p>パケット配列のアドレス</p></td>
<td align="left"><p>配列内のパケット数</p></td>
<td align="left"><p><strong>パケットが所有していないことを示します。</strong> ミニポートのパケット配列が破損しています。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>ミニブロックのアドレス</p></td>
<td align="left"><p>ドライバーオブジェクトのアドレス</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p><strong>NdisAddDevice: AddDevice</strong>が<strong>NdisMiniDriverList</strong>上にない<strong>miniblock</strong>を使用して呼び出されました。</p></td>
</tr>
<tr class="even">
<td align="left"><p>ミニブロックのアドレス</p></td>
<td align="left"><p>MiniBlock の参照カウント</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p><strong>NdisMUnload: MiniBlock</strong>はアンロードされていますが、まだ<strong>NdisMiniDriverList</strong>にあります。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>ミニポートブロックのアドレス</p></td>
<td align="left"><p>[メモリ] ページ</p></td>
<td align="left"><p>ラッパーコンテキスト</p></td>
<td align="left"><p>共有メモリ署名のアドレス</p></td>
<td align="left"><p><strong>以前に割り当てられた共有メモリを上書きします。</strong> 書き込まれているアドレスが NDIS 共有メモリにありません。</p></td>
</tr>
</tbody>
</table>

 

このバグチェックの次のインスタンスでは、パラメーターの意味はメッセージとパラメーター4の値によって異なります。

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
<th align="left">パラメーター3</th>
<th align="left">パラメーター4</th>
<th align="left">メッセージと原因</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>ミニポートブロックのアドレス</p></td>
<td align="left"><p>ミニポート割り込みのアドレス</p></td>
<td align="left"><p>ミニポートタイマーキューのアドレス</p></td>
<td align="left"><p>1</p></td>
<td align="left"><p><strong>登録解除を中断せずにアンロードしています。</strong> ミニポートドライバーは、割り込みを解除せずに初期化に失敗しました。</p></td>
</tr>
<tr class="even">
<td align="left"><p>ミニポートブロックのアドレス</p></td>
<td align="left"><p>ミニポートタイマーキューのアドレス</p></td>
<td align="left"><p>ミニポート割り込みのアドレス</p></td>
<td align="left"><p>2</p></td>
<td align="left"><p><strong>登録解除を中断せずにアンロードしています。</strong> ミニポートドライバーは、停止処理中に割り込みを登録解除しませんでした。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>ミニポートブロックのアドレス</p></td>
<td align="left"><p>ミニポート割り込みのアドレス</p></td>
<td align="left"><p>ミニポートタイマーキューのアドレス</p></td>
<td align="left"><p>1</p></td>
<td align="left"><p><strong>アンロードタイマーなしでアンロードしています。</strong> ミニポートドライバーは、すべてのタイマーを正常にキャンセルせずに初期化に失敗しました。</p></td>
</tr>
<tr class="even">
<td align="left"><p>ミニポートブロックのアドレス</p></td>
<td align="left"><p>ミニポートタイマーキューのアドレス</p></td>
<td align="left"><p>ミニポート割り込みのアドレス</p></td>
<td align="left"><p>2</p></td>
<td align="left"><p><strong>アンロードタイマーなしでアンロードしています。</strong> ミニポートドライバーは、すべてのタイマーを正常にキャンセルせずに停止しました。</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>解説
-------

このバグチェックコードは、Windows 2000 および Windows XP でのみ発生します。 Windows Server 2003 以降では、対応するコードは、[**バグチェック 0x7C (バグ**](bug-check-0x7c--bugcode-ndis-driver.md)コード \_ NDIS \_ ドライバー) です。

Windows のチェックされたビルドでは、このバグチェックが**保留状態**になっている場合に、**共有メモリの割り当てが発生**したときにのみリセットを完了します。 バグチェック0xD2 の他のすべてのインスタンスは、アサートで置き換えられます。 詳細について[は、「デバッガーの中断](breaking-into-the-debugger.md)」を参照してください。

> [!NOTE]
> チェックを行ったビルドは、Windows 10 バージョン1803より前の古いバージョンの Windows で使用できました。
> Driver Verifier や GFlags などのツールを使用して、新しいバージョンの Windows でドライバーコードを確認します。
 

 




