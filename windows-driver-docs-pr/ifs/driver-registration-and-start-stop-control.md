---
title: ドライバーの登録と開始/停止制御
description: ドライバーの登録と開始/停止制御
ms.assetid: 66f44703-1277-49fe-a481-c8712172db0f
keywords:
- RDBSS WDK ファイルシステム、スタート/停止コントロール
- リダイレクトされたドライブバッファリングサブシステム WDK ファイルシステム、開始/停止コントロール
- スタート/停止コントロールの WDK RDBSS
- RDBSS WDK ファイルシステム、ドライバーの登録
- リダイレクトされたドライブバッファリングサブシステム WDK ファイルシステム、ドライバーの登録
- ドライバーの登録 (WDK RDBSS)
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9d8a1cff9b9082bf5e39a47ef60d02ff4da1fd5d
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72841433"
---
# <a name="driver-registration-and-startstop-control"></a>ドライバーの登録と開始/停止制御


## <span id="ddk_driver_registration_and_start_stop_control_if"></span><span id="DDK_DRIVER_REGISTRATION_AND_START_STOP_CONTROL_IF"></span>


オペレーティングシステムが起動すると、Windows によって、レジストリの設定に基づいて、RDBSS およびすべてのネットワークミニリダイレクタードライバーが読み込まれます。 Rdbsslib を使用して静的にリンクされているモノリシックネットワークミニリダイレクタードライバーの場合、ドライバーは[**RxDriverEntry**](https://docs.microsoft.com/windows-hardware/drivers/ddi/rxprocs/nf-rxprocs-rxdriverentry)ルーチンを[**driverentry**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_initialize)ルーチンから呼び出して、ネットワークにリンクされている rdbsslib ライブラリのコピーを初期化する必要があります。driver. この場合、他の RDBSS ルーチンが呼び出されて使用される前に、 **RxDriverEntry**ルーチンを呼び出す必要があります。 モノリシックではないネットワークミニリダイレクタードライバー (Microsoft SMB リダイレクター) の場合、rdbss デバイスドライバーは、読み込まれると、独自の**Driverentry**ルーチンで初期化されます。

ドライバーがカーネルによって読み込まれ、ドライバーがアンロードされたときに RDBSS で登録解除されると、ネットワークミニリダイレクターは RDBSS に登録します。 ネットワークミニリダイレクターは、RDBSS からエクスポートされた登録ルーチン[**RxRegisterMinirdr**](https://docs.microsoft.com/windows-hardware/drivers/ddi/mrx/nf-mrx-rxregisterminirdr)を呼び出すことによって読み込まれたことを RDBSS に通知します。 この登録プロセスの一環として、ネットワークミニリダイレクターは**RxRegisterMinirdr**にパラメーターを渡します。このパラメーターは、大きな構造体である minirdr\_DISPATCH へのポインターです。 この構造体には、ネットワークミニリダイレクターの構成情報と、ネットワークミニリダイレクターカーネルドライバーによって実装されるコールバックルーチンへのポインターのディスパッチテーブルが含まれています。 RDBSS は、このコールバックルーチンの一覧を使用してネットワークミニリダイレクタードライバーを呼び出します。

[**RxRegisterMinirdr**](https://docs.microsoft.com/windows-hardware/drivers/ddi/mrx/nf-mrx-rxregisterminirdr)ルーチンは、最上位レベルの RDBSS ディスパッチルーチン[**RxFsdDispatch**](https://docs.microsoft.com/windows-hardware/drivers/ddi/mrx/nf-mrx-rxfsddispatch)を指すように、ネットワークミニリダイレクタードライバーのすべてのドライバーディスパッチルーチンを設定します。 ネットワークミニリダイレクターは、独自のエントリポイントを保存し、 **RxRegisterMinirdr**への呼び出しが返された後、またはを呼び出す**ときに特別なパラメーターを設定することにより、この動作をオーバーライドできます。RxRegisterMinirdr**。

ネットワークミニリダイレクタードライバーは、 [**MRxStart**](https://docs.microsoft.com/windows-hardware/drivers/ddi/mrx/nc-mrx-pmrx_calldown_ctx)ルーチンへの呼び出しを受け取るまで、実際には操作を開始しません。これは、minirdr\_ディスパッチ構造体で渡されたコールバックルーチンの1つです。 **MrxStart**コールバックルーチンは、ネットワークミニリダイレクターが独自のドライバーディスパッチエントリポイントを保持しない限り、操作のコールバックルーチンを受信する場合は、ネットワークミニリダイレクタードライバーによって実装される必要があります。 それ以外の場合、RDBSS は、 **MrxStart**が正常に返されるまで、次の i/o 要求パケットだけをドライバーに送信できます。

-   デバイスに対する IRP 要求では、IRPSP の FileObject&gt;のファイル名の長さが0で、FileObject&gt;の関連性のある Fileobject が**NULL**のデバイス操作が作成されます。

その他の IRP 要求では、RDBSS ディスパッチルーチン[**RxFsdDispatch**](https://docs.microsoft.com/windows-hardware/drivers/ddi/mrx/nf-mrx-rxfsddispatch)は\_開始されていない状態\_リダイレクター\_状態の状態を返します。

RDBSS ディスパッチルーチンは、次の i/o 要求パケットに対するすべての要求も失敗します。

-   \_メールスロットを作成\_IRP\_MJ

-   IRP\_MJ\_\_パイプ\_名前を作成します

ネットワークミニリダイレクターによって実装される[**MrxStart**](https://docs.microsoft.com/windows-hardware/drivers/ddi/mrx/nc-mrx-pmrx_calldown_ctx)コールバックルーチンは、 [**RxStartMinirdr**](https://docs.microsoft.com/windows-hardware/drivers/ddi/mrx/nf-mrx-rxstartminirdr)ルーチンが呼び出されたときに RDBSS によって呼び出されます。 RDBSS **RxStartMinirdr**ルーチンは、通常、ネットワークミニリダイレクターを開始するために、ユーザーモードのアプリケーションまたはサービスからのファイルシステム制御コード (FSCTL) または i/o 制御コード (IOCTL) 要求の結果として呼び出されます。 [**RxRegisterMinirdr**](https://docs.microsoft.com/windows-hardware/drivers/ddi/mrx/nf-mrx-rxregisterminirdr)への呼び出しが成功した後、ネットワークミニリダイレクターの[**driverentry**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_initialize)ルーチンから**RxStartMinirdr**を呼び出すことはできません。一部の開始処理では、ドライバーの初期化が必要になるためです。完了. **RxStartMinirdr**呼び出しが受信されると、RDBSS はネットワークミニリダイレクターの**MrxStart**ルーチンを呼び出すことによって開始プロセスを完了します。 **MrxStart**を呼び出すと成功が返された場合、RDBSS は RDBSS 内のミニリダイレクターの内部状態を RDBSS\_開始に設定します。

RDBSS は、 [**RxSetDomainForMailslotBroadcast**](https://docs.microsoft.com/windows-hardware/drivers/ddi/mrx/nf-mrx-rxsetdomainformailslotbroadcast)のルーチンをエクスポートして、メールスロットブロードキャスト用にドメインを設定します。 このルーチンは、ネットワークミニリダイレクターが mailslots をサポートしている場合に、登録時に使用されます。

RDBSS によってエクスポートされた便宜的なルーチン[ **\_\_RxFillAndInstallFastIoDispatch**](https://docs.microsoft.com/windows-hardware/drivers/ddi/mrx/nf-mrx-__rxfillandinstallfastiodispatch)を使用して、i/o 要求処理を同等の高速 i/o ディスパッチに処理するための、すべての IRP\_MJ\_XXX ドライバールーチンポインターをコピーできます。ベクターですが、このルーチンはモノリシックでないドライバーに対してのみ機能します。

また、RDBSS は、ネットワークミニリダイレクターが開始または停止していることを RDBSS に通知するルーチンもエクスポートします。 これらの呼び出しは、ネットワークミニリダイレクターに、リダイレクターを開始および停止するユーザーモード管理サービスまたはユーティリティアプリケーションが含まれている場合に使用されます。 このユーザーモードサービスまたはアプリケーションは、ネットワークミニリダイレクタードライバーにカスタム FSCTL または IOCTL 要求を送信して、開始または停止する必要があることを示すことができます。 リダイレクターは、RDBSS [**RxStartMinirdr**](https://docs.microsoft.com/windows-hardware/drivers/ddi/mrx/nf-mrx-rxstartminirdr)または[**RxStopMinirdr**](https://docs.microsoft.com/windows-hardware/drivers/ddi/mrx/nf-mrx-rxstopminirdr)ルーチンを呼び出して、このネットワークミニリダイレクターを開始または停止するように RDBSS に通知できます。

次の表は、RDBSS ドライバーの登録と開始/停止の制御ルーチンを示しています。

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
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/rxprocs/nf-rxprocs-rxdriverentry" data-raw-source="[&lt;strong&gt;RxDriverEntry&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/rxprocs/nf-rxprocs-rxdriverentry)"><strong>RxDriverEntry</strong></a></p></td>
<td align="left"><p>このルーチンは、RDBSS を初期化するために、 <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_initialize" data-raw-source="[&lt;strong&gt;DriverEntry&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_initialize)"><strong>Driverentry</strong></a>ルーチンからモノリシックネットワークミニリダイレクタードライバーによって呼び出されます。</p>
<p>モノリシックでないドライバーの場合、この初期化ルーチンは、rbss デバイスドライバーの<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_initialize" data-raw-source="[&lt;strong&gt;DriverEntry&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_initialize)"><strong>Driverentry</strong></a>ルーチンに相当します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/mrx/nf-mrx-rxregisterminirdr" data-raw-source="[&lt;strong&gt;RxRegisterMinirdr&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/mrx/nf-mrx-rxregisterminirdr)"><strong>RxRegisterMinirdr</strong></a></p></td>
<td align="left"><p>このルーチンは、ネットワークミニリダイレクタードライバーによって呼び出され、ドライバーを RDBSS に登録します。これにより、登録情報が内部登録テーブルに追加されます。 RDBSS は、ネットワークミニリダイレクター用のデバイスオブジェクトも構築します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/mrx/nf-mrx-rxsetdomainformailslotbroadcast" data-raw-source="[&lt;strong&gt;RxSetDomainForMailslotBroadcast&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/mrx/nf-mrx-rxsetdomainformailslotbroadcast)"><strong>RxSetDomainForMailslotBroadcast</strong></a></p></td>
<td align="left"><p>このルーチンは、mailslots がドライバーでサポートされている場合に、メールスロットブロードキャストに使用されるドメインを設定するために、ネットワークミニリダイレクタードライバーによって呼び出されます。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/mrx/nf-mrx-rxstartminirdr" data-raw-source="[&lt;strong&gt;RxStartMinirdr&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/mrx/nf-mrx-rxstartminirdr)"><strong>RxStartMinirdr</strong></a></p></td>
<td align="left"><p>このルーチンは、を呼び出して自身を登録するネットワークミニリダイレクターを起動します。 また、ドライバーが UNC 名のサポートを示す場合は、RDBSS はネットワークミニリダイレクタードライバーを、MUP と共に UNC プロバイダーとして登録します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/mrx/nf-mrx-rxstopminirdr" data-raw-source="[&lt;strong&gt;RxStopMinirdr&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/mrx/nf-mrx-rxstopminirdr)"><strong>RxStopMinirdr</strong></a></p></td>
<td align="left"><p>このルーチンは、ネットワークミニリダイレクタードライバーを停止します。 停止したドライバーは、IOCTL または FSCTL 要求を除く新しいコマンドを受信しなくなります。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/mrx/nf-mrx-rxpunregisterminirdr" data-raw-source="[&lt;strong&gt;RxpUnregisterMinirdr&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/mrx/nf-mrx-rxpunregisterminirdr)"><strong>RxpUnregisterMinirdr</strong></a></p></td>
<td align="left"><p>このルーチンは、ネットワークミニリダイレクタードライバーによって呼び出され、ドライバーを RDBSS に登録解除し、内部 RDBSS 登録テーブルから登録情報を削除します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/rxstruc/nf-rxstruc-rxunregisterminirdr" data-raw-source="[&lt;strong&gt;RxUnregisterMinirdr&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/rxstruc/nf-rxstruc-rxunregisterminirdr)"><strong>RxUnregisterMinirdr</strong></a></p></td>
<td align="left"><p>このルーチンは、rxstruc で定義されたインライン関数で、RDBSS にドライバーを登録解除し、内部 RDBSS 登録テーブルから登録情報を削除するために、ネットワークミニリダイレクタードライバーによって呼び出されます。 <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/rxstruc/nf-rxstruc-rxunregisterminirdr" data-raw-source="[&lt;strong&gt;RxUnregisterMinirdr&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/rxstruc/nf-rxstruc-rxunregisterminirdr)"><strong>RxUnregisterMinirdr</strong></a> inline 関数は、内部的に<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/mrx/nf-mrx-rxpunregisterminirdr" data-raw-source="[&lt;strong&gt;RxpUnregisterMinirdr&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/mrx/nf-mrx-rxpunregisterminirdr)"><strong>RxpUnregisterMinirdr</strong></a>を呼び出します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/mrx/nf-mrx-__rxfillandinstallfastiodispatch" data-raw-source="[&lt;strong&gt;__RxFillAndInstallFastIoDispatch&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/mrx/nf-mrx-__rxfillandinstallfastiodispatch)"><strong>__RxFillAndInstallFastIoDispatch</strong></a></p></td>
<td align="left"><p>このルーチンは、通常のディスパッチ i/o ベクターと同一の高速 i/o ディスパッチベクターを入力し、渡されたデバイスオブジェクトに関連付けられた driver オブジェクトにインストールします。</p></td>
</tr>
</tbody>
</table>

 

次のマクロは、これらのルーチンの1つを呼び出す mrx .h ヘッダーファイルで定義されています。 通常、このマクロは、 [ **\_\_RxFillAndInstallFastIoDispatch**](https://docs.microsoft.com/windows-hardware/drivers/ddi/mrx/nf-mrx-__rxfillandinstallfastiodispatch)ルーチンを直接呼び出す代わりに使用されます。

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
<td align="left"><p><strong>RxFillAndInstallFastIoDispatch</strong>(<em>__ devobj</em>, <em>__ fa</em>)</p></td>
<td align="left"><p>このマクロは、 <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/mrx/nf-mrx-__rxfillandinstallfastiodispatch" data-raw-source="[&lt;strong&gt;__RxFillAndInstallFastIoDispatch&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/mrx/nf-mrx-__rxfillandinstallfastiodispatch)"><strong>__RxFillAndInstallFastIoDispatch</strong></a>を呼び出して、通常のディスパッチ i/o ベクターと同一の高速 i/o ディスパッチベクターを入力し、渡されたデバイスオブジェクトに関連付けられた driver オブジェクトにインストールします。</p></td>
</tr>
</tbody>
</table>

 

 

 




