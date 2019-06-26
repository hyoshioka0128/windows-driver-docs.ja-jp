---
title: ドライバーの開始、停止、デバイス制御
description: ドライバーの開始、停止、デバイス制御
ms.assetid: d3608a5f-3bf4-43b1-8c32-55a6fcd4fbe8
keywords:
- ミニ リダイレクター WDK、開始
- ミニ リダイレクター WDK、停止しています
- ミニ リダイレクター WDK、デバイスのコントロール
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 15b53fc50e8a1b5b1c314a9e1dc239f797dfa7c5
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67386096"
---
# <a name="driver-start-stop-and-device-control"></a>ドライバーの開始、停止、デバイス制御


ドライバーの登録の処理、 **DriverEntry**ネットワーク ミニ リダイレクター ドライバーの日常的な。 ネットワークのミニ リダイレクターが初めて起動するときに (でその**DriverEntry**ルーチン)、ドライバーは、RDBSS を呼び出す必要があります[ **RxRegisterMinirdr** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/mrx/nf-mrx-rxregisterminirdr)ルーチンは、ネットワークを登録するにはミニ リダイレクター RDBSS とします。 ネットワーク ミニリダイレクター渡します、MINIRDR\_ネットワーク ミニ リダイレクター ドライバーを実装するルーチンに構成データと日常的なポインター (ディスパッチ テーブル) のテーブルを含む構造体をディスパッチします。

[ **MRxStart** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/mrx/nc-mrx-pmrx_calldown_ctx)と[ **MRxStop** ](https://docs.microsoft.com/windows-hardware/drivers/ifs/mrxstop)するドライバを許可するネットワーク ミニ リダイレクター ドライバーによってルーチンを実装する必要があります開始および停止します。

シーケンスを開始または停止するネットワークのミニ リダイレクターは複雑です。 このシーケンスは通常、管理、および管理のためのドライバーを制御するには、ユーザー モード アプリケーションまたはネットワーク ミニ リダイレクター ドライバーに付属しているサービスによって開始されます。 ネットワークのミニ リダイレクターは、オペレーティング システムの起動時に自動的に開始するように構成されたサービスを使用できます。 このサービスは、オペレーティング システムが起動されるたびに、ネットワークのミニ リダイレクターが開始されることを要求できます。

[**MRxStart** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/mrx/nc-mrx-pmrx_calldown_ctx) RDBSS によって呼び出されるときに、 [ **RxStartMinirdr** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/mrx/nf-mrx-rxstartminirdr)ルーチンが呼び出されます。 **RxStartMinirdr**ルーチンが、FSCTL または IOCTL 要求の結果としてネットワーク ミニリダイレクターを開始するには、ユーザー モード アプリケーションまたはサービスから通常呼び出されます。 呼び出し**RxStartMinirdr**から行ったことはできません、 **DriverEntry**ネットワークのミニ リダイレクターに成功した呼び出しの後の日常的な[ **RxRegisterMinirdr**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/mrx/nf-mrx-rxregisterminirdr)いくつかの処理を開始は、ドライバーの初期化が完了する必要があるためです。 1 回、 **RxStartMinirdr**呼び出しが受信される、RDBSS が呼び出すことにより、起動プロセスを完了、 **MRxStart**ネットワーク ミニ リダイレクターのルーチンです。 場合に呼び出し**MRxStart**を返します。 成功すると、RDBSS RDBSS に RDBSS でミニ リダイレクターの内部状態を設定する\_開始します。

[**MRxStop** ](https://docs.microsoft.com/windows-hardware/drivers/ifs/mrxstop) RDBSS によって呼び出されるときに、 [ **RxStopMinirdr** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/mrx/nf-mrx-rxstopminirdr)ルーチンが呼び出されます。 RDBSS **RxStopMinirdr**ルーチンが、FSCTL または IOCTL 要求の結果としてネットワーク ミニリダイレクターを停止するには、ユーザー モード アプリケーションまたはサービスから通常呼び出されます。 オペレーティング システムによってネットワーク ミニリダイレクターからか、シャット ダウン プロセスの一部としてこの呼び出しを実行もできます。 1 回、 **RxStopMinirdr**呼び出しが受信される、RDBSS の呼び出すことによって、プロセスが完了すると、 **MRxStop**ネットワーク ミニ リダイレクターの日常的な。

[ **MRxDevFcbXXXControlFile** ](https://docs.microsoft.com/windows-hardware/drivers/ifs/mrxdevfcbxxxcontrolfile) FCB のデバイスで IOCTL または FSCTL 呼び出しを行うと、ネットワークのミニ リダイレクターを制御するには、ユーザー モード アプリケーションまたはサービスから要求を受信するルーチンを使用します。

さらに、これにはドライバー オブジェクトの IOCTL と FSCTL の操作を処理する 2 つの低 I/O ルーチンがあります。[**MRxLowIOSubmit\[LOWIO\_OP\_FSCTL\]**  ](https://msdn.microsoft.com/library/windows/hardware/ff550709)と[ **MRxLowIOSubmit\[LOWIO\_OP\_IOCTL\]** ](https://msdn.microsoft.com/library/windows/hardware/ff550715)します。

ネットワークのミニ リダイレクターでは、ユーザー モード アプリケーションまたはサービスからネットワークのミニ リダイレクターの制御と管理を提供するのにこれらの低い I/O ルーチンも使用できます。

次の表では、開始、停止、およびデバイスの管理操作のネットワーク ミニ リダイレクターで実装できるルーチンを示します。

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
<td align="left"><a href="https://docs.microsoft.com/windows-hardware/drivers/ifs/mrxdevfcbxxxcontrolfile" data-raw-source="[&lt;strong&gt;MRxDevFcbXXXControlFile&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ifs/mrxdevfcbxxxcontrolfile)"><strong>MRxDevFcbXXXControlFile</strong></a></td>
<td align="left"><p>RDBSS では、ネットワークのミニ リダイレクターにデバイス FCB のコントロール要求を渡すには、このルーチンを呼び出します。 RDBSS は、FCB のデバイスで、IRP_MJ_DEVICE_CONTROL、IRP_MJ_FILE_SYSTEM_CONTROL、または IRP_MJ_INTERNAL_DEVICE_CONTROL を受け取るへの応答には、この呼び出しを発行します。</p></td>
</tr>
<tr class="even">
<td align="left"><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/mrx/nc-mrx-pmrx_calldown_ctx" data-raw-source="[&lt;strong&gt;MRxStart&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/mrx/nc-mrx-pmrx_calldown_ctx)"><strong>MRxStart</strong></a></td>
<td align="left"><p>RDBSS では、ネットワークのミニ リダイレクターを開始するには、このルーチンを呼び出します。</p></td>
</tr>
<tr class="odd">
<td align="left"><a href="https://docs.microsoft.com/windows-hardware/drivers/ifs/mrxstop" data-raw-source="[&lt;strong&gt;MRxStop&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ifs/mrxstop)"><strong>MRxStop</strong></a></td>
<td align="left"><p>RDBSS では、ネットワークのミニ リダイレクターを停止するには、このルーチンを呼び出します。</p></td>
</tr>
</tbody>
</table>

 

 

 




