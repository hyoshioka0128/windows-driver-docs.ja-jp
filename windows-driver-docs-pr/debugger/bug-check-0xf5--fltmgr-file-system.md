---
title: Bug Check 0xF5 FLTMGR_FILE_SYSTEM
description: FLTMGR_FILE_SYSTEM のバグ チェックでは、0x000000F5 の値を持ちます。 これは、フィルター マネージャーで、回復不可能なエラーが発生したことを示します。
ms.assetid: 9b008c76-65c8-4de4-b7a0-96d8732c7b7e
keywords:
- Bug Check 0xF5 FLTMGR_FILE_SYSTEM
- FLTMGR_FILE_SYSTEM
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- FLTMGR_FILE_SYSTEM
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 81c2036fd621ffd6500429a7ce8bfb70ba4a0fa8
ms.sourcegitcommit: 55d7f63bb9e7668d65aa0999e65d18fabd44758e
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/08/2019
ms.locfileid: "59239563"
---
# <a name="bug-check-0xf5-fltmgrfilesystem"></a>バグ チェック 0xF5:FLTMGR\_ファイル\_システム


FLTMGR\_ファイル\_システムのバグ チェックが 0x000000F5 の値を持ちます。 これは、フィルター マネージャーで、回復不可能なエラーが発生したことを示します。

> [!IMPORTANT]
> このトピックはプログラマーを対象としています。 コンピューターを使用しているときに、エラー コードがブルー スクリーンが受信した顧客の場合を参照してください。[トラブルシューティング ブルー スクリーン エラー](https://windows.microsoft.com/windows-10/troubleshoot-blue-screen-errors)します。


## <a name="fltmgrfilesystem-parameters"></a>FLTMGR\_ファイル\_システム パラメーター


パラメーター 1 では、違反の種類を示します。 その他のパラメーターの意味は、パラメーター 1 の値によって異なります。

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
<th align="left">エラーの原因</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>0x66</p></td>
<td align="left"><p>操作のコールバックのデータ構造へのポインター。</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>ミニフィルター FLT_PREOP_SUCCESS_WITH_CALLBACK または FLT_PREOP_SYNCHRONIZE から preoperation コールバックが、対応する postoperation コールバックを登録しませんでした。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x67</p></td>
<td align="left"><p>操作のコールバックのデータ構造へのポインター。</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>操作のエラー NTSTATUS コード</p></td>
<td align="left"><p>内部オブジェクトが、領域不足になりましたが、システムが新しい領域を割り当てることができません。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x68</p></td>
<td align="left"><p>予約済み</p></td>
<td align="left"><p>FLT_FILE_NAME_INFORMATIONN 構造体のアドレス</p></td>
<td align="left"><p>予約済み</p></td>
<td align="left"><p>FLT_FILE_NAME_INFORMATION 構造体には、回数が多すぎますが逆参照します。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x6A</p></td>
<td align="left"><p>ファイルのファイル オブジェクト ポインター。</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>ファイルを開くか、ファイル作成要求をキャンセルできませんでした、ファイルの 1 つまたは複数のハンドルが作成されたためです。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x6B</p></td>
<td align="left"><p>フレーム ID</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>スレッド</p></td>
<td align="left"><p>BACKPOCKET IRPCTRL の状態が無効です。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x6C</p></td>
<td align="left"><p>フレーム ID</p></td>
<td align="left"><p>BackPocket 一覧</p></td>
<td align="left"><p>スレッド</p></td>
<td align="left"><p>BACKPOCKETED IRPCTR の入れ子になった PageFaults が多すぎます。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x6D</p></td>
<td align="left"><p>ミニフィルターのコンテキストの構造体のアドレス</p></td>
<td align="left"><p>CONTEXT_NODE 構造体のアドレス</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>Context 構造体には、回数が多すぎますが逆参照します。 これがまだ関連付けられているオブジェクトにアタッチされている間に、フィルター マネージャーの CONTEXT_NODE 構造の参照カウントが 0 にしたことを意味します。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x6E</p></td>
<td align="left"><p>ミニフィルターのコンテキストの構造体のアドレス</p></td>
<td align="left"><p>CONTEXT_NODE 構造体のアドレス</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>Context 構造は、解放された後に参照されました。</p></td>
</tr>
</tbody>
</table>

 

<a name="cause"></a>原因
-----

問題の原因は、パラメーター 1 の値によって示されます。 パラメーター セクションの表を参照してください。

<a name="resolution"></a>解決方法
----------

パラメーター 1 と等しい場合**0x66**、ミニフィルター ドライバーでこの操作の後の操作のコールバックが登録されていることを確認することでこの問題をデバッグすることができます。 コールバックのデータ構造では、現在の操作を確認できます。 (パラメーター 2 を参照してください)。使用して、 **! fltkd.cbd**デバッガー拡張機能。

パラメーター 1 と等しい場合**0x67**、ことがない、非ページ プールのリークどこかにシステムのことを確認する必要があります。

パラメーター 1 と等しい場合**0x6A**、ミニフィルター ドライバーがこのファイルを参照していないことを確認します (パラメーター 2 を参照してください) を任意の時点でこの操作のミニフィルターの処理中にハンドルを取得するオブジェクトします。

パラメーター 1 と等しい場合**0x6B**または**0x6C**、オペレーティング システムのバグ チェックが起こると、内部状態を回復できないエラーが発生しました。

パラメーター 1 と等しい場合**0x6D**、ミニフィルター ドライバーは呼び出さないことを確認**FltReleaseContext**指定されたコンテキストの回数が多すぎます (パラメーター 2 を参照してください)。

パラメーター 1 と等しい場合 0x6E、ミニフィルター ドライバーは呼び出しません確認**FltReferenceContext**指定されたコンテキストが削除された後 (パラメーター 2 を参照してください)。

 

 




