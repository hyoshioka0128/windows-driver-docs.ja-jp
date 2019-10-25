---
title: バグチェック 0x144 BUGCODE_USB3_DRIVER
description: BUGCODE_USB3_DRIVER のバグチェックの値は0x00000144 です。 これは、すべての USB 3 バグチェックに使用されるコードです。
ms.assetid: 39414287-3E20-405B-846A-B7F9F8AEE078
keywords:
- バグチェック 0x144 BUGCODE_USB3_DRIVER
- BUGCODE_USB3_DRIVER
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- BUGCODE_USB3_DRIVER
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 74c25bd7361e531d0fdf0fa1316267cbe733edf5
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72837635"
---
# <a name="bug-check-0x144-bugcode_usb3_driver"></a>バグチェック 0x144: バグコード\_USB3\_ドライバー


バグ**コード\_USB3\_ドライバー**のバグチェックには、0x00000144 という値が指定されています。 これは、すべての USB 3 バグチェックに使用されるコードです。 パラメーター1は、USB 3 のバグチェックの種類を指定し、その他のパラメーターの意味はパラメーター1に依存します。

> [!IMPORTANT]
> このトピックはプログラマーを対象としています。 コンピューターの使用中にブルースクリーンのエラーコードが表示された顧客の場合は、「[ブルースクリーンエラーのトラブルシューティング](https://www.windows.com/stopcode)」を参照してください。


## <a name="bugcode_usb3_driver-parameters"></a>USB3\_ドライバーパラメーター\_のバグコード


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
<th align="left">パラメーター1</th>
<th align="left">パラメータ 2</th>
<th align="left">パラメーター3</th>
<th align="left">パラメーター4</th>
<th align="left">エラーの原因</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>0x1</p></td>
<td align="left"><p>(省略可能)。 URB を再送信するために使用される IRP へのポインター</p></td>
<td align="left"><p>URB へのポインター</p></td>
<td align="left"><p>クライアントドライバーのデバイスオブジェクトへのポインター</p></td>
<td align="left"><p>クライアントドライバーは、以前にコアスタックに送信した URB を使用しました。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x2</p></td>
<td align="left"><p>ブートデバイスの物理デバイスオブジェクト (PDO) へのポインター</p></td>
<td align="left"><p>予約済み</p></td>
<td align="left"><p>予約済み</p></td>
<td align="left"><p>ブートデバイスまたはページングデバイスを再列挙できませんでした。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x3</p></td>
<td align="left"><p>(省略可能)。 URB の送信に使用される IRP へのポインター</p></td>
<td align="left"><p>破損した URB へのポインター</p></td>
<td align="left"><p>クライアントドライバーのデバイスオブジェクトへのポインター</p></td>
<td align="left"><p>クライアントドライバーが、破損した URB をコアスタックに送信しました。 これは、クライアントドライバーが<strong>USBD_<em>xxx</em>ur・</strong>を使用して urb を割り当てなかったか、クライアントドライバーが urb 用のバッファーアンダーランを使用したために発生する可能性があります。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x800</p></td>
<td align="left"><p>オープンスタティックストリーム要求が送信された IRQL</p></td>
<td align="left"><p>開いている静的ストリーム IRP へのポインター</p></td>
<td align="left"><p>クライアントドライバーのデバイスオブジェクトへのポインター</p></td>
<td align="left"><p>オープンスタティックストリーム要求が、IRQL &gt; パッシブレベルで送信されました。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x801</p></td>
<td align="left"><p>開いている静的ストリーム IRP へのポインター</p></td>
<td align="left"><p>開いている静的ストリームの URB へのポインター</p></td>
<td align="left"><p>クライアントドライバーのデバイスオブジェクトへのポインター</p></td>
<td align="left"><p>クライアントドライバーがストリームの機能を照会する前に、静的ストリームを開こうとしました。 クライアントドライバーは、ストリーム機能のクエリが正常に実行されるまで、静的ストリームを開くことができません。 詳細については、「解説」を参照してください。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x802</p></td>
<td align="left"><p>クライアントドライバーが開こうとした静的ストリームの数</p></td>
<td align="left"><p>クライアントドライバーに付与された静的ストリームの数</p></td>
<td align="left"><p>クライアントドライバーのデバイスオブジェクトへのポインター</p></td>
<td align="left"><p>クライアントドライバーが、無効な数の静的ストリームを開こうとしました。 ストリームの数を0にすることはできません。また、クエリの USB 機能呼び出しでクライアントドライバーに返される値よりも大きくすることはできません。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x803</p></td>
<td align="left"><p>開いている静的ストリーム IRP へのポインター</p></td>
<td align="left"><p>開いている静的ストリームの URB へのポインター</p></td>
<td align="left"><p>クライアントドライバーのデバイスオブジェクトへのポインター</p></td>
<td align="left"><p>クライアントドライバーが、既に静的ストリームを開いているエンドポイントの静的ストリームを開こうとしました。 静的ストリームを開く前に、クライアントドライバーは、前に開いていた静的ストリームを閉じる必要があります。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x804</p></td>
<td align="left"><p>リークされたハンドルコンテキスト。 リークしたハンドルと URBs に関する情報を取得するには、 <strong>! usbanalyze-v</strong>を実行します。 クライアントドライバーのドライバー検証を有効にする必要があります。</p></td>
<td align="left"><p><strong><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/usbdlib/nf-usbdlib-usbd_createhandle" data-raw-source="[USBD_CreateHandle](https://docs.microsoft.com/windows-hardware/drivers/ddi/usbdlib/nf-usbdlib-usbd_createhandle)">USBD_CreateHandle</a></strong>に渡されるデバイスオブジェクト。</p></td>
<td align="left"><p>予約済み</p></td>
<td align="left"><p>クライアントドライバーは、以前に<strong><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/usbdlib/nf-usbdlib-usbd_createhandle" data-raw-source="[USBD_CreateHandle](https://docs.microsoft.com/windows-hardware/drivers/ddi/usbdlib/nf-usbdlib-usbd_createhandle)">USBD_CreateHandle</a></strong>を使用して作成したハンドルを閉じることを忘れたか、割り当てた URB の解放を忘れました。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x805</p></td>
<td align="left"><p>閉じる静的ストリームの URB の<a href="https://docs.microsoft.com/windows-hardware/drivers/wdf/framework-request-objects" data-raw-source="[WDFREQUEST](https://docs.microsoft.com/windows-hardware/drivers/wdf/framework-request-objects)">Wdfrequest</a>ハンドル</p></td>
<td align="left"><p>閉じる静的ストリームの URB へのポインター</p></td>
<td align="left"><p>クライアントドライバーのデバイスオブジェクトへのポインター</p></td>
<td align="left"><p>クライアントドライバーが、無効な状態 (たとえば、D0 Exit の処理後) に、閉じた静的ストリームの URB を送信しました。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x806</p></td>
<td align="left"><p>IRP へのポインター</p></td>
<td align="left"><p>URB へのポインター</p></td>
<td align="left"><p>クライアントドライバーのデバイスオブジェクトへのポインター</p></td>
<td align="left"><p>クライアントドライバーがチェーンされた<strong>mdl 機能の</strong>クエリを実行する前に、チェーンされた<strong><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_mdl" data-raw-source="[MDL](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_mdl)">mdl</a></strong>を送信しようとしました。 クライアントドライバーは、チェーンされた<strong>mdl</strong>機能のクエリが正常に行われるまで、チェーンされた<strong>mdl</strong>を送信できません。 詳細については、「解説」を参照してください。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x807</p></td>
<td align="left"><p>チェーンされた <strong><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_mdl" data-raw-source="[MDL](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_mdl)">MDL</a>へのポインター</strong></p></td>
<td align="left"><p>URB へのポインター</p></td>
<td align="left"><p>クライアントドライバーのデバイスオブジェクトへのポインター (使用可能な場合)</p></td>
<td align="left"><p>クライアントドライバーが、渡された<strong><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_mdl" data-raw-source="[MDL](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_mdl)">MDL</a></strong>のバイト数 ( <strong><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-mmgetmdlbytecount" data-raw-source="[MmGetMdlByteCount](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-mmgetmdlbytecount)">MmGetMdlByteCount</a></strong>によって返されたバイト数) よりも長い転送バッファー長を持つコアスタックに URB を送信しました。 詳細については、「解説」を参照してください。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x1001</p></td>
<td align="left"><p>XHCI_LIVEDUMP_CONTEXT</p></td>
<td align="left"><p>予約済み</p></td>
<td align="left"><p>予約済み</p></td>
<td align="left"><p>XHCI コントローラーは、ホストシステムエラーを示す HSE ビットをアサートします。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x1002</p></td>
<td align="left"><p>XHCI_LIVEDUMP_CONTEXT</p></td>
<td align="left"><p>予約済み</p></td>
<td align="left"><p>予約済み</p></td>
<td align="left"><p>XHCI コントローラーは、ホストコントローラーエラーを示す HCE ビットをアサートします。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x1003</p></td>
<td align="left"><p>XHCI_LIVEDUMP_CONTEXT</p></td>
<td align="left"><p>予約済み</p></td>
<td align="left"><p>予約済み</p></td>
<td align="left"><p>XHCI stop endpoint コマンドにより、未処理の完了コードが返されました。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x1004</p></td>
<td align="left"><p>XHCI_LIVEDUMP_CONTEXT</p></td>
<td align="left"><p>予約済み</p></td>
<td align="left"><p>予約済み</p></td>
<td align="left"><p>XHCI エンドポイントの状態は、xHCI endpoint stop コマンドが発行された後にコンテキスト状態エラーを受信しました。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x1005</p></td>
<td align="left"><p>XHCI_LIVEDUMP_CONTEXT</p></td>
<td align="left"><p>予約済み</p></td>
<td align="left"><p>予約済み</p></td>
<td align="left"><p>コントロールエンドポイントの停止を解除しようとしたときに、デキューポインターを設定できませんでした。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x1006</p></td>
<td align="left"><p>XHCI_LIVEDUMP_CONTEXT</p></td>
<td align="left"><p>予約済み</p></td>
<td align="left"><p>予約済み</p></td>
<td align="left"><p>コントロールエンドポイントの停止を解除しようとしたときに、EP をリセットできませんでした。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x1007</p></td>
<td align="left"><p>XHCI_LIVEDUMP_CONTEXT</p></td>
<td align="left"><p>予約済み</p></td>
<td align="left"><p>予約済み</p></td>
<td align="left"><p>リセットの復旧中に、xHCI コントローラーをリセットできませんでした。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x1008</p></td>
<td align="left"><p>XHCI_LIVEDUMP_CONTEXT</p></td>
<td align="left"><p>予約済み</p></td>
<td align="left"><p>予約済み</p></td>
<td align="left"><p>リセットの復旧中に、xHCI コントローラーの再起動に失敗しました。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x1009</p></td>
<td align="left"><p>XHCI_LIVEDUMP_CONTEXT</p></td>
<td align="left"><p>予約済み</p></td>
<td align="left"><p>予約済み</p></td>
<td align="left"><p>コマンドタイムアウトの中止後、xHCI controller コマンドを完了できませんでした。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x100A</p></td>
<td align="left"><p>XHCI_LIVEDUMP_CONTEXT</p></td>
<td align="left"><p>予約済み</p></td>
<td align="left"><p>予約済み</p></td>
<td align="left"><p>エンドポイントの停止完了後にデキューポインターを設定しようとしたときに、デキューポインターを設定できませんでした。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x100B</p></td>
<td align="left"><p>XHCI_LIVEDUMP_CONTEXT</p></td>
<td align="left"><p>予約済み</p></td>
<td align="left"><p>予約済み</p></td>
<td align="left"><p>リセットの復旧中に、xHCI コントローラーの停止に失敗しました。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x100C</p></td>
<td align="left"><p>XHCI_LIVEDUMP_CONTEXT</p></td>
<td align="left"><p>予約済み</p></td>
<td align="left"><p>予約済み</p></td>
<td align="left"><p>XHCI コントローラーのファームウェアはサポートされていません。 ファームウェアが更新されない限り、xHCI ドライバーはこのコントローラーに読み込まれません。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x100D</p></td>
<td align="left"><p>XHCI_LIVEDUMP_CONTEXT</p></td>
<td align="left"><p>予約済み</p></td>
<td align="left"><p>予約済み</p></td>
<td align="left"><p>コントローラーが物理的に削除されたことが検出されました。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x100E</p></td>
<td align="left"><p>XHCI_LIVEDUMP_CONTEXT</p></td>
<td align="left"><p>予約済み</p></td>
<td align="left"><p>予約済み</p></td>
<td align="left"><p>ドライバーは、ストリームが有効なエンドポイントでエラーを検出します。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x100F</p></td>
<td align="left"><p>XHCI_LIVEDUMP_CONTEXT</p></td>
<td align="left"><p>予約済み</p></td>
<td align="left"><p>予約済み</p></td>
<td align="left"><p>XHCI コントローラーのファームウェアが古くなっています。 XHCI ドライバーはこのコントローラーの操作を続行しますが、いくつかの問題が発生する可能性があります。 ファームウェアを更新することをお勧めします。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x1010</p></td>
<td align="left"><p>XHCI_LIVEDUMP_CONTEXT</p></td>
<td align="left"><p>予約済み</p></td>
<td align="left"><p>予約済み</p></td>
<td align="left"><p>未処理の完了コードを使用して、転送イベントが完了しました。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x1011</p></td>
<td align="left"><p>XHCI_LIVEDUMP_CONTEXT</p></td>
<td align="left"><p>予約済み</p></td>
<td align="left"><p>予約済み</p></td>
<td align="left"><p>コントローラーは、イベントリングがいっぱいになったことを報告しました。 コントローラーは、この発生時にイベントを削除することも知られています。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x1012</p></td>
<td align="left"><p>XHCI_LIVEDUMP_CONTEXT</p></td>
<td align="left"><p>予約済み</p></td>
<td align="left"><p>予約済み</p></td>
<td align="left"><p>コントローラーはコマンドの順序が正常に完了しませんでした。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x1013</p></td>
<td align="left"><p>XHCI_LIVEDUMP_CONTEXT</p></td>
<td align="left"><p>予約済み</p></td>
<td align="left"><p>予約済み</p></td>
<td align="left"><p>コマンドの中止が完了すると、コントローラーによって報告されたコマンドリングデキューポインターが正しくありません。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x1014</p></td>
<td align="left"><p>XHCI_LIVEDUMP_CONTEXT</p></td>
<td align="left"><p>予約済み</p></td>
<td align="left"><p>予約済み</p></td>
<td align="left"><p>スロットの有効化を有効にした後、コントローラーから無効なスロット id が与えられました。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x1015</p></td>
<td align="left"><p>XHCI_LIVEDUMP_CONTEXT</p></td>
<td align="left"><p>予約済み</p></td>
<td align="left"><p>予約済み</p></td>
<td align="left"><p>コントローラーが BSR1 で SetAddress コマンドを実行できませんでした。 これは予期されていません。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x1016</p></td>
<td align="left"><p>XHCI_LIVEDUMP_CONTEXT</p></td>
<td align="left"><p>予約済み</p></td>
<td align="left"><p>予約済み</p></td>
<td align="left"><p>Usb デバイスのリセット中にコントローラーがスロットを有効にできませんでした。 これは予期されていません。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x1017</p></td>
<td align="left"><p>XHCI_LIVEDUMP_CONTEXT</p></td>
<td align="left"><p>予約済み</p></td>
<td align="left"><p>予約済み</p></td>
<td align="left"><p>コントローラーが、エンドポイントを構成するコマンドを構成できませんでした。エンドポイントを deconfiguring しました。 これは予期されていません。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x1018</p></td>
<td align="left"><p>XHCI_LIVEDUMP_CONTEXT</p></td>
<td align="left"><p>予約済み</p></td>
<td align="left"><p>予約済み</p></td>
<td align="left"><p>コントローラーがスロットの無効化コマンドを実行できませんでした。 これは予期されていません。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x1019</p></td>
<td align="left"><p>XHCI_LIVEDUMP_CONTEXT</p></td>
<td align="left"><p>予約済み</p></td>
<td align="left"><p>予約済み</p></td>
<td align="left"><p>コントローラーで USB デバイスのリセットコマンドを実行できませんでした。 これは予期されていません。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x101A</p></td>
<td align="left"><p>XHCI_LIVEDUMP_CONTEXT</p></td>
<td align="left"><p>予約済み</p></td>
<td align="left"><p>予約済み</p></td>
<td align="left"><p>エンドポイントのリセット後に、デキューポインターの設定コマンドが失敗しました。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x101B</p></td>
<td align="left"><p>XHCI_LIVEDUMP_CONTEXT</p></td>
<td align="left"><p>予約済み</p></td>
<td align="left"><p>予約済み</p></td>
<td align="left"><p>XHCI reset endpoint コマンドにより、未処理の完了コードが返されました。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x101C</p></td>
<td align="left"><p>XHCI_LIVEDUMP_CONTEXT</p></td>
<td align="left"><p>予約済み</p></td>
<td align="left"><p>予約済み</p></td>
<td align="left"><p>XHCI の D0Entry が失敗しました。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x101D</p></td>
<td align="left"><p>XHCI_LIVEDUMP_CONTEXT</p></td>
<td align="left"><p>予約済み</p></td>
<td align="left"><p>予約済み</p></td>
<td align="left"><p>要求のキャンセル時にデキューポインターを設定するのではなく、エンドポイントの構成コマンドを使用すると、ストリームエンドポイント (2 つのコマンドとして) を一時的に削除して、追加できませんでした。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x101E</p></td>
<td align="left"><p>XHCI_LIVEDUMP_CONTEXT</p></td>
<td align="left"><p>予約済み</p></td>
<td align="left"><p>予約済み</p></td>
<td align="left"><p>コントローラーで、コントローラーで保留されていない転送完了が示されました。 EventData = = 1 (転送イベント TRB のポインターを逆参照すると、バグチェックが発生しました)</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x101F</p></td>
<td align="left"><p>XHCI_LIVEDUMP_CONTEXT</p></td>
<td align="left"><p>予約済み</p></td>
<td align="left"><p>予約済み</p></td>
<td align="left"><p>コントローラーで、コントローラーで保留されていない転送完了が示されました。 EventData = = 0 (転送イベントの論理アドレス TRB が一致しません)</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x0</p></td>
<td align="left"><p>XHCI_LIVEDUMP_CONTEXT</p></td>
<td align="left"><p>予約済み</p></td>
<td align="left"><p>予約済み</p></td>
<td align="left"><p>コントローラーで、コントローラーで保留されていない転送完了が示されました。 EventData = = 0 (転送イベント TRB の論理アドレスが一致しません) 転送イベント TRB は冗長になる可能性があります (最近完了した要求の近くの場所を指します)。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x-1</p></td>
<td align="left"><p>XHCI_LIVEDUMP_CONTEXT</p></td>
<td align="left"><p>予約済み</p></td>
<td align="left"><p>予約済み</p></td>
<td align="left"><p>停止していないエンドポイントのリセットの一環として [エンドポイントの構成] コマンドを使用すると、ストリームエンドポイント (2 つのコマンドとして) を一時的に削除して追加できませんでした。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x1024 x 2</p></td>
<td align="left"><p>XHCI_LIVEDUMP_CONTEXT</p></td>
<td align="left"><p>予約済み</p></td>
<td align="left"><p>予約済み</p></td>
<td align="left"><p>(1 つのコマンドとして) 同じエンドポイントを削除して追加できませんでした。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x3000</p></td>
<td align="left"><p>USBHUB3_LIVEDUMP_CONTEXT</p></td>
<td align="left"><p>予約済み</p></td>
<td align="left"><p>予約済み</p></td>
<td align="left"><p>ハブドライバーによって不適切なハブが正常にリセットされました。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x3001</p></td>
<td align="left"><p>USBHUB3_LIVEDUMP_CONTEXT</p></td>
<td align="left"><p>予約済み</p></td>
<td align="left"><p>予約済み</p></td>
<td align="left"><p>ハブドライバによって不適切なハブを正常にリセットできませんでした。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x3002</p></td>
<td align="left"><p>USBHUB3_LIVEDUMP_CONTEXT</p></td>
<td align="left"><p>予約済み</p></td>
<td align="left"><p>予約済み</p></td>
<td align="left"><p>非関数 SuperSpeed hub はハブドライバーによって無効にされました。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x3003</p></td>
<td align="left"><p>USBHUB3_LIVEDUMP_CONTEXT</p></td>
<td align="left"><p>予約済み</p></td>
<td align="left"><p>予約済み</p></td>
<td align="left"><p>USB デバイスの列挙に失敗しました。</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>注釈
-------

USB 機能を照会するには、クライアントドライバーが[**WdfUsbTargetDeviceQueryUsbCapability**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfusb/nf-wdfusb-wdfusbtargetdevicequeryusbcapability)または[**USBD\_queryusbcapability**](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/hh406230(v=vs.85))を呼び出す必要があります。

チェーン化された[**mdl**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_mdl)を送信するには、クライアントドライバーは[**USBD\_queryusbcapability**](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/hh406230(v=vs.85))を呼び出し、 **URB\_関数を使用\_一括\_または\_\_のチェーン化された\_を使用して\_を転送\_転送する必要があります。** または **\_関数\_ISOCH\_転送\_を使用して**\_にチェーン化します。

## <a name="span-idsee_alsospansee-also"></a><span id="see_also"></span>関連項目


[ユニバーサル シリアル バス (USB)](https://docs.microsoft.com/windows-hardware/drivers/)

 

 




