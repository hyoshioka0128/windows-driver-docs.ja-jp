---
title: バグ チェック 0x144 BUGCODE_USB3_DRIVER
description: BUGCODE_USB3_DRIVER のバグ チェックでは、0x00000144 の値を持ちます。 これは、すべての USB 3 のバグ チェックに使用されるコードです。
ms.assetid: 39414287-3E20-405B-846A-B7F9F8AEE078
keywords:
- バグ チェック 0x144 BUGCODE_USB3_DRIVER
- BUGCODE_USB3_DRIVER
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- BUGCODE_USB3_DRIVER
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: f15c50c5da6354677cd7c6016becdc0f17697519
ms.sourcegitcommit: d03b44343cd32b3653d0471afcdd3d35cb800c0d
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/02/2019
ms.locfileid: "67520162"
---
# <a name="bug-check-0x144-bugcodeusb3driver"></a>バグ チェック 0x144:BUGCODE\_USB3\_ドライバー


**BUGCODE\_USB3\_ドライバー**バグ チェックが 0x00000144 の値を持ちます。 これは、すべての USB 3 のバグ チェックに使用されるコードです。 パラメーター 1 は、USB 3 のバグ チェックの種類を指定し、その他のパラメーターの意味では、パラメーター 1 に依存します。

> [!IMPORTANT]
> このトピックはプログラマーを対象としています。 コンピューターを使用しているときに、エラー コードがブルー スクリーンが受信した顧客の場合を参照してください。[トラブルシューティング ブルー スクリーン エラー](https://www.windows.com/stopcode)します。


## <a name="bugcodeusb3driver-parameters"></a>BUGCODE\_USB3\_ドライバーのパラメーター


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
<td align="left"><p>0x1</p></td>
<td align="left"><p>(省略可能)。 IRP へのポインター、URB を再送信するために使用</p></td>
<td align="left"><p>URB へのポインター</p></td>
<td align="left"><p>クライアント ドライバーのデバイス オブジェクトへのポインター</p></td>
<td align="left"><p>クライアント ドライバーでは、core スタックすることが以前に送信する、URB を使用します。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x2</p></td>
<td align="left"><p>ブート デバイスの物理デバイス オブジェクト (PDO) へのポインター</p></td>
<td align="left"><p>予約済み</p></td>
<td align="left"><p>予約済み</p></td>
<td align="left"><p>ブートまたはページングのデバイスは再列挙に失敗しました。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x3</p></td>
<td align="left"><p>(省略可能)。 IRP へのポインター、URB を送信するために使用</p></td>
<td align="left"><p>破損した URB へのポインター</p></td>
<td align="left"><p>クライアント ドライバーのデバイス オブジェクトへのポインター</p></td>
<td align="left"><p>クライアント ドライバーでは、core スタックに破損した URB が送信されます。 クライアント ドライバーを使用して、URB も割り当てられませんでしたので、これに<strong>USBD_<em>xxx</em>UrbAllocate</strong>またはクライアント ドライバーが、バッファー アンダーラン URB の。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x800</p></td>
<td align="left"><p>IRQL は静的、開いているストリーム要求の送信</p></td>
<td align="left"><p>開いている静的ストリーム IRP へのポインター</p></td>
<td align="left"><p>クライアント ドライバーのデバイス オブジェクトへのポインター</p></td>
<td align="left"><p>IRQL で、静的、開いているストリームの要求が送信された&gt;パッシブ レベル。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x801</p></td>
<td align="left"><p>開いている静的ストリーム IRP へのポインター</p></td>
<td align="left"><p>開いている静的ストリーム URB へのポインター</p></td>
<td align="left"><p>クライアント ドライバーのデバイス オブジェクトへのポインター</p></td>
<td align="left"><p>クライアント ドライバーでは、ストリームの機能のクエリを実行する前に静的ストリームを開こうとしました。 クライアント ドライバー開くことができませんまで静的ストリーム後に正常にストリームの機能のためのクエリ。 詳細については、「解説」を参照してください。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x802</p></td>
<td align="left"><p>クライアント ドライバーを開こうとした静的のストリームの数</p></td>
<td align="left"><p>クライアント ドライバーに与えられていた静的ストリームの数</p></td>
<td align="left"><p>クライアント ドライバーのデバイス オブジェクトへのポインター</p></td>
<td align="left"><p>クライアント ドライバーでは、静的なストリームの数が無効を開こうとしました。 ストリームの数は 0 にすることはできませんし、クエリ機能の呼び出しを USB クライアント ドライバーに返される値より大きくすることはできません。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x803</p></td>
<td align="left"><p>開いている静的ストリーム IRP へのポインター</p></td>
<td align="left"><p>開いている静的ストリーム URB へのポインター</p></td>
<td align="left"><p>クライアント ドライバーのデバイス オブジェクトへのポインター</p></td>
<td align="left"><p>クライアント ドライバーは、静的なストリームを開く、静的なストリームが既に存在するエンドポイントを開こうとしました。 静的ストリームを開く前に、クライアント ドライバーは、以前に開かれた静的ストリームを閉じる必要があります。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x804</p></td>
<td align="left"><p>漏洩したハンドル コンテキスト。 実行<strong>! usbanalyze v</strong>漏洩ハンドルと翻訳に関する情報を取得します。 クライアント ドライバーをドライバーの検証を有効にする必要があります。</p></td>
<td align="left"><p>デバイス オブジェクトに渡される <strong><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/usbdlib/nf-usbdlib-usbd_createhandle" data-raw-source="[USBD_CreateHandle](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/usbdlib/nf-usbdlib-usbd_createhandle)">USBD_CreateHandle</a></strong>します。</p></td>
<td align="left"><p>予約済み</p></td>
<td align="left"><p>使用して作成された、ハンドルを閉じることを忘れた場合、クライアント ドライバー <strong><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/usbdlib/nf-usbdlib-usbd_createhandle" data-raw-source="[USBD_CreateHandle](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/usbdlib/nf-usbdlib-usbd_createhandle)">USBD_CreateHandle</a></strong> URB、割り当てを解放していませんか。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x805</p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/wdf/framework-request-objects" data-raw-source="[WDFREQUEST](https://docs.microsoft.com/windows-hardware/drivers/wdf/framework-request-objects)">WDFREQUEST</a>閉じる静的ストリーム URB の処理</p></td>
<td align="left"><p>閉じる静的ストリーム URB へのポインター</p></td>
<td align="left"><p>クライアント ドライバーのデバイス オブジェクトへのポインター</p></td>
<td align="left"><p>クライアント ドライバーでは、(たとえば、D0 の終了を処理) 後、無効な状態で閉じる静的ストリーム URB を送信します。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x806</p></td>
<td align="left"><p>IRP へのポインター</p></td>
<td align="left"><p>URB へのポインター</p></td>
<td align="left"><p>クライアント ドライバーのデバイス オブジェクトへのポインター</p></td>
<td align="left"><p>クライアント ドライバーが、チェーンを送信しようとしています。 <strong><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/ns-wdm-_mdl" data-raw-source="[MDL](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/ns-wdm-_mdl)">MDL</a></strong>チェーンのクエリを実行する前に<strong>MDL</strong>機能します。 クライアント ドライバーは、連鎖送信できない<strong>MDL</strong> 、チェーンを正常に照会した後まで<strong>MDL</strong>機能します。 詳細については、「解説」を参照してください。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x807</p></td>
<td align="left"><p>連鎖的に呼び出すへのポインター  <strong><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/ns-wdm-_mdl" data-raw-source="[MDL](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/ns-wdm-_mdl)">MDL</a></strong></p></td>
<td align="left"><p>URB へのポインター</p></td>
<td align="left"><p>使用可能な場合に、クライアント ドライバーのデバイス オブジェクトへのポインター</p></td>
<td align="left"><p>クライアント ドライバー、URB に送信、転送 core スタック バッファー長をバイト数よりも長い (によって返される <strong><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-mmgetmdlbytecount" data-raw-source="[MmGetMdlByteCount](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-mmgetmdlbytecount)">MmGetMdlByteCount</a></strong>) の <strong><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/ns-wdm-_mdl" data-raw-source="[MDL](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/ns-wdm-_mdl)">MDL</a></strong>で渡されます。 詳細については、「解説」を参照してください。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x1001</p></td>
<td align="left"><p>XHCI_LIVEDUMP_CONTEXT</p></td>
<td align="left"><p>予約済み</p></td>
<td align="left"><p>予約済み</p></td>
<td align="left"><p>XHCI コント ローラーは、ホスト システムのエラーを示す HSE ビットをアサートします。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x1002</p></td>
<td align="left"><p>XHCI_LIVEDUMP_CONTEXT</p></td>
<td align="left"><p>予約済み</p></td>
<td align="left"><p>予約済み</p></td>
<td align="left"><p>XHCI コント ローラーは、ホスト コント ローラーのエラーを示す HCE ビットをアサートします。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x1003</p></td>
<td align="left"><p>XHCI_LIVEDUMP_CONTEXT</p></td>
<td align="left"><p>予約済み</p></td>
<td align="left"><p>予約済み</p></td>
<td align="left"><p>XHCI stop エンドポイントのコマンドでは、ハンドルされていない終了コードが返されます。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x1004</p></td>
<td align="left"><p>XHCI_LIVEDUMP_CONTEXT</p></td>
<td align="left"><p>予約済み</p></td>
<td align="left"><p>予約済み</p></td>
<td align="left"><p>XHCI のエンドポイントの状態では、xHCI エンドポイントの停止コマンドが実行された後にコンテキストの状態エラーが発生します。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x1005</p></td>
<td align="left"><p>XHCI_LIVEDUMP_CONTEXT</p></td>
<td align="left"><p>予約済み</p></td>
<td align="left"><p>予約済み</p></td>
<td align="left"><p>セットには、ポインターがコントロール エンドポイントの停止をオフの試行中に失敗しましたがキューから削除します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x1006</p></td>
<td align="left"><p>XHCI_LIVEDUMP_CONTEXT</p></td>
<td align="left"><p>予約済み</p></td>
<td align="left"><p>予約済み</p></td>
<td align="left"><p>コントロール エンドポイントの停止をオフにしようとリセット EP に失敗しました。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x1007</p></td>
<td align="left"><p>XHCI_LIVEDUMP_CONTEXT</p></td>
<td align="left"><p>予約済み</p></td>
<td align="left"><p>予約済み</p></td>
<td align="left"><p>中に失敗しました xHCI コント ローラーのリセットでは、復旧をリセットします。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x1008</p></td>
<td align="left"><p>XHCI_LIVEDUMP_CONTEXT</p></td>
<td align="left"><p>予約済み</p></td>
<td align="left"><p>予約済み</p></td>
<td align="left"><p>中に失敗しました xHCI コント ローラーの再起動は、復旧をリセットします。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x1009</p></td>
<td align="left"><p>XHCI_LIVEDUMP_CONTEXT</p></td>
<td align="left"><p>予約済み</p></td>
<td align="left"><p>予約済み</p></td>
<td align="left"><p>XHCI コント ローラーのコマンドをコマンドのタイムアウトを中止後に完了できませんでした。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x100A</p></td>
<td align="left"><p>XHCI_LIVEDUMP_CONTEXT</p></td>
<td align="left"><p>予約済み</p></td>
<td align="left"><p>予約済み</p></td>
<td align="left"><p>エンドポイントの停止完了後にデキュー ポインターの設定の試行中に失敗しましたデキュー ポインターを設定します。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x100B</p></td>
<td align="left"><p>XHCI_LIVEDUMP_CONTEXT</p></td>
<td align="left"><p>予約済み</p></td>
<td align="left"><p>予約済み</p></td>
<td align="left"><p>中に失敗しました xHCI コント ローラーの停止は、復旧をリセットします。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x100C</p></td>
<td align="left"><p>XHCI_LIVEDUMP_CONTEXT</p></td>
<td align="left"><p>予約済み</p></td>
<td align="left"><p>予約済み</p></td>
<td align="left"><p>XHCI コント ローラーのファームウェアがサポートされていません。 ファームウェアを更新しない限り、このコント ローラーで、xHCI ドライバーは読み込まれません。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x100D</p></td>
<td align="left"><p>XHCI_LIVEDUMP_CONTEXT</p></td>
<td align="left"><p>予約済み</p></td>
<td align="left"><p>予約済み</p></td>
<td align="left"><p>物理的に削除するコント ローラーが検出されました。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x100E</p></td>
<td align="left"><p>XHCI_LIVEDUMP_CONTEXT</p></td>
<td align="left"><p>予約済み</p></td>
<td align="left"><p>予約済み</p></td>
<td align="left"><p>ドライバーは、ストリームが有効になっているエンドポイントでエラーを検出します。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x100F</p></td>
<td align="left"><p>XHCI_LIVEDUMP_CONTEXT</p></td>
<td align="left"><p>予約済み</p></td>
<td align="left"><p>予約済み</p></td>
<td align="left"><p>XHCI コント ローラーのファームウェアが切れています。 XHCI ドライバーでは、このコント ローラーの操作を続行しますが、いくつかの問題が遭遇する可能性があります。 ファームウェアの更新をお勧めします。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x1010</p></td>
<td align="left"><p>XHCI_LIVEDUMP_CONTEXT</p></td>
<td align="left"><p>予約済み</p></td>
<td align="left"><p>予約済み</p></td>
<td align="left"><p>転送イベント TRB ハンドルされていない終了コードを正常に完了します。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x1011</p></td>
<td align="left"><p>XHCI_LIVEDUMP_CONTEXT</p></td>
<td align="left"><p>予約済み</p></td>
<td align="left"><p>予約済み</p></td>
<td align="left"><p>コント ローラーは、イベントのリングが満杯を報告します。 コント ローラーは、このような場合にイベントを削除するも呼ばれます。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x1012</p></td>
<td align="left"><p>XHCI_LIVEDUMP_CONTEXT</p></td>
<td align="left"><p>予約済み</p></td>
<td align="left"><p>予約済み</p></td>
<td align="left"><p>コント ローラーには、誤順序のコマンドが完了しました。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x1013</p></td>
<td align="left"><p>XHCI_LIVEDUMP_CONTEXT</p></td>
<td align="left"><p>予約済み</p></td>
<td align="left"><p>予約済み</p></td>
<td align="left"><p>コマンドのリングがデキュー コマンドが完了を中止後、コント ローラーによって報告されたポインターが正しくありません。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x1014</p></td>
<td align="left"><p>XHCI_LIVEDUMP_CONTEXT</p></td>
<td align="left"><p>予約済み</p></td>
<td align="left"><p>予約済み</p></td>
<td align="left"><p>有効にするスロットの完了後にコント ローラーくれました不適切なスロット id。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x1015</p></td>
<td align="left"><p>XHCI_LIVEDUMP_CONTEXT</p></td>
<td align="left"><p>予約済み</p></td>
<td align="left"><p>予約済み</p></td>
<td align="left"><p>コント ローラーには、BSR1 SetAddress コマンドが失敗しました。 予想されるではありません。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x1016</p></td>
<td align="left"><p>XHCI_LIVEDUMP_CONTEXT</p></td>
<td align="left"><p>予約済み</p></td>
<td align="left"><p>予約済み</p></td>
<td align="left"><p>コント ローラーは、usbdevice のリセット中に、スロットを有効にできませんでした。 これは、予期されていません。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x1017</p></td>
<td align="left"><p>XHCI_LIVEDUMP_CONTEXT</p></td>
<td align="left"><p>予約済み</p></td>
<td align="left"><p>予約済み</p></td>
<td align="left"><p>コント ローラーには、エンドポイントが失敗しました。 エンドポイントを deconfiguring 私たちがコマンドを構成します。 予想されるではありません。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x1018</p></td>
<td align="left"><p>XHCI_LIVEDUMP_CONTEXT</p></td>
<td align="left"><p>予約済み</p></td>
<td align="left"><p>予約済み</p></td>
<td align="left"><p>コント ローラーには、無効にするスロットのコマンドが失敗しました。 予想されるではありません。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x1019</p></td>
<td align="left"><p>XHCI_LIVEDUMP_CONTEXT</p></td>
<td align="left"><p>予約済み</p></td>
<td align="left"><p>予約済み</p></td>
<td align="left"><p>コント ローラーには、USB デバイスのリセット コマンドが失敗しました。 予想されるではありません。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x101A</p></td>
<td align="left"><p>XHCI_LIVEDUMP_CONTEXT</p></td>
<td align="left"><p>予約済み</p></td>
<td align="left"><p>予約済み</p></td>
<td align="left"><p>エンドポイントをリセットした後は、デキュー ポインターの設定コマンドが失敗しました。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x101B</p></td>
<td align="left"><p>XHCI_LIVEDUMP_CONTEXT</p></td>
<td align="left"><p>予約済み</p></td>
<td align="left"><p>予約済み</p></td>
<td align="left"><p>XHCI では、ハンドルされていない終了コードが返されたエンドポイントのコマンドをリセットします。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x101C</p></td>
<td align="left"><p>XHCI_LIVEDUMP_CONTEXT</p></td>
<td align="left"><p>予約済み</p></td>
<td align="left"><p>予約済み</p></td>
<td align="left"><p>Xhci D0Entry に失敗しました。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x101D</p></td>
<td align="left"><p>XHCI_LIVEDUMP_CONTEXT</p></td>
<td align="left"><p>予約済み</p></td>
<td align="left"><p>予約済み</p></td>
<td align="left"><p>一時的に削除し、要求のキャンセル中にデキュー ポインターの設定ではなく、エンドポイントの構成コマンドを使用する場合に失敗しました (2 つのコマンド) としてストリームのエンドポイントを追加します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x101E</p></td>
<td align="left"><p>XHCI_LIVEDUMP_CONTEXT</p></td>
<td align="left"><p>予約済み</p></td>
<td align="left"><p>予約済み</p></td>
<td align="left"><p>示された転送の完了が保留中のコント ローラー、コント ローラーにします。 EventData 1 = = (転送イベント TRB のポインターの逆参照が発生しますが、バグチェック)</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x101F</p></td>
<td align="left"><p>XHCI_LIVEDUMP_CONTEXT</p></td>
<td align="left"><p>予約済み</p></td>
<td align="left"><p>予約済み</p></td>
<td align="left"><p>示された転送の完了が保留中のコント ローラー、コント ローラーにします。 EventData = 0 (転送イベントと一致しない TRB の論理アドレス)</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x1020</p></td>
<td align="left"><p>XHCI_LIVEDUMP_CONTEXT</p></td>
<td align="left"><p>予約済み</p></td>
<td align="left"><p>予約済み</p></td>
<td align="left"><p>示された転送の完了が保留中のコント ローラー、コント ローラーにします。 EventData (転送イベントと一致しない TRB の論理アドレス) の 0 を = =、転送イベント TRB 冗長 (最近完了した要求のどこかに近いポイント) があります。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x1021</p></td>
<td align="left"><p>XHCI_LIVEDUMP_CONTEXT</p></td>
<td align="left"><p>予約済み</p></td>
<td align="left"><p>予約済み</p></td>
<td align="left"><p>一時的に削除して (2 つのコマンド) としてストリーム エンドポイントの追加に失敗が停止されていないエンドポイントのリセットの一環としてエンドポイントの構成コマンドを使用する場合。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x1022</p></td>
<td align="left"><p>XHCI_LIVEDUMP_CONTEXT</p></td>
<td align="left"><p>予約済み</p></td>
<td align="left"><p>予約済み</p></td>
<td align="left"><p>削除して、(1 つのコマンド) と同じエンドポイントを追加することができませんでした。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x3000</p></td>
<td align="left"><p>USBHUB3_LIVEDUMP_CONTEXT</p></td>
<td align="left"><p>予約済み</p></td>
<td align="left"><p>予約済み</p></td>
<td align="left"><p>不適切な動作のハブはハブのドライバーが正常にリセットされました。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x3001</p></td>
<td align="left"><p>USBHUB3_LIVEDUMP_CONTEXT</p></td>
<td align="left"><p>予約済み</p></td>
<td align="left"><p>予約済み</p></td>
<td align="left"><p>不適切な動作のハブは、ハブのドライバーによって正常にリセットできませんでした。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x3002</p></td>
<td align="left"><p>USBHUB3_LIVEDUMP_CONTEXT</p></td>
<td align="left"><p>予約済み</p></td>
<td align="left"><p>予約済み</p></td>
<td align="left"><p>関数ではない SuperSpeed ハブは、ハブのドライバーにより無効にされました。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x3003</p></td>
<td align="left"><p>USBHUB3_LIVEDUMP_CONTEXT</p></td>
<td align="left"><p>予約済み</p></td>
<td align="left"><p>予約済み</p></td>
<td align="left"><p>USB デバイスには、列挙が失敗しました。</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>注釈
-------

USB 機能の 1 つのクエリを実行するクライアント ドライバーを呼び出す必要があります[ **WdfUsbTargetDeviceQueryUsbCapability** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfusb/nf-wdfusb-wdfusbtargetdevicequeryusbcapability)または[ **USBD\_QueryUsbCapability**](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/hh406230(v=vs.85))

チェーンを送信する[ **MDL**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/ns-wdm-_mdl)、クライアント ドライバーを呼び出す必要があります[ **USBD\_QueryUsbCapability** ](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/hh406230(v=vs.85))して**URB\_関数\_一括\_OR\_INTERRUPT\_転送\_USING\_連結された\_MDL**または**URB\_関数\_アイソクロナス\_転送\_USING\_連結された\_MDL**します。

## <a name="span-idseealsospansee-also"></a><span id="see_also"></span>参照してください。


[ユニバーサル シリアル バス (USB)](https://docs.microsoft.com/windows-hardware/drivers/)

 

 




