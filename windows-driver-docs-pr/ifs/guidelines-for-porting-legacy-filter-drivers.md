---
title: レガシ フィルター ドライバーの移植ガイドライン
description: レガシ フィルター ドライバーの移植ガイドライン
ms.assetid: 6dd9637e-e9b3-4434-996c-c3f8ce6584c4
keywords:
- フィルターマネージャー WDK ファイルシステムミニフィルター、レガシドライバーの移植
- レガシフィルタードライバーの移植
- レガシフィルタードライバー WDK ファイルシステムミニフィルター
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 647e80068c821c53c682a4815405641cd80011bc
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72841226"
---
# <a name="guidelines-for-porting-legacy-filter-drivers"></a>レガシ フィルター ドライバーの移植ガイドライン


## <span id="ddk_when_the_filterunloadcallback_routine_is_called_if"></span><span id="DDK_WHEN_THE_FILTERUNLOADCALLBACK_ROUTINE_IS_CALLED_IF"></span>


開発者は、フィルタードライバーの機能を強化し、システムの信頼性を向上させるために、従来のフィルタードライバーをフィルターマネージャーモデルに移植することをお勧めします。 経験豊富な開発者は、従来のフィルタードライバーをミニフィルタードライバーに移植するのは比較的簡単です。 Microsoft のフィルタードライバー開発者は、次の方法をお勧めします。

-   信頼性の高い回帰テストスイートから開始して、レガシフィルタードライバーと移植されたミニフィルタードライバーの動作を検証します。

-   ミニフィルタードライバーシェルを作成し、従来のフィルタードライバーからミニフィルタードライバーに機能を体系的に移動します。 たとえば、添付ファイルが動作していることを確認し、一度に1つの操作を移植して、各操作の後にテストします。

-   ユーザーモード/カーネルモードの通信が最後に変更されたので、既存のツールを使用してミニフィルタードライバーをテストすることができます。

-   PREfast を使用してコンパイルし、ドライバー検証ツールの [検証ツール i/o 検証] オプションを使用してテストします。

移植プロセスでは、フィルターマネージャーの機能を最大限に活用するために、すべてのレガシフィルタードライバーコードを確認する必要があります。 特に、次の点に注意してください。

-   IRP ベースの i/o および高速 i/o 操作は、必要に応じて同じ操作を行うことができます。これにより、コードの重複を減らすことができます。

-   操作に登録すると、ミニフィルタードライバーは、すべてのページング i/o とキャッシュされた i/o を無視するように明示的に選択できます。これにより、コードをチェックする必要がなくなります。

-   インスタンス通知は、アタッチ/デタッチロジックを大幅に簡素化します。

-   ミニフィルタードライバーで処理する必要がある操作に対してのみ登録します。他のすべてを無視できます。

-   フィルターマネージャーのコンテキストと名前管理のサポートを活用してください。

-   非再帰的 i/o を発行するためのフィルターマネージャーサポートを利用します。

-   レガシフィルタードライバーとは異なり、ミニフィルタードライバーはローカル変数に依存して、preoperation 処理から postoperation 処理までのコンテキストを維持することはできません。 操作状態を格納するには、ルックアサイドリストを割り当てることを検討してください。

-   名前またはコンテキストで終了した場合は、必ず参照を解放してください。

-   ユーザーモードの完了ポートは、キューを構築するための強力な手法を追加します。 1つの名前付きポートへの接続は1つしか必要ありません。

次の表に、レガシフィルタードライバーでの一般的な操作と、それらの操作をフィルターマネージャーモデルにマップする方法を示します。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">レガシフィルタードライバーモデル</th>
<th align="left">フィルターマネージャーモデル</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>完了ルーチンのないパススルー操作</p></td>
<td align="left"><p>ミニフィルタードライバーがこの種類の i/o 操作に対して機能しない場合は、この操作に対して preoperation または postoperation コールバックルーチンを登録しないでください。</p>
<p>それ以外の場合は、この操作に登録されている preoperation コールバックルーチンから FLT_PREOP_SUCCESS_NO_CALLBACK を返します。</p>
<p>「 <a href="returning-flt-preop-success-no-callback.md" data-raw-source="[Returning FLT_PREOP_SUCCESS_NO_CALLBACK](returning-flt-preop-success-no-callback.md)">FLT_PREOP_SUCCESS_NO_CALLBACK を返す</a>」を参照してください。</p></td>
</tr>
<tr class="even">
<td align="left"><p>完了ルーチンを使用したパススルー操作</p></td>
<td align="left"><p>Preoperation コールバックルーチンから FLT_PREOP_SUCCESS_WITH_CALLBACK を返します。</p>
<p>「 <a href="returning-flt-preop-success-with-callback.md" data-raw-source="[Returning FLT_PREOP_SUCCESS_WITH_CALLBACK](returning-flt-preop-success-with-callback.md)">FLT_PREOP_SUCCESS_WITH_CALLBACK を返す</a>」を参照してください。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>Preoperation コールバックルーチンでの保留操作</p></td>
<td align="left"><p>必要に応じて<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltlockuserbuffer" data-raw-source="[&lt;strong&gt;FltLockUserBuffer&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltlockuserbuffer)"><strong>FltLockUserBuffer</strong></a>を呼び出して、ワーカースレッドでアクセスできるように、すべてのユーザーバッファーが適切にロックされていることを確認します。</p>
<p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltallocatedeferredioworkitem" data-raw-source="[&lt;strong&gt;FltAllocateDeferredIoWorkItem&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltallocatedeferredioworkitem)"><strong>FltAllocateDeferredIoWorkItem</strong></a>や<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltqueuedeferredioworkitem" data-raw-source="[&lt;strong&gt;FltQueueDeferredIoWorkItem&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltqueuedeferredioworkitem)"><strong>FltQueueDeferredIoWorkItem</strong></a>などのサポートルーチンを呼び出してワーカースレッドに作業をキューに置いてください。</p>
<p>Preoperation コールバックルーチンから FLT_PREOP_PENDING を返します。</p>
<p>I/o 操作をフィルターマネージャーに返す準備ができたら、 <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltcompletependedpreoperation" data-raw-source="[&lt;strong&gt;FltCompletePendedPreOperation&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltcompletependedpreoperation)"><strong>Fltcompletependedpreoperation</strong></a>を呼び出します。</p>
<p>「<a href="pending-an-i-o-operation-in-a-preoperation-callback-routine.md" data-raw-source="[Pending an I/O Operation in a Preoperation Callback Routine](pending-an-i-o-operation-in-a-preoperation-callback-routine.md)">プリ操作コールバックルーチンでの I/o 操作の保留</a>」を参照してください。</p></td>
</tr>
<tr class="even">
<td align="left"><p>Postoperation コールバックルーチンでの保留操作</p></td>
<td align="left"><p>Preoperation コールバックルーチンで、 <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltlockuserbuffer" data-raw-source="[&lt;strong&gt;FltLockUserBuffer&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltlockuserbuffer)"><strong>FltLockUserBuffer</strong></a>を呼び出して、ワーカースレッドでアクセスできるように、ユーザーバッファーが適切にロックされていることを確認します。</p>
<p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltallocategenericworkitem" data-raw-source="[&lt;strong&gt;FltAllocateGenericWorkItem&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltallocategenericworkitem)"><strong>FltAllocateGenericWorkItem</strong></a>や<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltqueuegenericworkitem" data-raw-source="[&lt;strong&gt;FltQueueGenericWorkItem&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltqueuegenericworkitem)"><strong>Fltqueuegenericworkitem</strong></a>などのサポートルーチンを呼び出して、ワーカースレッドに作業をキューに置いてください。</p>
<p>Postoperation コールバックルーチンから FLT_POSTOP_MORE_PROCESSING_REQUIRED を返します。</p>
<p>I/o 操作をフィルターマネージャーに返す準備ができたら、 <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltcompletependedpostoperation" data-raw-source="[&lt;strong&gt;FltCompletePendedPostOperation&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltcompletependedpostoperation)"><strong>Fltcompletependedpostoperation</strong></a>を呼び出します。</p>
<p>「 <a href="pending-an-i-o-operation-in-a-postoperation-callback-routine.md" data-raw-source="[Pending an I/O Operation in a Postoperation Callback Routine](pending-an-i-o-operation-in-a-postoperation-callback-routine.md)">Postoperation コールバックルーチンでの I/o 操作の保留</a>」を参照してください。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>操作を同期する</p></td>
<td align="left"><p>Preoperation コールバックルーチンから FLT_PREOP_SYNCHRONIZE を返します。</p>
<p>「 <a href="returning-flt-preop-synchronize.md" data-raw-source="[Returning FLT_PREOP_SYNCHRONIZE](returning-flt-preop-synchronize.md)">FLT_PREOP_SYNCHRONIZE を返す</a>」を参照してください。</p></td>
</tr>
<tr class="even">
<td align="left"><p>Preoperation コールバックルーチンで操作を完了します。</p></td>
<td align="left"><p>操作の最後の操作の状態と、 <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/ns-fltkernel-_flt_callback_data" data-raw-source="[&lt;strong&gt;FLT_CALLBACK_DATA&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/ns-fltkernel-_flt_callback_data)"><strong>FLT_CALLBACK_DATA</strong></a>構造体の<strong>iostatus</strong>メンバーの情報を設定します。</p>
<p>Preoperation コールバックルーチンから FLT_PREOP_COMPLETE を返します。</p>
<p>「<a href="completing-an-i-o-operation-in-a-preoperation-callback-routine.md" data-raw-source="[Completing an I/O Operation in a Preoperation Callback Routine](completing-an-i-o-operation-in-a-preoperation-callback-routine.md)">プリ操作コールバックルーチンでの I/o 操作の完了</a>」を参照してください。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>Preoperation コールバックルーチンで保留された後に操作を完了します</p></td>
<td align="left"><p>操作の最後の操作の状態と、 <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/ns-fltkernel-_flt_callback_data" data-raw-source="[&lt;strong&gt;FLT_CALLBACK_DATA&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/ns-fltkernel-_flt_callback_data)"><strong>FLT_CALLBACK_DATA</strong></a>構造体の<strong>iostatus</strong>メンバーの情報を設定します。</p>
<p>I/o 操作を処理するワーカースレッドから<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltcompletependedpreoperation" data-raw-source="[&lt;strong&gt;FltCompletePendedPreOperation&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltcompletependedpreoperation)"><strong>FltcompleteFLT_PREOP_COMPLETE Dedpreoperation</strong></a>を呼び出し、コールアウト<em>状態</em>パラメーターとしてを渡します。</p>
<p>「<a href="completing-an-i-o-operation-in-a-preoperation-callback-routine.md" data-raw-source="[Completing an I/O Operation in a Preoperation Callback Routine](completing-an-i-o-operation-in-a-preoperation-callback-routine.md)">プリ操作コールバックルーチンでの I/o 操作の完了</a>」を参照してください。</p></td>
</tr>
<tr class="even">
<td align="left"><p>完了ルーチンですべての完了作業を実行します</p></td>
<td align="left"><p>Postoperation コールバックルーチンから FLT_POSTOP_FINISHED_PROCESSING を返します。</p>
<p>「 <a href="writing-postoperation-callback-routines.md" data-raw-source="[Writing Postoperation Callback Routines](writing-postoperation-callback-routines.md)">Postoperation コールバックルーチンの記述</a>」を参照してください。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>安全な IRQL での作業の完了</p></td>
<td align="left"><p>Postoperation コールバックルーチンから<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltdocompletionprocessingwhensafe" data-raw-source="[&lt;strong&gt;FltDoCompletionProcessingWhenSafe&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltdocompletionprocessingwhensafe)"><strong>Fltdoの Processingwhensafe</strong></a>を呼び出します。</p>
<p>「<a href="ensuring-that-completion-processing-is-performed-at-safe-irql.md" data-raw-source="[Ensuring that Completion Processing is Performed at Safe IRQL](ensuring-that-completion-processing-is-performed-at-safe-irql.md)">完了処理が安全な IRQL で実行されるようにする」を</a>参照してください。</p></td>
</tr>
<tr class="even">
<td align="left"><p>完了ルーチンからイベントを通知します</p></td>
<td align="left"><p>この操作の preoperation コールバックルーチンから FLT_PREOP_SYNCHRONIZE を返します。</p>
<p>フィルターマネージャーは、IRQL &lt;= APC_LEVEL で、preoperation コールバックルーチンと同じスレッドコンテキストで postoperation コールバックルーチンを呼び出します。</p>
<p>「 <a href="returning-flt-preop-synchronize.md" data-raw-source="[Returning FLT_PREOP_SYNCHRONIZE](returning-flt-preop-synchronize.md)">FLT_PREOP_SYNCHRONIZE を返す</a>」を参照してください。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>成功した作成操作の失敗</p></td>
<td align="left"><p>作成操作の postoperation コールバックルーチンから<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltcancelfileopen" data-raw-source="[&lt;strong&gt;FltCancelFileOpen&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltcancelfileopen)"><strong>Fltcancelfileopen</strong></a>を呼び出します。</p>
<p>操作の<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/ns-fltkernel-_flt_callback_data" data-raw-source="[&lt;strong&gt;FLT_CALLBACK_DATA&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/ns-fltkernel-_flt_callback_data)"><strong>FLT_CALLBACK_DATA</strong></a>構造体の<strong>iostatus</strong>メンバーに、適切なエラー NTSTATUS 値を設定します。</p>
<p>FLT_POSTOP_FINISHED_PROCESSING を返します。</p>
<p>「 <a href="failing-an-i-o-operation-in-a-postoperation-callback-routine.md" data-raw-source="[Failing an I/O Operation in a Postoperation Callback Routine](failing-an-i-o-operation-in-a-postoperation-callback-routine.md)">Postoperation コールバックルーチンでの I/o 操作の失敗</a>」を参照してください。</p></td>
</tr>
<tr class="even">
<td align="left"><p>I/o 操作の高速 i/o パスを介して i/o を禁止する</p></td>
<td align="left"><p>操作の preoperation コールバックルーチンから FLT_STATUS_DISALLOW_FAST_IO を返します。</p>
<p>「<a href="disallowing-a-fast-i-o-operation-in-a-preoperation-callback-routine.md" data-raw-source="[Disallowing a Fast I/O Operation in a Preoperation Callback Routine](disallowing-a-fast-i-o-operation-in-a-preoperation-callback-routine.md)">事前操作コールバックルーチンでの高速 I/o 操作の禁止</a>」を参照してください。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>I/o 操作のパラメーターを変更する</p></td>
<td align="left"><p>操作の<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/ns-fltkernel-_flt_callback_data" data-raw-source="[&lt;strong&gt;FLT_CALLBACK_DATA&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/ns-fltkernel-_flt_callback_data)"><strong>FLT_CALLBACK_DATA</strong></a>構造体の<strong>Iopb</strong>メンバーの変更されたパラメーター値を設定します。</p>
<p>FLT_CALLBACK_DATA 構造体の<strong>Iostatus</strong>メンバーの内容を変更した場合を除き、 <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltsetcallbackdatadirty" data-raw-source="[&lt;strong&gt;FltSetCallbackDataDirty&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltsetcallbackdatadirty)"><strong>FltSetCallbackDataDirty</strong></a>を呼び出して、FLT_CALLBACK_DATA 構造をダーティとしてマークします。</p>
<p>「 <a href="modifying-the-parameters-for-an-i-o-operation.md" data-raw-source="[Modifying the Parameters for an I/O Operation](modifying-the-parameters-for-an-i-o-operation.md)">I/o 操作のパラメーターの変更」を</a>参照してください。</p></td>
</tr>
<tr class="even">
<td align="left"><p>操作のユーザーバッファーをロックします</p></td>
<td align="left"><p>「 <a href="accessing-the-user-buffers-for-an-i-o-operation.md" data-raw-source="[Accessing the User Buffers for an I/O Operation](accessing-the-user-buffers-for-an-i-o-operation.md)">I/o 操作のユーザーバッファーへのアクセス</a>」で説明されている手法とガイドラインを使用します。</p></td>
</tr>
</tbody>
</table>

 

 

 




