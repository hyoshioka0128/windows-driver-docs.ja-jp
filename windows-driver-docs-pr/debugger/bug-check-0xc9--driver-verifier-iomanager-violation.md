---
title: バグ チェック 0xC9 DRIVER_VERIFIER_IOMANAGER_VIOLATION
description: DRIVER_VERIFIER_IOMANAGER_VIOLATION のバグ チェックでは、0x000000C9 の値を持ちます。 これは、すべてのドライバー検証ツールの I/O の検証違反のバグ チェック コードです。
ms.assetid: dcafb0df-cbc1-44f4-8ec4-976df0842f0c
keywords:
- バグ チェック 0xC9 DRIVER_VERIFIER_IOMANAGER_VIOLATION
- DRIVER_VERIFIER_IOMANAGER_VIOLATION
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- DRIVER_VERIFIER_IOMANAGER_VIOLATION
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: fec71d67eabeb87eb9c13f860be93e28ec95a6c8
ms.sourcegitcommit: b3859d56cb393e698c698d3fb13519ff1522c7f3
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/05/2019
ms.locfileid: "57350427"
---
# <a name="bug-check-0xc9-driververifieriomanagerviolation"></a>バグ チェック 0xC9:ドライバー\_VERIFIER\_IOMANAGER\_違反


ドライバー\_VERIFIER\_IOMANAGER\_違反のバグ チェックが 0x000000C9 の値を持ちます。 これは、すべての Driver Verifier のバグ チェック コード**I/O の検証**違反。

**重要な**プログラマ向けのトピックです。 コンピューターを使用しているときに、エラー コードがブルー スクリーンが受信した顧客の場合を参照してください。[トラブルシューティング ブルー スクリーン エラー](https://windows.microsoft.com/windows-10/troubleshoot-blue-screen-errors)します。

## <a name="driververifieriomanagerviolation-parameters"></a>ドライバー\_VERIFIER\_IOMANAGER\_違反パラメーター


ドライバーの検証ツールがアクティブの場合と**I/O の検証**は選択すると、さまざまな I/O 違反により発行される場合は、このバグ チェックします。 パラメーター 1 では、違反の種類を識別します。

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
<td align="left"><p>0x01</p></td>
<td align="left"><p>解放される IRP のアドレス</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>ドライバーは、その型を持つ IO_TYPE_IRP でないオブジェクトを解放しようとしました。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x02</p></td>
<td align="left"><p>解放される IRP のアドレス</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>ドライバーが IRP がスレッドに関連付けられているを解放しようとするとします。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x03</p></td>
<td align="left"><p>送信される IRP のアドレス</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>ドライバーに渡される<strong>保留</strong>IRP の種類が IRP_TYPE 等しくありません。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x04</p></td>
<td align="left"><p>デバイス オブジェクトのアドレス</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>ドライバーに渡される<strong>保留</strong>デバイスの無効なオブジェクト。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x05</p></td>
<td align="left"><p>関連付けられた問題のあるデバイス オブジェクトのアドレス ドライバー</p></td>
<td align="left"><p>前に、の IRQL<strong>保留</strong></p></td>
<td align="left"><p>後の IRQL<strong>保留</strong></p></td>
<td align="left"><p>IRQL は、ドライバーのディスパッチ ルーチンの呼び出し中に変更します。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x06</p></td>
<td align="left"><p>IRP の状態</p></td>
<td align="left"><p>IRP の完了のアドレス</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>ドライバーと呼ばれる<strong>IoCompleteRequest</strong>状態と保留中 (または-1) をマークします。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x07</p></td>
<td align="left"><p>キャンセル ルーチンのアドレス</p></td>
<td align="left"><p>IRP の完了のアドレス</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>ドライバーと呼ばれる<strong>IoCompleteRequest</strong>設定された、キャンセル ルーチン中にします。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x08</p></td>
<td align="left"><p>デバイス オブジェクトのアドレス</p></td>
<td align="left"><p>IRP の主要な関数のコード</p></td>
<td align="left"><p>例外の状態コード</p></td>
<td align="left"><p>ドライバーに渡される<strong>IoBuildAsynchronousFsdRequest</strong>バッファーが無効です。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x09</p></td>
<td align="left"><p>デバイス オブジェクトのアドレス</p></td>
<td align="left"><p>I/O 制御コード</p></td>
<td align="left"><p>例外の状態コード</p></td>
<td align="left"><p>ドライバーに渡される<strong>IoBuildDeviceIoControlRequest</strong>バッファーが無効です。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x10</p></td>
<td align="left"><p>現在の IRQL</p></td>
<td align="left"><p>予約済み</p></td>
<td align="left"><p>予約済み</p></td>
<td align="left"><p>保留は、DISPATCH_LEVEL 上が呼び出されました。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x11</p></td>
<td align="left"><p>ドライバーの高速な I/O ディスパッチの日常的なアドレス</p></td>
<td align="left"><p>IRQL ドライバー ディスパッチ ルーチンを呼び出す前に</p></td>
<td align="left"><p>現在の IRQL</p></td>
<td align="left"><p>保留は、DISPATCH_LEVEL 上が呼び出されました。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x12</p></td>
<td align="left"><p>ドライバーのディスパッチ ルーチンのアドレス</p></td>
<td align="left"><p>IRQL ドライバー ディスパッチ ルーチンを呼び出す前に</p></td>
<td align="left"><p>現在の IRQL</p></td>
<td align="left"><p>保留は、DISPATCH_LEVEL 上が呼び出されました。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x0A</p></td>
<td align="left"><p>デバイス オブジェクトのアドレス</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>ドライバーに渡される<strong>IoInitializeTimer</strong>既に初期化されているタイマーを使用して、デバイス オブジェクト。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x0C</p></td>
<td align="left"><p>状態の I/O ブロックのアドレス</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>ドライバーが IRP に、I/O の状態のブロックを渡されるが、このブロックがその時点より後にアンワインドが既にスタックに割り当てられます。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x0D</p></td>
<td align="left"><p>ユーザー イベント オブジェクトのアドレス</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>このイベントは、その時点より後にアンワインドが既にスタックに割り当てられますが、ドライバーは IRP をユーザー イベントを渡されました。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x0E</p></td>
<td align="left"><p>現在の IRQL</p></td>
<td align="left"><p>IRP のアドレス</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>ドライバーと呼ばれる<strong>IoCompleteRequest</strong> IRQL で&gt;DISPATCH_LEVEL します。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x0F</p></td>
<td align="left"><p>IRP が送信されて、デバイス オブジェクトのアドレス</p></td>
<td align="left"><p>IRP へのポインター</p></td>
<td align="left"><p>ファイル オブジェクトへのポインター</p></td>
<td align="left"><p>ドライバーには、ファイルのオブジェクトで問題が閉じられて、または取り消された、開く必要があったと作成要求が送信されます。</p></td>
</tr>
</tbody>
</table>

 

数があるだけでなく、前の表に記載されたエラー、 **I/O の検証**Driver Verifier システムを停止する原因となるが、実際にはバグ チェックされていないエラーです。

これらのエラーでは、クラッシュ ダンプ ファイル、およびカーネル デバッガーは、ブルー スクリーンに表示するメッセージがあります。 これらのメッセージは、それぞれの場所に異なる方法で表示されます。 16 進数のバグ チェック コード 0xC9 とバグがドライバーの文字列をチェックするこれらのエラーが発生すると、\_VERIFIER\_IOMANAGER\_違反または表示されませんブルー スクリーンに、デバッガーでは、クラッシュ ダンプ ファイルに表示されます.

青の画面では、次のデータが表示されます。

-   メッセージ**IO システム検証エラー**します。

-   メッセージ**WDM ドライバー エラー** *XXX*ここで、 *XXX*は特定のエラーを表す 16 進数コードです。 (詳しくは、I/O エラー コードとその意味の一覧については、次の表を参照してください)。

-   エラーを発生させたドライバーの名前。

-   エラーの場所は、ドライバーのコード内のアドレスには、(パラメーター 2) が検出されました。

-   IRP (パラメーター 3) へのポインター。

-   デバイス オブジェクト (パラメーター 4) へのポインター。

カーネル モードのクラッシュ ダンプが有効の場合、クラッシュ ダンプ ファイルに次の情報が表示されます。

-   メッセージ**バグチェック 0xC9 (ドライバー\_VERIFIER\_IOMANAGER\_違反)** します。

-   16 進数の I/O エラー コード。 (詳しくは、I/O エラー コードとその意味の一覧については、次の表を参照してください)。

-   エラーが検出されたドライバーのコード内のアドレス。

-   IRP へのポインター。

-   デバイス オブジェクトへのポインター。

カーネル デバッガーがこの違反が発生しました、システムに接続されている場合、次の情報は、デバッガーに送信されます。

-   メッセージ**WDM ドライバー エラー**、と共に、エラーの重大度を評価します。

-   エラーを発生させたドライバーの名前。

-   このエラーの原因を説明するわかりやすい文字列。 多くの場合、追加の情報は、IRP へのポインターなど、渡されます。 (これらのわかりやすい文字列とどのような追加情報は、指定の一覧については、次の表を参照してください)。

-   さらにアクションに対するクエリ。 可能な応答は**b** (中断)**は**(無視) **z** (zap) **r** (削除)、または**d** (無効)。 オペレーティング システムを継続的に指示を使用すると、何が起こる"line"ダウンこのエラーが発生していない場合を参照してください。 もちろん、この多くの場合、により、追加のバグ チェックされます。 "Zap"オプションは、検出するには、このエラーの原因となったブレークポイントを実際に削除されます。

**注**  この方法では無視できるその他のバグはチェックを行わない。 このようなの**I/O の検証**エラーを無視してもこれらのエラーは、カーネル デバッガーがアタッチされている場合にのみ無視されます。

 

次の表に一覧された**I/O の検証**エラーを表示できます。

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">I/O エラー コード</th>
<th align="left">重大度</th>
<th align="left">エラーの原因</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>0x200</p></td>
<td align="left"><p>Unknown</p></td>
<td align="left"><p>このコードはすべての不明な<strong>I/O の検証</strong>エラー。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x201</p></td>
<td align="left"><p>致命的なエラー</p></td>
<td align="left"><p>ドライバー スタックの下にある別のデバイスがデバイスの削除自体自動的にしています。 呼び出し元が呼び出しを忘れた可能性があります<strong>IoDetachDevice</strong>優先、または下位のドライバーが不適切に削除自体。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x202</p></td>
<td align="left"><p>致命的なエラー</p></td>
<td align="left"><p>ドライバーは、どこにもアタッチされていないデバイス オブジェクトからデタッチしようとしました。 これは、場合に発生デタッチが同じデバイス オブジェクトを 2 回呼び出されました。 (デバイス オブジェクトを指定します。)</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x203</p></td>
<td align="left"><p>致命的なエラー</p></td>
<td align="left"><p>ドライバーが呼び出されて<strong>保留</strong>IRP をキャンセル ルーチンを設定せず<strong>NULL</strong>します。 (IRP を指定します。)</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x204</p></td>
<td align="left"><p>致命的なエラー</p></td>
<td align="left"><p>呼び出し元が渡されて<strong>NULL</strong>デバイス オブジェクトとして。 これは致命的です。 (IRP を指定します。)</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x205</p></td>
<td align="left"><p>致命的なエラー</p></td>
<td align="left"><p>呼び出し元には、その下にあるキューに現在ある IRP が転送します。 このドライバーで STATUS_PENDING を返す Irp を処理するコードは、破損が表示されます。 (IRP を指定します。)</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x206</p></td>
<td align="left"><p>致命的なエラー</p></td>
<td align="left"><p>呼び出し元が正しく転送しない IRP (コントロールのフィールドをゼロに設定されません)。 ドライバーを使用する必要があります<strong>IoCopyCurrentIrpStackLocationToNext</strong>または<strong>IoSkipCurrentIrpStackLocation</strong>します。 (IRP を指定します。)</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x207</p></td>
<td align="left"><p>致命的なエラー</p></td>
<td align="left"><p>呼び出し元は、スタックが手動でコピーし、上位層の完了ルーチンのコピーが誤ってします。 ドライバーを使用する必要があります<strong>IoCopyCurrentIrpStackLocationToNext</strong>します。 (IRP を指定します。)</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x208</p></td>
<td align="left"><p>致命的なエラー</p></td>
<td align="left"><p>この IRP では、スタックの場所から実行しようとしています。 別のスタックからこの IRP を転送だれかが可能性があります。 (IRP を指定します。)</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x209</p></td>
<td align="left"><p>致命的なエラー</p></td>
<td align="left"><p>呼び出し元は、その下にある現在キューに配置する IRP を完了しています。 このドライバーで STATUS_PENDING を返す Irp を処理するコードは、破損が表示されます。 (IRP を指定します。)</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x20A</p></td>
<td align="left"><p>致命的なエラー</p></td>
<td align="left"><p>呼び出し元<strong>IoFreeIrp</strong>使用中である IRP を解放します。 (元 IRP および IRP を使用して指定します。)</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x20B</p></td>
<td align="left"><p>致命的なエラー</p></td>
<td align="left"><p>呼び出し元<strong>IoFreeIrp</strong>使用中である IRP を解放します。 (IRP を指定します。)</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x20C</p></td>
<td align="left"><p>致命的なエラー</p></td>
<td align="left"><p>呼び出し元<strong>IoFreeIrp</strong>スレッドに対してはまだキューに配置する IRP を解放します。 (IRP を指定します。)</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x20D</p></td>
<td align="left"><p>致命的なエラー</p></td>
<td align="left"><p>呼び出し元<strong>IoInitializeIrp</strong>で割り当てられた IRP が渡される<strong>IoAllocateIrp</strong>します。 これは無効なと、不要なとクォータのリークが発生しました。 マニュアルを参照<strong>IoReuseIrp</strong>この IRP がリサイクルされている場合。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x20E</p></td>
<td align="left"><p>致命的でないエラー</p></td>
<td align="left"><p>PNP IRP が無効な状態です。 (任意の PNP IRP が必要 STATUS_NOT_SUPPORTED に初期化された状態です。)(IRP を指定します。)</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x20F</p></td>
<td align="left"><p>致命的でないエラー</p></td>
<td align="left"><p>電源 IRP が無効な状態です。 (任意の Power IRP が必要 STATUS_NOT_SUPPORTED に初期化された状態です。)(IRP を指定します。)</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x210</p></td>
<td align="left"><p>致命的でないエラー</p></td>
<td align="left"><p>WMI の IRP では、無効な状態があります。 (任意の WMI IRP が必要 STATUS_NOT_SUPPORTED に初期化された状態です。)(IRP を指定します。)</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x211</p></td>
<td align="left"><p>致命的でないエラー</p></td>
<td align="left"><p>呼び出し元には、スタック内のデバイス オブジェクトをスキップ中に IRP が転送されます。 呼び出し元がおそらく Irp をによって返されるデバイスの代わりに、PDO 送信<strong>IoAttachDeviceToDeviceStack</strong>します。 (IRP を指定します。)</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x212</p></td>
<td align="left"><p>致命的でないエラー</p></td>
<td align="left"><p>呼び出し元は、ごみ箱に入れがまたはの IRP スタックが正しくコピーされていません。 (IRP を指定します。)</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x213</p></td>
<td align="left"><p>致命的でないエラー</p></td>
<td align="left"><p>呼び出し元が認識しない IRP のステータス フィールドが変更されました。 (IRP を指定します。)</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x214</p></td>
<td align="left"><p>致命的でないエラー</p></td>
<td align="left"><p>呼び出し元が認識しない IRP の情報フィールドが変更されました。 (IRP を指定します。)</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x215</p></td>
<td align="left"><p>致命的でないエラー</p></td>
<td align="left"><p>スタックの IRP_MJ_PNP が成功しなかった非 STATUS_NOT_SUPPORTED IRP ステータスが渡されます。 (IRP を指定します。)失敗した PNP Irp を完了する必要があります。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x216</p></td>
<td align="left"><p>致命的でないエラー</p></td>
<td align="left"><p>前に設定された IRP_MJ_PNP 状態は STATUS_NOT_SUPPORTED に変換されています。 (IRP を指定します。)このエラー状態は、オペレーティング システムで使用するために予約されています。 ドライバーには、この値を持つ PnP IRP が失敗することはできません。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x217</p></td>
<td align="left"><p>致命的でないエラー</p></td>
<td align="left"><p>ドライバーが必要な IRP を処理していません。 ドライバーが処理されたかどうかを示す IRP の状態を更新する必要があります。 (IRP を指定します。)</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x218</p></td>
<td align="left"><p>致命的でないエラー</p></td>
<td align="left"><p>ドライバーは、別の場所スタック内の他のデバイス オブジェクトに予約されている IRP に応答しました。 (IRP を指定します。)</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x219</p></td>
<td align="left"><p>致命的でないエラー</p></td>
<td align="left"><p>スタックに対し、IRP_MJ_POWER が成功しなかった非 STATUS_NOT_SUPPORTED IRP のステータスが渡されます。 (IRP を指定します。)障害が発生した電源 Irp を完了する必要があります。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x21A</p></td>
<td align="left"><p>致命的でないエラー</p></td>
<td align="left"><p>前に設定された対し、IRP_MJ_POWER 状態は STATUS_NOT_SUPPORTED に変換されています。 (IRP を指定します。)</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x21B</p></td>
<td align="left"><p>致命的でないエラー</p></td>
<td align="left"><p>ドライバーには、不審なステータスが返されます。 ドライバーの初期化されていない変数バグが原因として考えられます。 (IRP を指定します。)</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x21C</p></td>
<td align="left"><p>警告</p></td>
<td align="left"><p>IRP スタックのコピーが、呼び出し元が、完了ルーチンを設定できません。 これは効率的ではありません--を使用して、 <strong>IoSkipCurrentIrpStackLocation</strong>代わりにします。 (IRP を指定します。)</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x21D</p></td>
<td align="left"><p>致命的なエラー</p></td>
<td align="left"><p>IRP のディスパッチ ハンドラーが削除 IRP を受信すると、下にあるスタックから正しくデタッチがされません。 (デバイス オブジェクト、ディスパッチ ルーチン、および IRP の指定)</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x21E</p></td>
<td align="left"><p>致命的なエラー</p></td>
<td align="left"><p>IRP のディスパッチ ハンドラーは、削除 IRP を受信すると、そのデバイス オブジェクトを正しく削除されませんが。 (デバイス オブジェクト、ディスパッチ ルーチン、および IRP の指定)</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x21F</p></td>
<td align="left"><p>致命的でないエラー</p></td>
<td align="left"><p>ドライバーは、必要な IRP の主要な関数のディスパッチ ルーチンはデータが格納されません。 (IRP を指定します。)</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x220</p></td>
<td align="left"><p>致命的でないエラー</p></td>
<td align="left"><p>ProviderId が以外によって IRP_MJ_SYSTEM_CONTROL が完了しました。 この IRP では、する必要がありますか、完了前または渡される必要があります。 (対象となったデバイス オブジェクトと共に指定 IRP)。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x221</p></td>
<td align="left"><p>致命的なエラー</p></td>
<td align="left"><p>PDO の IRP にディスパッチ ハンドラーがそのデバイス オブジェクトを削除しますが、バスのリレーションのクエリで不足するいると、ハードウェアが報告されていません。 (デバイス オブジェクト、ディスパッチ ルーチン、および IRP の指定)</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x222</p></td>
<td align="left"><p>致命的なエラー</p></td>
<td align="left"><p>Bus フィルターの IRP ディスパッチ ハンドラーが PDO がアライブの場合は、削除 IRP を受信するとデタッチします。 クリーンアップする必要があります bus フィルター <strong>FastIoDetach</strong>コールバック。 (デバイス オブジェクト、ディスパッチ ルーチン、および IRP の指定)</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x223</p></td>
<td align="left"><p>致命的なエラー</p></td>
<td align="left"><p>バスのフィルターの IRP ディスパッチ ハンドラーがそのデバイス オブジェクトを削除は、PDO はまだ存在します。 クリーンアップする必要があります bus フィルター <strong>FastIoDetach</strong>コールバック。 (デバイス オブジェクト、ディスパッチ ルーチン、および IRP の指定)</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x224</p></td>
<td align="left"><p>致命的なエラー</p></td>
<td align="left"><p>IRP のディスパッチ ハンドラーに IRP に矛盾する状態が返される<strong>IoStatus.Status</strong>フィールド。 (ハンドラー ルーチン、IRP、IRP の IoStatus.Status、および返された状態の指定をディスパッチします。)</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x225</p></td>
<td align="left"><p>致命的でないエラー</p></td>
<td align="left"><p>IRP のディスパッチ ハンドラーには有効でない状態が返されましたが (0 xffffffff) です。 これはおそらく、初期化されていないスタック変数です。 このエラーをデバッグするには、使用、 <strong><a href="ln--list-nearest-symbols-.md" data-raw-source="[ln (List Nearest Symbols)](ln--list-nearest-symbols-.md)">ln (最も近いシンボルの一覧)</a></strong>アドレスが指定されているコマンド。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x226</p></td>
<td align="left"><p>致命的なエラー</p></td>
<td align="left"><p>渡して、または、この IRP の完了せず IRP のディスパッチ ハンドラーが返されるまたは STATUS_PENDING を返すことをユーザーが忘れた場合します。 (IRP を指定します。)</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x227</p></td>
<td align="left"><p>致命的なエラー</p></td>
<td align="left"><p>IRP の完了ルーチンが、ページング可能なコードです。 (これはできません。)(ルーチンと IRP を指定します)。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x228</p></td>
<td align="left"><p>致命的でないエラー</p></td>
<td align="left"><p>ドライバーの完了のルーチンが保留中の場合は IRP をマークしていない、 <strong>PendingReturned</strong>フィールドが渡された IRP に設定します。 スタックによってエラーが返される場合は特に、停止して Windows があります。 (ルーチンと IRP を指定します)。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x229</p></td>
<td align="left"><p>致命的なエラー</p></td>
<td align="left"><p>キャンセル ルーチンは、おそらくそのキャンセル ルーチンを費やし、スタック内の下位のドライバーで現在処理中 IRP の設定されています。 (ルーチンと IRP を指定します)。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x22A</p></td>
<td align="left"><p>致命的でないエラー</p></td>
<td align="left"><p>物理デバイス オブジェクト (PDO) が必要な IRP に応答しませんでした。 (IRP を指定します。)</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x22B</p></td>
<td align="left"><p>致命的でないエラー</p></td>
<td align="left"><p>物理デバイス オブジェクト (PDO) が、デバイスの関係のリストの PDO の入力を忘れた、 <strong>TargetDeviceRelation</strong>クエリ。 (IRP を指定します。)</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x22C</p></td>
<td align="left"><p>致命的なエラー</p></td>
<td align="left"><p>コードを実装する、 <strong>TargetDeviceRelation</strong>クエリが呼び出されていない<strong>ObReferenceObject</strong> PDO にします。 (IRP を指定します。)</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x22D</p></td>
<td align="left"><p>致命的でないエラー</p></td>
<td align="left"><p>呼び出し元に渡すことではなくそれを理解していない IRP_MJ_PNP が完了しました。 (IRP を指定します。)</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x22E</p></td>
<td align="left"><p>致命的でないエラー</p></td>
<td align="left"><p>呼び出し元に渡すことではなく成功 IRP_MJ_PNP が完了しました。 (IRP を指定します。)</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x22F</p></td>
<td align="left"><p>致命的でないエラー</p></td>
<td align="left"><p>呼び出し元の (IRP を渡します)、代わりに手を加えず、IRP_MJ_PNP が完了したか、非 PDO は STATUS_NOT_SUPPORTED の無効な値を使用して IRP を失敗しました。 (IRP を指定します。)</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x230</p></td>
<td align="left"><p>致命的でないエラー</p></td>
<td align="left"><p>呼び出し元渡すことではなく理解していないことに対し、IRP_MJ_POWER が完了しました。 (IRP を指定します。)</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x231</p></td>
<td align="left"><p>致命的なエラー</p></td>
<td align="left"><p>呼び出し元渡すことではなく、正常に対し、IRP_MJ_POWER が完了しました。 (IRP を指定します。)</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x232</p></td>
<td align="left"><p>致命的でないエラー</p></td>
<td align="left"><p>呼び出し元が完了 (IRP を渡します)、代わりに対し、手を加えず、IRP_MJ_POWER または PDO 以外に STATUS_NOT_SUPPORTED の無効な値を使用して IRP が失敗しました。 (IRP を指定します。)</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x233</p></td>
<td align="left"><p>致命的でないエラー</p></td>
<td align="left"><p>IRP が正しく初期化されていないクエリ機能のクエリ機能の構造のバージョン フィールド。 (IRP を指定します。)</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x234</p></td>
<td align="left"><p>致命的でないエラー</p></td>
<td align="left"><p>IRP が正しく初期化されていないクエリ機能のクエリ機能の構造体のサイズのフィールド。 (IRP を指定します。)</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x235</p></td>
<td align="left"><p>致命的でないエラー</p></td>
<td align="left"><p>IRP が-1 に正しく初期化されていませんクエリ機能のクエリ機能の構造体のアドレス フィールドです。 (IRP を指定します。)</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x236</p></td>
<td align="left"><p>致命的でないエラー</p></td>
<td align="left"><p>IRP が-1 に正しく初期化されていませんクエリ機能のクエリ機能の構造体の UI 番号フィールドです。 (IRP を指定します。)</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x237</p></td>
<td align="left"><p>致命的なエラー</p></td>
<td align="left"><p>ドライバーは IRP がシステムでのみ使用が制限されているが送信されます。 (IRP を指定します。)</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x238</p></td>
<td align="left"><p>警告</p></td>
<td align="left"><p>呼び出し元<strong>IoInitializeIrp</strong>で割り当てられた IRP が渡される<strong>IoAllocateIrp</strong>します。 これは無効な不要なし、通常の用途でのパフォーマンスが低下します。 この IRP がリサイクルされている場合は、<strong>IoReuseIrp</strong> Windows Driver Kit でを参照してください。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x239</p></td>
<td align="left"><p>警告</p></td>
<td align="left"><p>呼び出し元<strong>IoCompleteRequest</strong>が完了しているが、決してへの呼び出しを使用して転送された IRP<strong>保留</strong>または<strong>PoCallDriver</strong>します。 バグがあります。 (IRP を指定します。)</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x23A</p></td>
<td align="left"><p>致命的なエラー</p></td>
<td align="left"><p>ドライバーでは、この大規模なコードに対して有効である IRQL で IRP を転送します。 (IRP を指定します。)</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x23B</p></td>
<td align="left"><p>致命的でないエラー</p></td>
<td align="left"><p>呼び出し元が認識しない IRP のステータス フィールドが変更されました。 (IRP を指定します。)</p></td>
</tr>
</tbody>
</table>

 

次の表にリストに追加**I/O の検証**エラーを表示できます。 場合これらのエラーのいくつか公開のみ**I/O の検証の強化された**がアクティブ化されます。 Windows Vista 以降では、 **I/O の検証の強化された**設定の一部として含める**I/O の検証**です。

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">I/O エラー コード</th>
<th align="left">重大度</th>
<th align="left">エラーの原因</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>0x23C</p></td>
<td align="left"><p>致命的なエラー</p></td>
<td align="left"><p>ドライバーが IRP を完了したキャンセル ルーチンを IRP を設定せず<strong>NULL</strong>します。 (IRP を指定します。)</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x23D</p></td>
<td align="left"><p>致命的でないエラー</p></td>
<td align="left"><p>ドライバーは STATUS_PENDING を返しましたが、呼び出しに保留中の IRP まったくマークしていない<strong>IoMarkIrpPending</strong>します。 (IRP を指定します。)</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x23E</p></td>
<td align="left"><p>致命的でないエラー</p></td>
<td align="left"><p>ドライバーは保留中の IRP がマークしますが、STATUS_PENDING を返されませんでした。 (IRP を指定します。)</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x23F</p></td>
<td align="left"><p>致命的なエラー</p></td>
<td align="left"><p>ドライバーは、スタックがアタッチされてから DO_POWER_PAGABLE ビットを継承されませんが。 (デバイス オブジェクトを指定します。)</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x240</p></td>
<td align="left"><p>致命的なエラー</p></td>
<td align="left"><p>以前の呼び出しには既に削除されているデバイス オブジェクトを削除しようとして、ドライバー <strong>IoDeleteDevice</strong>します。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x241</p></td>
<td align="left"><p>致命的なエラー</p></td>
<td align="left"><p>ドライバーが突然削除 IRP の中にデバイス、そのオブジェクトをデタッチします。 (IRP とデバイス オブジェクトを指定します。)</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x242</p></td>
<td align="left"><p>致命的なエラー</p></td>
<td align="left"><p>ドライバーには、突然削除 IRP の中にそのデバイス オブジェクトが削除されました。 (IRP とデバイス オブジェクトを指定します。)</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x243</p></td>
<td align="left"><p>致命的なエラー</p></td>
<td align="left"><p>末尾に DO_DEVICE_INITIALIZING フラグをクリアするドライバーが失敗しました<strong>AddDevice</strong>します。 (デバイス オブジェクトを指定します。)</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x244</p></td>
<td align="left"><p>致命的なエラー</p></td>
<td align="left"><p>アタッチは、デバイス オブジェクトからは、ドライバーが、DO_BUFFERED_IO または DO_DIRECT_IO フラグはコピーしていません。 (デバイス オブジェクトを指定します。)</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x245</p></td>
<td align="left"><p>致命的なエラー</p></td>
<td align="left"><p>ドライバーが、DO_BUFFERED_IO と DO_DIRECT_IO フラグの両方に設定します。 これらのフラグは、相互に排他的です。 (デバイス オブジェクトを指定します。)</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x246</p></td>
<td align="left"><p>致命的なエラー</p></td>
<td align="left"><p>ドライバーがコピーに失敗しましたが、 <strong>DeviceType</strong>フィールドへのアタッチは、デバイス オブジェクトからです。 (デバイス オブジェクトを指定します。)</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x247</p></td>
<td align="left"><p>致命的なエラー</p></td>
<td align="left"><p>ドライバーには、合法的に失敗したことはできません IRP が失敗しました。 (IRP を指定します。)</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x248</p></td>
<td align="left"><p>致命的なエラー</p></td>
<td align="left"><p>ドライバーが、デバイスのリレーションのクエリに PDO ではないデバイス オブジェクトを追加します。 (IRP とデバイス オブジェクトを指定します。)</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x249</p></td>
<td align="left"><p>致命的でないエラー</p></td>
<td align="left"><p>ドライバーが同じデバイス Id が返される 2 つの子 Pdo を列挙します。 (両方デバイス オブジェクトを指定します。)</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x24A</p></td>
<td align="left"><p>致命的なエラー</p></td>
<td align="left"><p>ドライバーが誤ってファイルと呼ばれる、IRQL で関数を I/O PASSIVE_LEVEL 等しくありません。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x24B</p></td>
<td align="left"><p>致命的なエラー</p></td>
<td align="left"><p>ドライバーには、型の IRP_MN_QUERY_DEVICE_RELATIONS 要求が完了した<strong>TargetDeviceRelation</strong>として成功するですが正しくない要求に記入か、基になるハードウェアのスタックに IRP を転送します。 (デバイス オブジェクトを指定します。)</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x24C</p></td>
<td align="left"><p>致命的でないエラー</p></td>
<td align="left"><p>ドライバーは STATUS_PENDING を返しましたが、まったくへの呼び出しで保留中の IRP をマークしていない<strong>IoMarkIrpPending</strong>します。 (IRP を指定します。)</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x24D</p></td>
<td align="left"><p>致命的なエラー</p></td>
<td align="left"><p>ドライバーには、PDO を必要とする関数に無効なデバイス オブジェクトが渡されます。 (デバイス オブジェクトを指定します。)</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x300</p></td>
<td align="left"><p>致命的でないエラー</p></td>
<td align="left"><p>ドライバーには、不審なステータスが返されます。 ドライバーの初期化されていない変数バグが原因として考えられます。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x301</p></td>
<td align="left"><p>致命的でないエラー</p></td>
<td align="left"><p>ドライバーは IRP IRQL で、転送&gt;DISPATCH_LEVEL します。 (IRQL の値を指定)</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x302</p></td>
<td align="left"><p>致命的でないエラー</p></td>
<td align="left"><p>ドライバーは IRP IRQL で、転送&gt;APC_LEVEL を = です。</p>
<p>この要求を完了する APC をキューには、I/O マネージャーは必要があります。 APC では、呼び出し元が既に APC レベルでは、呼び出し元はデッドロックが発生する可能性が高いため、実行できません。 (IRQL の値を指定)</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x306</p></td>
<td align="left"><p>致命的でないエラー</p></td>
<td align="left"><p>ドライバーが完了して、(メジャー) IRP_MJ_PNP と IRP_MN_REMOVE_DEVICE (マイナー) 要求の失敗の状態コード。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x307</p></td>
<td align="left"><p>致命的でないエラー</p></td>
<td align="left"><p>ドライバーとイベントが既にシグナル状態し、STATUS_PENDING 応答の受信の I/O 要求が発行されます。 アンワインド、I/O が完了する前に、これがあります。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x310</p></td>
<td align="left"><p>致命的でないエラー</p></td>
<td align="left"><p>ドライバーが使用中である IRP を再初期化します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x311</p></td>
<td align="left"><p>致命的でないエラー</p></td>
<td align="left"><p>ドライバーが、IoMakeAssociatedIrp、IoBuildAsynchronousFsdRequest、IoBuildSynchronousFsdRequest IoBuildDeviceIoControlRequest で作成された IRP を再初期化します。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x312</p></td>
<td align="left"><p>致命的でないエラー</p></td>
<td align="left"><p>呼び出し元には、システムのバッファーの出力セクションよりも大きい値を持つ IRP のステータス情報フィールドが提供されています。</p></td>
</tr>
</tbody>
</table>

 

<a name="cause"></a>原因
-----

原因の詳細については、パラメーター セクション内の各コードの説明を参照してください。

<a name="resolution"></a>解決方法
----------

このバグ チェックは、Driver Verifier が 1 つまたは複数のドライバーを監視するように指示された場合にのみ発生します。 Driver Verifier の使用は意図しない、非アクティブ化する必要があります。 この問題の原因となったドライバーの削除を検討する可能性があります。

ドライバー開発者の場合は、このバグ チェックで得られた情報を使用して、コードで、バグを修正します。

詳細については、Driver Verifier は、Windows ドライバー キットを参照してください。

 

 




