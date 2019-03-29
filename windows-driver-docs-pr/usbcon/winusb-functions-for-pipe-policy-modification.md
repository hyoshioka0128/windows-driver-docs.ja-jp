---
Description: Winusb.dll では、パイプの既定のポリシーを取得する WinUsb_GetPipePolicy 関数を公開します。
title: パイプ ポリシー修正のための WinUSB 関数
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: be882716dba12fa59631c16209c695a0d6a5f078
ms.sourcegitcommit: b3859d56cb393e698c698d3fb13519ff1522c7f3
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/05/2019
ms.locfileid: "57349927"
---
# <a name="winusb-functions-for-pipe-policy-modification"></a>パイプ ポリシー修正のための WinUSB 関数


Winusb.dll を公開するアプリケーションを取得およびエンドポイント パイプの既定のポリシー パラメーターの設定を有効にする、 [ **WinUsb\_GetPipePolicy** ](https://msdn.microsoft.com/library/windows/hardware/ff540266)パイプの既定のポリシーを取得します。 [ **WinUsb\_SetPipePolicy** ](https://msdn.microsoft.com/library/windows/hardware/ff540304)関数により、アプリケーションでポリシー パラメーターを新しい値に設定します。

WinUSB は、エンドポイントのパイプにポリシーを適用することで、既定の動作を変更することができます。 これらのポリシーを使用すると、その機能は、デバイスに最適に WinUSB を構成できます。 次の表では、WinUSB でサポートされているパイプ ポリシーの一覧を示します。

**注**  の表で説明されているポリシーは、指定したエンドポイントでのみ有効です。 他のエンドポイント上のポリシーを設定しても、読み取りまたは書き込み要求の WinUSB の動作に影響はありません。

 

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
<th>ポリシーの数</th>
<th>ポリシー名</th>
<th>説明</th>
<th>エンドポイント (の方向)</th>
<th>既定値</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>0x01</td>
<td>SHORT_PACKET_TERMINATE</td>
<td>長さゼロのパケットのバッファーをエンドポイントでサポートされている最大パケット サイズの倍数では、書き込み要求を送信します。</td>
<td><p>(OUT) 一括します。</p>
<p>(OUT) を中断します。</p></td>
<td>FALSE</td>
</tr>
<tr class="even">
<td>0x02</td>
<td>AUTO_CLEAR_STALL</td>
<td>データ フローを停止することがなく停止しているパイプが自動的にクリアします。</td>
<td><p>一括 (IN)</p>
<p>割り込み (IN)</p></td>
<td>FALSE</td>
</tr>
<tr class="odd">
<td>0x03</td>
<td>PIPE_TRANSFER_TIMEOUT</td>
<td>タイムアウト期間 (ミリ秒単位)、要求をキャンセルする前に待機します。</td>
<td><p>一括 (IN)</p>
<p>(OUT) 一括します。</p>
<p>割り込み (IN)</p>
<p>(OUT) を中断します。</p></td>
<td>コントロールの 5 秒間 (5000 ミリ秒)他のユーザーの場合は 0</td>
</tr>
<tr class="even">
<td>0x04</td>
<td>IGNORE_SHORT_PACKETS</td>
<td>短いパケットが受信されるか、読み取るバイト数と、読み取り要求を完了します。 ファイル サイズが不明な場合は、短いパケットを要求が終了しました。</td>
<td><p>一括 (IN)</p>
<p>割り込み (IN)</p></td>
<td>FALSE</td>
</tr>
<tr class="odd">
<td>0x05</td>
<td>ALLOW_PARTIAL_READS</td>
<td>呼び出し元によって要求された以上のデータを返すデバイスからの読み取り要求を許可します。</td>
<td><p>一括 (IN)</p>
<p>割り込み (IN)</p></td>
<td>TRUE</td>
</tr>
<tr class="even">
<td>0x06</td>
<td>AUTO_FLUSH</td>
<td>読み取り要求から余分なデータを保存し、次の読み取り要求に追加します。 または余分なデータを破棄します。</td>
<td><p>一括 (IN)</p>
<p>割り込み (IN)</p></td>
<td>FALSE</td>
</tr>
<tr class="odd">
<td>0x07</td>
<td>RAW_IO</td>
<td>キューのバイパスとエラー処理を複数の読み取り要求のパフォーマンスを向上させます。</td>
<td><p>一括 (IN)</p>
<p>割り込み (IN)</p></td>
<td>FALSE</td>
</tr>
<tr class="even">
<td>0x08</td>
<td>MAXIMUM_TRANSFER_SIZE</td>
<td>WinUSB でサポートされている USB 転送の最大サイズを取得します。 これは、読み取り専用のポリシーで、呼び出すことによって取得できる<a href="https://msdn.microsoft.com/library/windows/hardware/ff540266" data-raw-source="[&lt;strong&gt;WinUsb_GetPipePolicy&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff540266)"> <strong>WinUsb_GetPipePolicy</strong></a>します。</td>
<td><p>一括 (IN)</p>
<p>(OUT) 一括します。</p>
<p>割り込み (IN)</p>
<p>(OUT) を中断します。</p></td>
<td></td>
</tr>
<tr class="odd">
<td>0x09</td>
<td>RESET_PIPE_ON_RESUME</td>
<td>新しい要求を受け入れる前に中断から再開した後、エンドポイントのパイプをリセットします。</td>
<td><p>一括 (IN)</p>
<p>(OUT) 一括します。</p>
<p>割り込み (IN)</p>
<p>(OUT) を中断します。</p></td>
<td>FALSE</td>
</tr>
</tbody>
</table>

 

次の表では、各パイプのポリシーを使用する方法のベスト プラクティスを識別し、ポリシーが有効にすると、結果の動作をについて説明します。

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<thead>
<tr class="header">
<th>ポリシー</th>
<th>場合に有効にする.</th>
<th>動作</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>SHORT_PACKET_TERMINATE(0x01)</td>
<td>デバイスでは、長さ 0 のパケットで終了するためにアウト転送が必要です。 ほとんどのデバイスには、この要件はありません。</td>
<td><p>有効になっている場合 (ポリシー パラメーターの値が<strong>TRUE</strong>または 0 以外の場合)、エンドポイントでサポートされている最大パケット サイズの倍数であるすべての書き込み要求の長さ 0 のパケットが続きます。</p>
<p>ホスト コント ローラーにデータを送信した後 WinUSB が長さ 0 のパケットの書き込み要求を送信し、によって作成された要求を完了し、 <a href="https://msdn.microsoft.com/library/windows/hardware/ff540322" data-raw-source="[&lt;strong&gt;WinUsb_WritePipe&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff540322)"> <strong>WinUsb_WritePipe</strong></a>します。</p></td>
</tr>
<tr class="even">
<td>AUTO_CLEAR_STALL</td>
<td>停止している状態で、エンドポイントのままにするために失敗した転送したくない場合。 このポリシーは RAW_IO が無効にすると、エンドポイントに複数の保留中の読み取り要求がある場合にのみです。</td>
<td><ul>
<li><p>有効になっている場合 (ポリシー パラメーターの値が<strong>TRUE</strong>または 0 以外の場合)、停止状態が自動的にクリアします。 このポリシーのパラメーターは、コントロールのパイプには影響しません。</p>
<p>場合読み取りの要求が失敗し、ホスト コント ローラーに STATUS_CANCELLED または STATUS_DEVICE_NOT_CONNECTED 以外の状態が返されます、WinUSB は、失敗した要求を完了する前に、パイプをリセットします。 パイプをリセットするデータ フローを中断することがなく失速条件をクリアします。 データ転送の新しいデバイスから到着する限り、エンドポイントでフローし続けます。 新しい転送には、いずれかの停止が発生したときにキューにあったを含めることができます。</p>
<p>このポリシーを有効にしても、パフォーマンスが大幅に影響はありません。</p></li>
<li>無効になっている場合 (ポリシー パラメーターの値が<strong>FALSE</strong>または 0)、呼び出し元が呼び出すことによって、エンドポイントのパイプを手動でリセットされるまで、遅延の転送後、エンドポイントに到着するすべての転送が失敗する<a href="https://msdn.microsoft.com/library/windows/hardware/ff540300" data-raw-source="[&lt;strong&gt;WinUsb_ResetPipe&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff540300)"> <strong>WinUsb_ResetPipe</strong></a>します。</li>
</ul></td>
</tr>
<tr class="odd">
<td>PIPE_TRANSFER_TIMEOUT</td>
<td>特定の時間内に完了のエンドポイントに転送されるはずです。</td>
<td><ul>
<li>0 (既定値) に設定すると、転送がタイムアウトしないホスト コント ローラーは、転送をキャンセルしていないためです。 この場合、転送は、手動で取り消されるか、転送が正常完了するまで無期限に待機します。</li>
<li><p>かどうかは 0 以外の値 (タイムアウト間隔) に設定すると、ホスト コント ローラーのタイマーが開始転送要求を受信するとします。 タイマーがタイムアウト間隔を超えているときに、要求が取り消されました。</p>
<p>タイマーの管理のため、わずかにパフォーマンスの低下が発生します。</p>
<div class="alert">
<strong>注</strong>  要求 WinUSB キューで待機中にタイムアウトしないをしないでください。
<p>Windows Vista での転送を有効になっている RAW_IO)、(を除くすべての転送 WinUSB 要求をキュー送信先エンドポイントに前のすべての転送が完了するまでです。 ホスト コント ローラーでは、タイムアウト間隔の計算でキューの時間は含まれません。</p>
<p>有効になっている RAW_IO、WinUSB は要求をキューされません。 代わりに、USB スタックに直接要求を渡す USB スタックが前の転送の処理でビジー状態かどうか。 USB スタックがビジー状態の場合、新しい要求の処理を遅延することができます。 タイムアウトが生じることに注意してください。</p>
</div>
<div>
 
</div></li>
</ul></td>
</tr>
<tr class="even">
<td>IGNORE_SHORT_PACKETS</td>
<td>RAW_IO が無効になり、読み取り要求を完了する短いパケットしたくないです。</td>
<td><ul>
<li>有効になっている場合 (ポリシー パラメーターの値が<strong>TRUE</strong>または 0 以外の場合)、ユーザーは短いパケットを受信した後すぐには、ホスト コント ローラーには、読み取り操作は完了しません。 代わりに、場合にのみ操作を実行します。
<ul>
<li>エラーが発生します。</li>
<li>要求が取り消されました。</li>
<li>要求されたすべてのバイトを受信するとします。</li>
</ul></li>
<li>無効になっている場合 (ポリシー パラメーターの値が<strong>FALSE</strong>または 0)、ホスト コント ローラーに要求されたバイト数を読み取りまたは短いパケットが受信した後に、読み取り操作を完了します。</li>
</ul></td>
</tr>
<tr class="odd">
<td>ALLOW_PARTIAL_READS</td>
<td>デバイスは、要求された以上のデータを送信できます。 これは、要求、バッファーのサイズが最大のエンドポイントのパケット サイズの倍数である場合に可能です。
<p>アプリケーションが読み取りの合計バイト数を決定するいくつかのバイトを読み取る必要がある場合に使用します。</p></td>
<td><ul>
<li>無効になっている場合 (ポリシー パラメーターの値が<strong>FALSE</strong>または 0) WinUSB がエラーで要求を完了すると、デバイスが要求された以上のデータを返します。</li>
<li><p>有効になっている場合 (ポリシー パラメーターの値が<strong>TRUE</strong>または 0 以外の場合) と、デバイスが要求された以上のデータを返します WinUSB (AUTO_FLUSH 設定) に応じて追加、余分なデータ読み取り要求から [次へ] の読み取りの先頭に要求または超過したデータを破棄します。</p>
<p>有効な場合、WinUSB はすぐに 0 バイトの読み取り要求を正常に完了して、下位のスタックの要求は送信しません。</p></li>
</ul></td>
</tr>
<tr class="even">
<td>AUTO_FLUSH</td>
<td>ALLOW_PARTIAL _READS ポリシーを有効にします。
<p>デバイスが要求しましたより多くのデータを送信し、アプリケーションがその他のデータを必要としません。 これは、要求、バッファーのサイズが最大のエンドポイントのパケット サイズの倍数である場合に可能です。</p></td>
<td><p>AUTO_FLUSH は、ALLOW_PARTIAL_READS が有効にすると、WinUSB の動作を定義します。 ALLOW_PARTIAL_READS が無効になっている場合 WinUSB AUTO_FLUSH 値は無視されます。</p>
<p>WinUSB する残りのデータを破棄するか、呼び出し元の次の読み取り要求を送信します。</p>
<ul>
<li>有効になっている場合 (ポリシー パラメーターの値が<strong>TRUE</strong>または 0 以外の場合)、WinUSB がエラー コードなしの追加のバイトを破棄します。</li>
<li>無効になっている場合 (ポリシー パラメーターの値が<strong>FALSE</strong>または 0)、WinUSB は、追加のバイトを保存し、呼び出し元の次の読み取り要求の先頭に追加し、次の読み取り操作の呼び出し元に、データを送信します。</li>
</ul></td>
</tr>
<tr class="odd">
<td>RAW_IO</td>
<td>パフォーマンスが優先度をし、アプリケーションが同じエンドポイントに同時の読み取り要求を送信します。
<p>RAW_IO で呼び出し元によって渡されるバッファーに対して特定の制限は、 <a href="https://msdn.microsoft.com/library/windows/hardware/ff540297" data-raw-source="[&lt;strong&gt;WinUsb_ReadPipe&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff540297)"> <strong>WinUsb_ReadPipe</strong></a>:</p>
<ul>
<li>バッファーの長さは、エンドポイントの最大パケット サイズの倍数である必要があります。</li>
<li>長さはによって取得された MAXIMUM_TRANSFER_SIZE の値未満である必要があります<a href="https://msdn.microsoft.com/library/windows/hardware/ff540266" data-raw-source="[&lt;strong&gt;WinUsb_GetPipePolicy&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff540266)"> <strong>WinUsb_GetPipePolicy</strong></a>します。</li>
</ul></td>
<td><p>有効な場合、キューと複数の読み取り要求のパフォーマンスを向上させるための処理エラーの転送をバイパスします。 WinUSB ハンドルは、次のような要求を表示します。</p>
<ul>
<li>エンドポイントの最大パケット サイズの倍数でない要求は失敗します。</li>
<li>WinUSB でサポートされる最大転送サイズよりも大きい要求は失敗します。</li>
<li>整形式のすべての要求は、すぐにホスト コント ローラーでスケジュールされるを USB core スタックに送信します。</li>
</ul>
大幅に、この設定を有効にすると、最後のパケットの転送は 1 つと、[次へ] の転送の最初のパケットの間の遅延を減らすことで複数の読み取り要求のパフォーマンスが向上します。</td>
</tr>
<tr class="even">
<td>RESET_PIPE_ON_RESUME</td>
<td>デバイスでは、そのデータのトグル状態は保持されません間で中断します。</td>
<td>中断から再開、WinUSB は、新しい要求をエンドポイントに送信する呼び出し元を許可する前に、エンドポイントをリセットします。</td>
</tr>
</tbody>
</table>

 

## <a name="related-topics"></a>関連トピック
[WinUSB 電源管理](winusb-power-management.md)  
[WinUSB アーキテクチャとモジュール](winusb-architecture.md)  
[USB クライアント ドライバーを開発するためのドライバー モデルの選択](winusb-considerations.md)  
[WinUSB (Winusb.sys) のインストール](winusb-installation.md)  
[WinUSB 関数を使用して、USB デバイスにアクセスする方法](using-winusb-api-to-communicate-with-a-usb-device.md)  
[WinUSB 関数](https://msdn.microsoft.com/library/windows/hardware/ff540046#winusb)  
[**WinUsb\_GetPipePolicy**](https://msdn.microsoft.com/library/windows/hardware/ff540266)  
[**WinUsb\_SetPipePolicy**](https://msdn.microsoft.com/library/windows/hardware/ff540304)  
[WinUSB](winusb.md)  



