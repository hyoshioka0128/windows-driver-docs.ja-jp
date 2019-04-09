---
title: バグ チェック 0x10E VIDEO_MEMORY_MANAGEMENT_INTERNAL
description: VIDEO_MEMORY_MANAGEMENT_INTERNAL のバグ チェックでは、0x0000010E の値を持ちます。 これは、ビデオ メモリ マネージャーがないから回復できるように条件を発生したことを示します。
ms.assetid: 2fb29098-084c-462a-bb06-789e73924d16
keywords:
- バグ チェック 0x10E VIDEO_MEMORY_MANAGEMENT_INTERNAL
- VIDEO_MEMORY_MANAGEMENT_INTERNAL
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- VIDEO_MEMORY_MANAGEMENT_INTERNAL
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 97a048d99b5a4a6ceb5d33184773f6b432237865
ms.sourcegitcommit: 55d7f63bb9e7668d65aa0999e65d18fabd44758e
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/08/2019
ms.locfileid: "59239825"
---
# <a name="bug-check-0x10e-videomemorymanagementinternal"></a>バグ チェック 0x10E:ビデオ\_メモリ\_管理\_内部


ビデオ\_メモリ\_管理\_内部バグ チェックが 0x0000010E の値を持ちます。 これは、ビデオ メモリ マネージャーがないから回復できるように条件を発生したことを示します。

> [!IMPORTANT]
> このトピックはプログラマーを対象としています。 コンピューターを使用しているときに、エラー コードがブルー スクリーンが受信した顧客の場合を参照してください。[トラブルシューティング ブルー スクリーン エラー](https://windows.microsoft.com/windows-10/troubleshoot-blue-screen-errors)します。


## <a name="videomemorymanagementinternal-parameters"></a>ビデオ\_メモリ\_管理\_内部パラメーター


パラメーター 1 が; 関心のある唯一のパラメーターこれは、正確な違反を識別します。 パラメーター 1 の値であり、このテーブルに表示されないを個別に調査する必要があります。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">パラメーター 1</th>
<th align="left">エラーの原因</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>0x1</p></td>
<td align="left"><p>回転回転以外の範囲が試行されました。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x2</p></td>
<td align="left"><p>空でないプロセス ヒープを破棄しようとしました。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x3</p></td>
<td align="left"><p>Aperture セグメントからマップ解除に失敗しました。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x4</p></td>
<td align="left"><p>回転をする必要があります-成功パスが失敗しました。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x5</p></td>
<td align="left"><p>遅延のコマンドが失敗しました。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x6</p></td>
<td align="left"><p>割り当てをその削除が取り消されましたがあるリソースの再割り当てが試行されました。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x7</p></td>
<td align="left"><p>無料使用量を延期する無効なしようとしました。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x8</p></td>
<td align="left"><p>分割のダイレクト メモリ アクセス (DMA) バッファーには、無効な参照が含まれています。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x9</p></td>
<td align="left"><p>割り当ての削除に失敗しました。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0 xa</p></td>
<td align="left"><p>固定された割り当てを使用する、無効なしようとしました。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0 xb</p></td>
<td align="left"><p>ドライバーから無効なエラー コードが返された<em>BuildPagingBuffer</em>します。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0 xc</p></td>
<td align="left"><p>セグメントでは、リソースのリークが検出されました。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0 xd</p></td>
<td align="left"><p>セグメントを正しく使用されています。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0xE</p></td>
<td align="left"><p>マップの開口部セグメントに割り当てに失敗しました。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0 xf です.</p></td>
<td align="left"><p>ドライバーから無効なエラー コードが返された<em>AcquireSwizzlingRange</em>します。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x10</p></td>
<td align="left"><p>ドライバーから無効なエラー コードが返された<em>ReleaseSwizzlingRange</em>します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x11</p></td>
<td align="left"><p>Aperture セグメントを使用する、無効なしようとしました。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x12</p></td>
<td align="left"><p>ドライバーには、指定された DMA バッファーがオーバーフローしました。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x13</p></td>
<td align="left"><p>ドライバーには、指定されたプライベート データ バッファーがオーバーフローしました。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x14</p></td>
<td align="left"><p>すべてのセグメントの消去に失敗しました。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x15</p></td>
<td align="left"><p>回転された状態で引き続き仮想アドレス記述子 (VAD) を解放しようとしました。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x16</p></td>
<td align="left"><p>ドライバーが保証された DMA バッファー モデル コントラクトを中断します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x17</p></td>
<td align="left"><p>予期しないシステムのコマンド エラーが発生しました。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x18</p></td>
<td align="left"><p>固定された割り当てのリソースを解放できませんでした。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x19</p></td>
<td align="left"><p>ドライバーは、DMA バッファーの修正プログラムを適用できませんでした。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x1A</p></td>
<td align="left"><p>共有の割り当ての所有者が解放されました。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x1B</p></td>
<td align="left"><p>使用中である aperture 範囲を解放しようとしました。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x25</p></td>
<td align="left"><p>GPU は、開口部の未定義の領域上を書き込もうとしました。</p></td>
</tr>
</tbody>
</table>

 

<a name="cause"></a>原因
-----

このバグ チェックが正しく動作して、ビデオ ドライバー通常発生します。

<a name="resolution"></a>解決方法
----------

問題が解決しない場合は、ビデオ ドライバーの更新の Windows 更新プログラムを確認します。

 

 




