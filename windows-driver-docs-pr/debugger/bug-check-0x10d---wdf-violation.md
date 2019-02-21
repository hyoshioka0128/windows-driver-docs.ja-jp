---
title: バグ チェック 0x10D WDF_VIOLATION
description: WDF_VIOLATION のバグ チェックでは、0x0000010D の値を持ちます。 これは、カーネル モード ドライバー フレームワーク (KMDF) には Windows では、framework ベースのドライバーにエラーが見つかりましたが検出されたことを示します。
ms.assetid: 2d8c9730-cd24-4f8c-8f8b-252644737847
keywords:
- バグ チェック 0x10D WDF_VIOLATION
- WDF_VIOLATION
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- WDF_VIOLATION
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 066ed6ba5e877d51fde3db7c84820e52b87a0f47
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56529513"
---
# <a name="bug-check-0x10d-wdfviolation"></a>バグ チェック 0x10D の。WDF\_違反


WDF\_違反のバグ チェックが 0x0000010D の値を持ちます。 これは、カーネル モード ドライバー フレームワーク (KMDF) には Windows では、framework ベースのドライバーにエラーが見つかりましたが検出されたことを示します。

**重要な**プログラマ向けのトピックです。 コンピューターを使用しているときに、エラー コードがブルー スクリーンが受信した顧客の場合を参照してください。[トラブルシューティング ブルー スクリーン エラー](https://windows.microsoft.com/windows-10/troubleshoot-blue-screen-errors)します。

## <a name="wdfviolation-parameters"></a>WDF\_違反パラメーター


パラメーター 1 では、特定のエラー コードのバグ チェックを示します。 パラメーター 4 が予約されています。

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
<th align="left">エラーの原因</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>0x1</p></td>
<td align="left"><p>WDF_POWER_ROUTINE_TIMED_OUT_DATA 構造へのポインター</p></td>
<td align="left"><p>予約済み</p></td>
<td align="left"><p>フレームワーク ベースのドライバーは、電源操作中にタイムアウトしました。 これは通常、デバイス スタック DO_POWER_PAGABLE ビットを設定していないと、ドライバーは、ページング デバイス スタックの電源を切断した後、ページング可能な操作を実行しようとことに意味します。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x2</p></td>
<td align="left"><p>予約済み</p></td>
<td align="left"><p>予約済み</p></td>
<td align="left"><p>現在保持されているロックの取得が試行されています。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x3</p></td>
<td align="left"><p>WDFREQUEST ハンドル</p></td>
<td align="left"><p>両方のバッファーに残っている未処理の参照の数</p></td>
<td align="left"><p>Windows Driver Framework Verifier 致命的なエラーが発生しました。 具体的には、I/O 要求を完了しましたが、入力バッファー、出力バッファー、またはその両方に未解決の参照があるために、フレームワークの要求オブジェクトを削除できません。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x4</p></td>
<td align="left"><p>予約済み</p></td>
<td align="left"><p>呼び出し元&#39;s アドレス</p></td>
<td align="left"><p>A <strong>NULL</strong>以外に必要な関数に渡されたパラメーター<strong>NULL</strong>値。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x5</p></td>
<td align="left"><p>渡されたハンドルの値</p></td>
<td align="left"><p>予約済み</p></td>
<td align="left"><p>Framework のオブジェクト メソッドの型が正しくない framework オブジェクトのハンドルが渡されました。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x6</p></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"><p>次の表を参照してください。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x7</p></td>
<td align="left"><p>Framework のオブジェクトのハンドル</p></td>
<td align="left"><p>予約済み</p></td>
<td align="left"><p>呼び出していない framework オブジェクトを正しく削除しようとしているドライバー <strong>WdfObjectDereference</strong>呼び出す代わりにハンドルを削除する<strong>WdfObjectDelete</strong>します。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x8</p></td>
<td align="left"><p>DMA のトランザクション オブジェクトのハンドル</p></td>
<td align="left"><p>予約済み</p></td>
<td align="left"><p>適切な状態でなかったときに、DMA トランザクション オブジェクトの操作が発生しました。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x9</p></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"><p>現在使用されていません。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0 xa</p></td>
<td align="left"><p>WDF_QUEUE_FATAL_ERROR_DATA 構造体へのポインター</p></td>
<td align="left"><p>予約済み</p></td>
<td align="left"><p>致命的なエラーが、現在キュー内にある要求の処理中に発生しました。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0 xb</p></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"><p>次の表を参照してください。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0 xc</p></td>
<td align="left"><p>WDFDEVICE ハンドル</p></td>
<td align="left"><p>新しい PnP IRP へのポインター</p></td>
<td align="left"><p>PnP IRP の状態を変更して別のドライバーが処理中に、新しい状態を変更の PnP IRP が到着します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0 xd</p></td>
<td align="left"><p>WDFDEVICE ハンドル</p></td>
<td align="left"><p>電源 IRP へのポインター</p></td>
<td align="left"><p>デバイス&#39;電源ポリシー所有者は電源要求しなかった IRP を受信します。 複数の電源ポリシーの所有者である可能性がありますが、1 つだけが許可されています。 KMDF ドライバーは、呼び出すことによって電源ポリシーの所有権を変更できる<strong>WdfDeviceInitSetPowerPolicyOwnership</strong>します。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0xE</p></td>
<td align="left"><p>IRQL はイベント コールバック関数を呼び出しました。</p></td>
<td align="left"><p>IRQL はイベント コールバック関数が返されます。</p></td>
<td align="left"><p>イベントのコールバック関数が呼び出された同じ IRQL で返されませんでした。 コールバック関数の IRQL 直接的または間接的に (たとえば、によって変更 DISPATCH_LEVEL の IRQL を発生させるには、スピン ロックの取得がスピンロックを解放していない)。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0 xf です.</p></td>
<td align="left"><p>イベントのコールバック関数のアドレス。</p></td>
<td align="left"><p>予約済み</p></td>
<td align="left"><p>イベントのコールバック関数がクリティカル領域では、入力したが、返す前に重要な領域が出ない。</p></td>
</tr>
</tbody>
</table>

 

**パラメーター 1 が 0x6 に等しい**

パラメーター 1 が 0x6 と等しい場合は、致命的なエラーは、WDF の要求を処理することで行われました。 この場合、パラメーター 2 でさらにが行われた、致命的なエラーの種類を指定の WDF 列挙体によって定義されている\_要求\_FATAL\_エラー。

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">パラメータ 2</th>
<th align="left">3 番目のパラメーター</th>
<th align="left">エラーの原因</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>0x1</p></td>
<td align="left"><p>IRP のアドレス</p></td>
<td align="left"><p>複数の I/O スタック場所がありません基になる IRP を書式設定を利用できます。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x2</p></td>
<td align="left"><p>WDF 要求ハンドル値</p></td>
<td align="left"><p>IRP を含まない framework 要求オブジェクトの書式を設定しようとしました。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x3</p></td>
<td align="left"><p>WDF 要求ハンドル値</p></td>
<td align="left"><p>ドライバーは、I/O のターゲットに既に送信されているフレームワークの要求を送信しようとしました。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x4</p></td>
<td align="left"><p>IRP、WDF 要求ハンドルの値、IRP の主な機能、およびバイト数へのポインターを格納する WDR_REQUEST_FATAL_ERROR_INFORMATION_LENGTH_MISMATCH_DATA 構造体へのポインターが、記述しようとしています。</p></td>
<td align="left"><p>ドライバーでは、フレームワークの要求が完了したが、IRP で指定された数よりは、出力バッファーにバイトが書き込まれます。</p></td>
</tr>
</tbody>
</table>

 

**パラメーター 1 が 0 xb に等しい**

パラメーター 1 が 0 xb と等しい場合は、取得するか、ロックを解放しようには、無効です。 この場合、パラメーター 3 にさらには、エラーになっているを指定します。

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">パラメータ 2</th>
<th align="left">3 番目のパラメーター</th>
<th align="left">エラーの原因</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>ハンドル値</p></td>
<td align="left"><p>0x0</p></td>
<td align="left"><p>渡されるハンドルを<strong>WdfObjectAcquireLock</strong>または<strong>WdfObjectReleaseLock</strong>同期ロックをサポートしていないオブジェクトを表します。</p></td>
</tr>
<tr class="even">
<td align="left"><p>WDF のスピン ロック ハンドル</p></td>
<td align="left"><p>0x1</p></td>
<td align="left"><p>スピン ロックを取得しなかったスレッドによって解放します。</p></td>
</tr>
</tbody>
</table>

 

<a name="cause"></a>原因
-----

原因の詳細については、パラメーター セクション内の各コードの説明を参照してください。

<a name="resolution"></a>解決方法
----------

[ **! 分析**](-analyze.md)バグ チェックに関する情報を表示拡張機能をデバッグおよびはエラー コード モジュールなどの情報を収集するときに非常に役に立ちます。

通常、WDF のダンプ ファイルが生成されますさらに、このバグ チェックの原因となったドライバーに関する情報。 このコマンドを使用して、ログ ファイルを確認します。

```dbgcmd
kd> !wdfkd.wdflogdump <WDF_Driver_Name>
```

パラメーター 1 と等しい場合**0x2**、問題のロックを判断する、呼び出し元のスタックを確認します。

パラメーター 1 と等しい場合**0x3**ドライバーのカーネル モード ドライバー フレームワークのエラー ログの詳細については、未解決の参照が含まれます。

パラメーター 1 と等しい場合**0x4**を使用して、 [ **ln デバッガー** ](ln--list-nearest-symbols-.md)コマンドの値と*パラメーター 3*判断するために、引数として関数に必要な以外**NULL**パラメーター。

パラメーター 1 と等しい場合**0x7**を使用して、**! wdfkd.wdfhandle***Parameter 2*ハンドルの種類を決定する拡張機能コマンド。

パラメーター 1 と等しい場合**0 xa**、WDF し\_キュー\_FATAL\_エラー\_データ構造は、問題のある要求またはキュー ハンドルのいずれかを示します。 NTSTATUS、場合なく状態も示されます\_成功すると、使用可能な場合。

 

 




