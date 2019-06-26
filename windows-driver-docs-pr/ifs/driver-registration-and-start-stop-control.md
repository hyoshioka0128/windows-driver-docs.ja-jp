---
title: ドライバーの登録と開始/停止制御
description: ドライバーの登録と開始/停止制御
ms.assetid: 66f44703-1277-49fe-a481-c8712172db0f
keywords:
- RDBSS WDK ファイル システムでは、コントロールの開始/停止
- リダイレクトされたサブシステムの WDK のバッファリングをドライブのファイル システム、コントロールの開始/停止
- WDK RDBSS のコントロールの開始/停止
- RDBSS WDK ファイル システム、ドライバーの登録
- リダイレクトされたサブシステムの WDK のバッファリングをドライブのファイル システム、ドライバーの登録
- ドライバー WDK RDBSS の登録
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9318232e9424377594eca0fb83484e9f40ba6199
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67380357"
---
# <a name="driver-registration-and-startstop-control"></a>ドライバーの登録と開始/停止制御


## <span id="ddk_driver_registration_and_start_stop_control_if"></span><span id="DDK_DRIVER_REGISTRATION_AND_START_STOP_CONTROL_IF"></span>


オペレーティング システムを起動すると、Windows は RDBSS とレジストリの設定に基づいてネットワーク ミニ リダイレクター ドライバーを読み込みます。 Rdbsslib.lib を静的にリンクされているモノリシック ネットワーク ミニ リダイレクター ドライバーのドライバーを呼び出す必要があります、 [ **RxDriverEntry** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/rxprocs/nf-rxprocs-rxdriverentry)ルーチンからその[ **DriverEntry** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_initialize)ネットワーク ドライバーとリンクされているルーチン RDBSSLIB ライブラリのコピーを初期化します。 ここで、 **RxDriverEntry** RDBSS 他のルーチンが呼び出され、使用前に、ルーチンを呼び出す必要があります。 独自の非モノリシック ネットワーク ミニ リダイレクター ドライバー (Microsoft SMB リダイレクター) の場合 rdbss.sys デバイス ドライバーが初期化される**DriverEntry**ルーチンが読み込まれるときにします。

ネットワークのミニ リダイレクターは、ドライバーは、カーネルによって読み込まれ、ドライバーが読み込まれると RDBSS で登録を解除します RDBSS を登録します。 ネットワークのミニ リダイレクターに通知を呼び出して読み込まれた RDBSS [ **RxRegisterMinirdr**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/mrx/nf-mrx-rxregisterminirdr)、RDBSS から登録ルーチンをエクスポートします。 この登録プロセスの一環として、ネットワークのミニ リダイレクターにパラメーターを渡します**RxRegisterMinirdr** MINIRDR 大きな構造体へのポインターは\_ディスパッチします。 この構造体には、ネットワークのミニ リダイレクターとネットワークのミニ リダイレクター カーネル ドライバーによって実装されるコールバック ルーチンへのポインターのディスパッチ テーブルの構成情報が含まれています。 RDBSS は、このコールバック ルーチンの一覧を使ってネットワーク ミニ リダイレクター ドライバーに呼び出しを行います。

[ **RxRegisterMinirdr** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/mrx/nf-mrx-rxregisterminirdr)ルーチンすべてドライバーの設定、最上位レベルの RDBSS ディスパッチ ルーチンを指すネットワーク ミニ リダイレクター ドライバーのディスパッチ ルーチン[ **RxFsdDispatch**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/mrx/nf-mrx-rxfsddispatch)します。 ネットワークのミニ リダイレクターは、独自のエントリ ポイントを保存し、呼び出しの後、独自のエントリ ポイントでドライバーのディスパッチをリライトしてこの動作をオーバーライドできます**RxRegisterMinirdr**を返すか、特別なパラメーターを設定してとき呼び出す**RxRegisterMinirdr**します。

ネットワークのミニ リダイレクター ドライバーは開始されません操作の呼び出しを受信するまでその[ **MRxStart** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/mrx/nc-mrx-pmrx_calldown_ctx) 、MINIRDR でのコールバック ルーチンのいずれかのルーチン、渡された\_ディスパッチ。構造体。 **MrxStart**ネットワーク ミニリダイレクター独自ドライバー ディスパッチのエントリ ポイントを保持しない限り、操作のコールバック ルーチンを受信する場合、ネットワーク ミニ リダイレクター ドライバーによってコールバック ルーチンを実装する必要があります。 それ以外の場合、RDBSS はまでドライバーを通じて次 I/O 要求パケットのみ許可**MrxStart**正常に返されます。

-   IRP のデバイスの作成要求とデバイスの操作を FileObject -&gt;、IRPSP で FileName.Length は 0 と FileObject -&gt;RelatedFileObject は**NULL**します。

IRP 要求に対して、RDBSS にディスパッチ ルーチン[ **RxFsdDispatch** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/mrx/nf-mrx-rxfsddispatch)のステータスが返されます\_リダイレクター\_いない\_開始します。

RDBSS ディスパッチ ルーチンは、次の I/O 要求パケットのすべての要求とも失敗します。

-   IRP\_MJ\_作成\_"メール スロット"

-   IRP\_MJ\_作成\_名前付き\_パイプ

[ **MrxStart** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/mrx/nc-mrx-pmrx_calldown_ctx) RDBSS によってネットワーク ミニリダイレクターによって実装されるコールバック ルーチンが呼び出されるときに、 [ **RxStartMinirdr** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/mrx/nf-mrx-rxstartminirdr)ルーチンが呼び出されます。 RDBSS **RxStartMinirdr**ルーチンは、通常、ファイル システムのコントロールのコード (FSCTL) の結果として呼び出されます。 または、ネットワークのミニ リダイレクターを開始するには、ユーザー モード アプリケーションまたはサービスから I/O 制御コード (IOCTL) を要求します。 呼び出し**RxStartMinirdr**から行ったことはできません、 [ **DriverEntry** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_initialize)ネットワークのミニ リダイレクターに成功した呼び出しの後の日常的な[ **RxRegisterMinirdr**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/mrx/nf-mrx-rxregisterminirdr)いくつかの処理を開始は、ドライバーの初期化が完了する必要があるためです。 1 回、 **RxStartMinirdr**呼び出しが受信される、RDBSS が呼び出すことにより、起動プロセスを完了、 **MrxStart**ネットワーク ミニ リダイレクターのルーチンです。 場合に呼び出し**MrxStart**を返します。 成功すると、RDBSS RDBSS に RDBSS でミニ リダイレクターの内部状態を設定する\_開始します。

RDBSS、ルーチンをエクスポートして[ **RxSetDomainForMailslotBroadcast**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/mrx/nf-mrx-rxsetdomainformailslotbroadcast)"メール スロット"ブロードキャスト ドメインを設定します。 このルーチンは、ネットワークのミニ リダイレクター メール スロットをサポートしている場合、登録時に使用されます。

利便性のためのルーチン、 [  **\_ \_RxFillAndInstallFastIoDispatch**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/mrx/nf-mrx-__rxfillandinstallfastiodispatch)、エクスポートされた RDBSS では、すべて IRP のコピーを使用できます\_MJ\_XXX ドライバーI/O 要求の処理に匹敵する高速な I/O を処理するための日常的なポインターのベクトルのディスパッチが、このルーチンは、モノリシック以外のドライバーのみ機能します。

RDBSS には、ネットワークのミニ リダイレクターが開始または停止する RDBSS に通知するルーチンもエクスポートされます。 これらの呼び出しはネットワークのミニ リダイレクターには、ユーザー モードの管理サービスが含まれている場合、使用またはユーティリティ アプリケーションの開始し、停止のリダイレクターです。 このユーザー モード サービスまたはアプリケーションの場合は、ネットワークのミニ リダイレクター ドライバーを開始または停止にする必要がありますを示すために FSCTL または IOCTL のカスタム要求を送信できます。 リダイレクターは、RDBSS を呼び出すことができます[ **RxStartMinirdr** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/mrx/nf-mrx-rxstartminirdr)または[ **RxStopMinirdr** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/mrx/nf-mrx-rxstopminirdr)ルーチンを開始または停止このネットワーク RDBSS に通知するにはミニ リダイレクター。

次の表では、ドライバーの登録と開始/停止を RDBSS 制御ルーチンを示します。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">ルーチン</th>
<th align="left">説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/rxprocs/nf-rxprocs-rxdriverentry" data-raw-source="[&lt;strong&gt;RxDriverEntry&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/rxprocs/nf-rxprocs-rxdriverentry)"><strong>RxDriverEntry</strong></a></p></td>
<td align="left"><p>このルーチンからモノリシック ネットワーク ミニ リダイレクター ドライバーによって呼び出されます。 その<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_initialize" data-raw-source="[&lt;strong&gt;DriverEntry&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_initialize)"> <strong>DriverEntry</strong> </a> RDBSS の初期化ルーチン。</p>
<p>モノリシック以外のドライバーの初期化ルーチンは等しく、 <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_initialize" data-raw-source="[&lt;strong&gt;DriverEntry&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_initialize)"> <strong>DriverEntry</strong> </a> rbss.sys デバイス ドライバーの日常的な。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/mrx/nf-mrx-rxregisterminirdr" data-raw-source="[&lt;strong&gt;RxRegisterMinirdr&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/mrx/nf-mrx-rxregisterminirdr)"><strong>RxRegisterMinirdr</strong></a></p></td>
<td align="left"><p>このルーチンは、RDBSS で、内部の登録の表に、登録情報を追加、ドライバーに登録するネットワーク ミニ リダイレクター ドライバーによって呼び出されます。 RDBSS もネットワーク ミニリダイレクターのデバイス オブジェクトを作成します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/mrx/nf-mrx-rxsetdomainformailslotbroadcast" data-raw-source="[&lt;strong&gt;RxSetDomainForMailslotBroadcast&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/mrx/nf-mrx-rxsetdomainformailslotbroadcast)"><strong>RxSetDomainForMailslotBroadcast</strong></a></p></td>
<td align="left"><p>このルーチンは、メール スロットがドライバーによってサポートされている場合は、メール スロットのブロードキャストを使用するドメインを設定するネットワーク ミニ リダイレクター ドライバーによって呼び出されます。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/mrx/nf-mrx-rxstartminirdr" data-raw-source="[&lt;strong&gt;RxStartMinirdr&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/mrx/nf-mrx-rxstartminirdr)"><strong>RxStartMinirdr</strong></a></p></td>
<td align="left"><p>このルーチンは、自身を登録するために呼び出さネットワーク ・ mini-リダイレクターを開始します。 ドライバーを UNC 名のサポートを示している場合 RDBSS は MUP の UNC プロバイダーとしても、ネットワークのミニ リダイレクター ドライバーを登録します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/mrx/nf-mrx-rxstopminirdr" data-raw-source="[&lt;strong&gt;RxStopMinirdr&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/mrx/nf-mrx-rxstopminirdr)"><strong>RxStopMinirdr</strong></a></p></td>
<td align="left"><p>このルーチンは、ネットワークのミニ リダイレクター ドライバーを停止します。 停止しているドライバーは、IOCTL または FSCTL 要求を除き、新しいコマンドを受けられなくなります。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/mrx/nf-mrx-rxpunregisterminirdr" data-raw-source="[&lt;strong&gt;RxpUnregisterMinirdr&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/mrx/nf-mrx-rxpunregisterminirdr)"><strong>RxpUnregisterMinirdr</strong></a></p></td>
<td align="left"><p>このルーチンは、RDBSS とドライバーの登録を解除し、内部の RDBSS 登録テーブルから登録情報を削除するネットワーク ミニ リダイレクター ドライバーによって呼び出されます。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/rxstruc/nf-rxstruc-rxunregisterminirdr" data-raw-source="[&lt;strong&gt;RxUnregisterMinirdr&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/rxstruc/nf-rxstruc-rxunregisterminirdr)"><strong>RxUnregisterMinirdr</strong></a></p></td>
<td align="left"><p>このルーチンは、RDBSS とドライバーの登録を解除し、内部の RDBSS 登録テーブルから登録情報を削除するネットワーク ミニ リダイレクター ドライバーによって呼び出される rxstruc.h で定義されているインライン関数です。 <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/rxstruc/nf-rxstruc-rxunregisterminirdr" data-raw-source="[&lt;strong&gt;RxUnregisterMinirdr&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/rxstruc/nf-rxstruc-rxunregisterminirdr)"> <strong>RxUnregisterMinirdr</strong> </a>インライン関数を内部的に呼び出します<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/mrx/nf-mrx-rxpunregisterminirdr" data-raw-source="[&lt;strong&gt;RxpUnregisterMinirdr&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/mrx/nf-mrx-rxpunregisterminirdr)"> <strong>RxpUnregisterMinirdr</strong></a>します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/mrx/nf-mrx-__rxfillandinstallfastiodispatch" data-raw-source="[&lt;strong&gt;__RxFillAndInstallFastIoDispatch&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/mrx/nf-mrx-__rxfillandinstallfastiodispatch)"><strong>__RxFillAndInstallFastIoDispatch</strong></a></p></td>
<td align="left"><p>このルーチンは、高速な I/O ディスパッチ ベクトル通常のディスパッチ I/O ベクターと一致するように入力し、渡されるデバイス オブジェクトに関連付けられているドライバー オブジェクトにインストールします。</p></td>
</tr>
</tbody>
</table>

 

次のマクロは、これらのルーチンの 1 つを呼び出す mrx.h ヘッダー ファイルで定義されます。 このマクロを呼び出す代わりに使用は、通常、 [  **\_ \_RxFillAndInstallFastIoDispatch** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/mrx/nf-mrx-__rxfillandinstallfastiodispatch)直接ルーチン。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">マクロ</th>
<th align="left">説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><strong>RxFillAndInstallFastIoDispatch</strong>(<em>__devobj</em>, <em>__fastiodisp</em>)</p></td>
<td align="left"><p>このマクロを呼び出す<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/mrx/nf-mrx-__rxfillandinstallfastiodispatch" data-raw-source="[&lt;strong&gt;__RxFillAndInstallFastIoDispatch&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/mrx/nf-mrx-__rxfillandinstallfastiodispatch)"> <strong>__RxFillAndInstallFastIoDispatch</strong></a>通常のディスパッチ I/O ベクターとそれをドライバー オブジェクトに関連付けられているインストールと一致するよう、高速な I/O ディスパッチ ベクターの入力をデバイス オブジェクトが渡されます。</p></td>
</tr>
</tbody>
</table>

 

 

 




