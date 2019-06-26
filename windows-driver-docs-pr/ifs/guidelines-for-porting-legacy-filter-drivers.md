---
title: レガシ フィルター ドライバーの移植ガイドライン
description: レガシ フィルター ドライバーの移植ガイドライン
ms.assetid: 6dd9637e-e9b3-4434-996c-c3f8ce6584c4
keywords:
- フィルター マネージャー WDK ファイル システム ミニフィルター、従来のドライバーの移植
- レガシ フィルター ドライバーの移植
- レガシ フィルター ドライバー WDK ファイル システム ミニフィルター
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c41fe9546f8aa784ef72a24c80f1c1efcd82ea9d
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67365894"
---
# <a name="guidelines-for-porting-legacy-filter-drivers"></a>レガシ フィルター ドライバーの移植ガイドライン


## <span id="ddk_when_the_filterunloadcallback_routine_is_called_if"></span><span id="DDK_WHEN_THE_FILTERUNLOADCALLBACK_ROUTINE_IS_CALLED_IF"></span>


開発者は、フィルター ドライバーの優れた機能を取得し、システムの信頼性を向上し、フィルター マネージャー モデルにポート レガシ フィルター ドライバーをお勧めします。 経験を積んだ開発者はずがポート ミニフィルター ドライバーにレガシ フィルター ドライバーを比較的簡単です。 マイクロソフトのフィルター ドライバー開発者は、次のアプローチをお勧めします。

-   レガシ フィルター ドライバーとインポート ミニフィルター ドライバーの動作を検証する信頼性の高い回帰テスト スイートを起動します。

-   ミニフィルター ドライバーのシェルを作成し、ミニフィルター ドライバーにレガシ フィルター ドライバーから機能を体系的に移動します。 たとえば、添付ファイルの作業を取得し、一度に 1 つの操作を各操作後にテストを移植します。

-   ミニフィルター ドライバーをテストする既存のツールを使用できるように、ユーザー モードまたはカーネル モードの通信を最後に、変更します。

-   PREfast を使用してコンパイルし、有効になっている Driver Verifier でフィルター Verifier I/O の確認オプションを使用してテストします。

移植の処理中には、フィルター マネージャーの機能を活用するためにすべてのレガシ フィルター ドライバーのコードを確認してください。 具体的には、次を注意に注意してください。

-   IRP ベースの I/O および高速な I/O 操作は取得できます、適切な場合は、同じ操作でのコードの重複の削減に役立つ。

-   操作のための登録時にミニフィルター ドライバーに明示的にすべての I/O のページングとキャッシュされた I/O は、これらをチェックするコードをする必要がなくなりますを無視する選択できます。

-   インスタンスの通知には、アタッチ/デタッチのロジックが大幅に簡略化します。

-   ミニフィルター ドライバーを処理する必要があります。 操作にのみ登録します。他のすべてを無視することができます。

-   フィルター マネージャーのコンテキストと名前の管理サポートを利用します。

-   非再帰的な I/O を発行するためのフィルター マネージャー サポートの活用します。

-   レガシ フィルター ドライバーとは異なり、ミニフィルター ドライバーは、preoperation postoperation 処理するために処理からコンテキストを維持するためにローカル変数を使用できません。 操作の状態を保存するルック アサイド リストの割り当てを検討してください。

-   名前またはコンテキストの使用が終わったらの参照を解放してください。

-   ユーザー モードで完了ポートは、キューを作成するための強力な手法を追加します。 ポートの名前を持つ単一への接続を 1 つのみを使用する必要があります。

次の表は、レガシ フィルター ドライバーと、フィルター マネージャー モデルへの割り当て方法の一般的な操作を一覧表示します。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">レガシ フィルター ドライバー モデル</th>
<th align="left">フィルター マネージャー モデル</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>パススルー操作完了ルーチンはありません。</p></td>
<td align="left"><p>ありません、ミニフィルター ドライバーは、この種類の I/O 操作の動作は、この操作の preoperation または postoperation コールバック ルーチンを登録しないでください。</p>
<p>この操作の preoperation コールバック ルーチンからそれ以外の場合、戻り値の FLT_PREOP_SUCCESS_NO_CALLBACK が登録されています。</p>
<p>参照してください<a href="returning-flt-preop-success-no-callback.md" data-raw-source="[Returning FLT_PREOP_SUCCESS_NO_CALLBACK](returning-flt-preop-success-no-callback.md)">FLT_PREOP_SUCCESS_NO_CALLBACK を返す</a>します。</p></td>
</tr>
<tr class="even">
<td align="left"><p>パススルー操作完了ルーチン</p></td>
<td align="left"><p>Preoperation コールバック ルーチンから FLT_PREOP_SUCCESS_WITH_CALLBACK を返します。</p>
<p>参照してください<a href="returning-flt-preop-success-with-callback.md" data-raw-source="[Returning FLT_PREOP_SUCCESS_WITH_CALLBACK](returning-flt-preop-success-with-callback.md)">FLT_PREOP_SUCCESS_WITH_CALLBACK を返す</a>します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>Preoperation コールバック ルーチン内の保留操作</p></td>
<td align="left"><p>呼び出す<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fltkernel/nf-fltkernel-fltlockuserbuffer" data-raw-source="[&lt;strong&gt;FltLockUserBuffer&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fltkernel/nf-fltkernel-fltlockuserbuffer)"> <strong>FltLockUserBuffer</strong> </a>ユーザー バッファーが ワーカー スレッドでアクセスできるように正しくロックされていることを確認するために必要とします。</p>
<p>呼び出すことによってワーカー スレッドに作業をキューのサポート ルーチン<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fltkernel/nf-fltkernel-fltallocatedeferredioworkitem" data-raw-source="[&lt;strong&gt;FltAllocateDeferredIoWorkItem&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fltkernel/nf-fltkernel-fltallocatedeferredioworkitem)"> <strong>FltAllocateDeferredIoWorkItem</strong> </a>と<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fltkernel/nf-fltkernel-fltqueuedeferredioworkitem" data-raw-source="[&lt;strong&gt;FltQueueDeferredIoWorkItem&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fltkernel/nf-fltkernel-fltqueuedeferredioworkitem)"> <strong>FltQueueDeferredIoWorkItem</strong> </a>.</p>
<p>Preoperation コールバック ルーチンから FLT_PREOP_PENDING を返します。</p>
<p>フィルター マネージャーに、I/O 操作を戻る準備が<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fltkernel/nf-fltkernel-fltcompletependedpreoperation" data-raw-source="[&lt;strong&gt;FltCompletePendedPreOperation&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fltkernel/nf-fltkernel-fltcompletependedpreoperation)"> <strong>FltCompletePendedPreOperation</strong></a>します。</p>
<p>参照してください<a href="pending-an-i-o-operation-in-a-preoperation-callback-routine.md" data-raw-source="[Pending an I/O Operation in a Preoperation Callback Routine](pending-an-i-o-operation-in-a-preoperation-callback-routine.md)">Preoperation コールバック ルーチン内の I/O 操作の保留中</a>します。</p></td>
</tr>
<tr class="even">
<td align="left"><p>Postoperation コールバック ルーチン内の保留操作</p></td>
<td align="left"><p>Preoperation コールバック ルーチンを呼び出して<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fltkernel/nf-fltkernel-fltlockuserbuffer" data-raw-source="[&lt;strong&gt;FltLockUserBuffer&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fltkernel/nf-fltkernel-fltlockuserbuffer)"> <strong>FltLockUserBuffer</strong> </a>そのユーザーを確実に正しくロックされているバッファーをワーカー スレッドでアクセスできるようにします。</p>
<p>呼び出すことによってワーカー スレッドに作業をキューのサポート ルーチン<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fltkernel/nf-fltkernel-fltallocategenericworkitem" data-raw-source="[&lt;strong&gt;FltAllocateGenericWorkItem&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fltkernel/nf-fltkernel-fltallocategenericworkitem)"> <strong>FltAllocateGenericWorkItem</strong> </a>と<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fltkernel/nf-fltkernel-fltqueuegenericworkitem" data-raw-source="[&lt;strong&gt;FltQueueGenericWorkItem&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fltkernel/nf-fltkernel-fltqueuegenericworkitem)"> <strong>FltQueueGenericWorkItem</strong> </a>.</p>
<p>Postoperation コールバック ルーチンから FLT_POSTOP_MORE_PROCESSING_REQUIRED を返します。</p>
<p>フィルター マネージャーに、I/O 操作を戻る準備が<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fltkernel/nf-fltkernel-fltcompletependedpostoperation" data-raw-source="[&lt;strong&gt;FltCompletePendedPostOperation&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fltkernel/nf-fltkernel-fltcompletependedpostoperation)"> <strong>FltCompletePendedPostOperation</strong></a>します。</p>
<p>参照してください<a href="pending-an-i-o-operation-in-a-postoperation-callback-routine.md" data-raw-source="[Pending an I/O Operation in a Postoperation Callback Routine](pending-an-i-o-operation-in-a-postoperation-callback-routine.md)">Postoperation コールバック ルーチン内の I/O 操作の保留中</a>します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>操作を同期します。</p></td>
<td align="left"><p>Preoperation コールバック ルーチンから FLT_PREOP_SYNCHRONIZE を返します。</p>
<p>参照してください<a href="returning-flt-preop-synchronize.md" data-raw-source="[Returning FLT_PREOP_SYNCHRONIZE](returning-flt-preop-synchronize.md)">FLT_PREOP_SYNCHRONIZE を返す</a>します。</p></td>
</tr>
<tr class="even">
<td align="left"><p>Preoperation コールバック ルーチンで操作を完了します。</p></td>
<td align="left"><p>最終的な操作の状態および情報の設定、 <strong>IoStatus</strong>のメンバー、 <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fltkernel/ns-fltkernel-_flt_callback_data" data-raw-source="[&lt;strong&gt;FLT_CALLBACK_DATA&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fltkernel/ns-fltkernel-_flt_callback_data)"> <strong>FLT_CALLBACK_DATA</strong> </a>操作の構造。</p>
<p>Preoperation コールバック ルーチンから FLT_PREOP_COMPLETE を返します。</p>
<p>参照してください<a href="completing-an-i-o-operation-in-a-preoperation-callback-routine.md" data-raw-source="[Completing an I/O Operation in a Preoperation Callback Routine](completing-an-i-o-operation-in-a-preoperation-callback-routine.md)">Preoperation コールバック ルーチン内の I/O 操作の完了</a>します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>Preoperation コールバック ルーチンを保留にされた後、操作を完了します。</p></td>
<td align="left"><p>最終的な操作の状態および情報の設定、 <strong>IoStatus</strong>のメンバー、 <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fltkernel/ns-fltkernel-_flt_callback_data" data-raw-source="[&lt;strong&gt;FLT_CALLBACK_DATA&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fltkernel/ns-fltkernel-_flt_callback_data)"> <strong>FLT_CALLBACK_DATA</strong> </a>操作の構造。</p>
<p>呼び出す<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fltkernel/nf-fltkernel-fltcompletependedpreoperation" data-raw-source="[&lt;strong&gt;FltCompletePendedPreOperation&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fltkernel/nf-fltkernel-fltcompletependedpreoperation)"> <strong>FltCompletePendedPreOperation</strong> </a>として FLT_PREOP_COMPLETE を渡して、I/O 操作を処理するワーカー スレッドから、 <em>CallbackStatus</em>パラメーター。</p>
<p>参照してください<a href="completing-an-i-o-operation-in-a-preoperation-callback-routine.md" data-raw-source="[Completing an I/O Operation in a Preoperation Callback Routine](completing-an-i-o-operation-in-a-preoperation-callback-routine.md)">Preoperation コールバック ルーチン内の I/O 操作の完了</a>します。</p></td>
</tr>
<tr class="even">
<td align="left"><p>すべての完了を行う完了ルーチンの動作</p></td>
<td align="left"><p>Postoperation コールバック ルーチンから FLT_POSTOP_FINISHED_PROCESSING を返します。</p>
<p>参照してください<a href="writing-postoperation-callback-routines.md" data-raw-source="[Writing Postoperation Callback Routines](writing-postoperation-callback-routines.md)">Postoperation コールバック ルーチンを記述</a>します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>安全な IRQL で作業を完了</p></td>
<td align="left"><p>呼び出す<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fltkernel/nf-fltkernel-fltdocompletionprocessingwhensafe" data-raw-source="[&lt;strong&gt;FltDoCompletionProcessingWhenSafe&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fltkernel/nf-fltkernel-fltdocompletionprocessingwhensafe)"> <strong>FltDoCompletionProcessingWhenSafe</strong> </a> postoperation コールバック ルーチンから。</p>
<p>参照してください<a href="ensuring-that-completion-processing-is-performed-at-safe-irql.md" data-raw-source="[Ensuring that Completion Processing is Performed at Safe IRQL](ensuring-that-completion-processing-is-performed-at-safe-irql.md)">完了処理が安全な IRQL で実行されることを確認</a>します。</p></td>
</tr>
<tr class="even">
<td align="left"><p>シグナル完了ルーチンからのイベント</p></td>
<td align="left"><p>この操作の preoperation コールバック ルーチンから FLT_PREOP_SYNCHRONIZE を返します。</p>
<p>フィルター マネージャーは、IRQL で preoperation コールバック ルーチンと同じスレッド コンテキストに postoperation コールバック ルーチンを呼び出す&lt;APC_LEVEL を = です。</p>
<p>参照してください<a href="returning-flt-preop-synchronize.md" data-raw-source="[Returning FLT_PREOP_SYNCHRONIZE](returning-flt-preop-synchronize.md)">FLT_PREOP_SYNCHRONIZE を返す</a>します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>失敗、成功した操作を作成します。</p></td>
<td align="left"><p>呼び出す<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fltkernel/nf-fltkernel-fltcancelfileopen" data-raw-source="[&lt;strong&gt;FltCancelFileOpen&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fltkernel/nf-fltkernel-fltcancelfileopen)"> <strong>FltCancelFileOpen</strong> </a>作成操作の postoperation コールバック ルーチンから。</p>
<p>適切なエラー NTSTATUS の値を設定、 <strong>IoStatus</strong>のメンバー、 <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fltkernel/ns-fltkernel-_flt_callback_data" data-raw-source="[&lt;strong&gt;FLT_CALLBACK_DATA&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fltkernel/ns-fltkernel-_flt_callback_data)"> <strong>FLT_CALLBACK_DATA</strong> </a>操作の構造。</p>
<p>FLT_POSTOP_FINISHED_PROCESSING を返します。</p>
<p>参照してください<a href="failing-an-i-o-operation-in-a-postoperation-callback-routine.md" data-raw-source="[Failing an I/O Operation in a Postoperation Callback Routine](failing-an-i-o-operation-in-a-postoperation-callback-routine.md)">Postoperation コールバック ルーチン内の I/O 操作が失敗した</a>します。</p></td>
</tr>
<tr class="even">
<td align="left"><p>I/O 操作の高速の I/O パスで I/O を禁止します。</p></td>
<td align="left"><p>操作の preoperation コールバック ルーチンから FLT_STATUS_DISALLOW_FAST_IO を返します。</p>
<p>参照してください<a href="disallowing-a-fast-i-o-operation-in-a-preoperation-callback-routine.md" data-raw-source="[Disallowing a Fast I/O Operation in a Preoperation Callback Routine](disallowing-a-fast-i-o-operation-in-a-preoperation-callback-routine.md)">Preoperation コールバック ルーチンで高速な I/O 操作を禁止する</a>します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>I/O 操作のパラメーターを修正します。</p></td>
<td align="left"><p>変更されたパラメーター値を設定、 <strong>Iopb</strong>のメンバー、 <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fltkernel/ns-fltkernel-_flt_callback_data" data-raw-source="[&lt;strong&gt;FLT_CALLBACK_DATA&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fltkernel/ns-fltkernel-_flt_callback_data)"> <strong>FLT_CALLBACK_DATA</strong> </a>操作の構造。</p>
<p>呼び出して FLT_CALLBACK_DATA 構造体をダーティとしてマーク<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fltkernel/nf-fltkernel-fltsetcallbackdatadirty" data-raw-source="[&lt;strong&gt;FltSetCallbackDataDirty&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fltkernel/nf-fltkernel-fltsetcallbackdatadirty)"> <strong>FltSetCallbackDataDirty</strong></a>の内容が変更されたときを除く、 <strong>IoStatus</strong> FLT_ のメンバーCALLBACK_DATA 構造体。</p>
<p>参照してください<a href="modifying-the-parameters-for-an-i-o-operation.md" data-raw-source="[Modifying the Parameters for an I/O Operation](modifying-the-parameters-for-an-i-o-operation.md)">I/O 操作のパラメーターを変更する</a>します。</p></td>
</tr>
<tr class="even">
<td align="left"><p>操作のユーザーのバッファーをロックします。</p></td>
<td align="left"><p>手法を使用し、で説明されているガイドライン<a href="accessing-the-user-buffers-for-an-i-o-operation.md" data-raw-source="[Accessing the User Buffers for an I/O Operation](accessing-the-user-buffers-for-an-i-o-operation.md)">、I/O 操作のユーザー バッファーへのアクセス</a>します。</p></td>
</tr>
</tbody>
</table>

 

 

 




