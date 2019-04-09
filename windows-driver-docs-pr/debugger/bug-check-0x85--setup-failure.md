---
title: バグ チェック 0x85 SETUP_FAILURE
description: SETUP_FAILURE のバグ チェックでは、0x00000085 の値を持ちます。 このバグ チェックでは、セットアップ中に致命的なエラーが発生したことを示します。
ms.assetid: 52c93485-7c20-4a7e-8fc7-d520753973ed
keywords:
- バグ チェック 0x85 SETUP_FAILURE
- SETUP_FAILURE
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- SETUP_FAILURE
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: eab60f0a67d6a3088b036248ab9004abc8800bcc
ms.sourcegitcommit: 55d7f63bb9e7668d65aa0999e65d18fabd44758e
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/08/2019
ms.locfileid: "59239295"
---
# <a name="bug-check-0x85-setupfailure"></a>バグ チェック 0x85:セットアップ\_エラー


セットアップ\_エラーのバグ チェックが 0x00000085 の値を持ちます。 このバグ チェックでは、セットアップ中に致命的なエラーが発生したことを示します。

> [!IMPORTANT]
> このトピックはプログラマーを対象としています。 コンピューターを使用しているときに、エラー コードがブルー スクリーンが受信した顧客の場合を参照してください。[トラブルシューティング ブルー スクリーン エラー](https://windows.microsoft.com/windows-10/troubleshoot-blue-screen-errors)します。


## <a name="setupfailure-parameters"></a>セットアップ\_エラー パラメーター


パラメーター 1 では、違反の種類を示します。 パラメーター 4 には使用されません。 その他のパラメーターの意味は、パラメーター 1 の値によって異なります。

<table>
<colgroup>
<col width="25%" />
<col width="25%" />
<col width="25%" />
<col width="25%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">パラメーター 1</th>
<th align="left">パラメータ 2</th>
<th align="left">3 番目のパラメーター</th>
<th align="left">原因</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>0x0</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>OEM HAL フォントは有効な .fon フォーマット ファイルでは、ためセットアップは、テキストを表示できません。</p>
<p>この原因には、ことを示します Vga<em>xxx</em>ブート フロッピー ディスクまたは CD に .fon が破損しています。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x1</p></td>
<td align="left"><p>正確なビデオの初期化エラー:</p>
<p><strong>0:NtCreateFile</strong> of \device\video0</p>
<p><strong>1:</strong>IOCTL_VIDEO_QUERY_NUM_AVAIL_MODES</p>
<p><strong>2:</strong>IOCTL_VIDEO_QUERY_AVAIL_MODES</p>
<p><strong>3:</strong>目的のビデオ モードがサポートされていません。 この値は、セットアップの内部エラーを示します。</p>
<p><strong>4:</strong>IOCTL_VIDEO_SET_CURRENT_MODE (ビデオのモードを設定することができません)</p>
<p><strong>5:</strong>IOCTL_VIDEO_MAP_VIDEO_MEMORY</p>
<p><strong>6:</strong>IOCTL_VIDEO_LOAD_AND_SET_FONT</p></td>
<td align="left"><p>該当する場合は、NT API の呼び出しからのステータス コード</p></td>
<td align="left"><p>ビデオの初期化に失敗しました。</p>
<p>このエラーは、Vga.sys を含むディスク (または別のビデオ ドライバーがコンピューターに適切な) が壊れているか、Microsoft Windows オペレーティング システムと通信できないビデオ ハードウェアを搭載する可能性があります。</p>
<p></p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x2</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>メモリ不足。</p>
<p></p></td>
</tr>
<tr class="even">
<td align="left"><p>0x3</p></td>
<td align="left"><p>正確なキーボードの初期化エラー:</p>
<p><strong>0:NtCreateFile</strong>の \device\KeyboardClass0 できませんでした。 (セットアップが見つかりませんでした、キーボードをコンピューターに接続します。)</p>
<p><strong>1:</strong>キーボード レイアウト DLL を読み込めません。 (セットアップを読み込めませんでしたキーボード レイアウト ファイルです。 このエラーを示します、CD またはフロッピー ディスクに、米国のリリースまたはローカライズされたリリース別のレイアウト DLL Kbdus.dll などのファイルがありません。)</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>キーボードの初期化に失敗しました。</p>
<p>このエラーは、キーボード ドライバー (I8042prt.sys または Kbdclass.sys) を含むディスクが破損しているか、搭載するキーボードのハードウェアを Windows と通信できないことに示している可能性があります。 このエラーも担当するキーボード レイアウトが DLL を読み込むことができませんでした。</p>
<p></p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x4</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>セットアップでは、デバイスをセットアップするの円弧のデバイス パス名は使用して起動は解決できませんでした。</p>
<p>このエラーは、セットアップの内部エラーです。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x5</p></td>
<td align="left"><p>予約済み</p></td>
<td align="left"><p>予約済み</p></td>
<td align="left"><p>サニティ チェックをパーティション分割できませんでした。</p>
<p>このエラーは、ディスク ドライバーにバグを示します。</p>
<p></p></td>
</tr>
</tbody>
</table>

 

 

 




