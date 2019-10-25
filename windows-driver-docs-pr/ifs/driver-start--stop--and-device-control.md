---
title: ドライバーの開始、停止、デバイス制御
description: ドライバーの開始、停止、デバイス制御
ms.assetid: d3608a5f-3bf4-43b1-8c32-55a6fcd4fbe8
keywords:
- ミニリダイレクター WDK、開始
- ミニリダイレクター WDK、停止
- ミニリダイレクター WDK、デバイスコントロール
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 65019dffc8a5d0189a57a9666b4164fd03eea8db
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72841431"
---
# <a name="driver-start-stop-and-device-control"></a>ドライバーの開始、停止、デバイス制御


ドライバーの登録は、ネットワークミニリダイレクタードライバーの**Driverentry**ルーチンで処理されます。 ネットワークミニリダイレクターが最初に起動したとき (その**Driverentry**ルーチン内)、ドライバーは RDBSS [**RxRegisterMinirdr**](https://docs.microsoft.com/windows-hardware/drivers/ddi/mrx/nf-mrx-rxregisterminirdr)ルーチンを呼び出して、ネットワークミニリダイレクターを RDBSS に登録する必要があります。 ネットワークミニリダイレクターは、構成データと、ネットワークミニリダイレクタードライバーが実装するルーチンへのルーチンポインター (ディスパッチテーブル) のテーブルを含む MINIRDR\_ディスパッチ構造体を渡します。

ドライバーを開始および停止できるようにするには、 [**MRxStart**](https://docs.microsoft.com/windows-hardware/drivers/ddi/mrx/nc-mrx-pmrx_calldown_ctx)ルーチンと[**MRxStop**](https://docs.microsoft.com/windows-hardware/drivers/ifs/mrxstop)ルーチンをネットワークミニリダイレクタードライバーで実装する必要があります。

ネットワークミニリダイレクターを開始または停止する順序は複雑です。 通常、このシーケンスは、管理と管理の目的でドライバーを制御するために、ネットワークミニリダイレクタードライバーで提供されるユーザーモードアプリケーションまたはサービスによって開始されます。 ネットワークミニリダイレクターは、オペレーティングシステムの起動時に自動的に開始するように構成されているサービスを使用できます。 このサービスは、オペレーティングシステムが起動するたびにネットワークミニリダイレクターを開始するように要求できます。

[**MRxStart**](https://docs.microsoft.com/windows-hardware/drivers/ddi/mrx/nc-mrx-pmrx_calldown_ctx)は、 [**RxStartMinirdr**](https://docs.microsoft.com/windows-hardware/drivers/ddi/mrx/nf-mrx-rxstartminirdr)ルーチンが呼び出されたときに RDBSS によって呼び出されます。 **RxStartMinirdr**ルーチンは、通常、ユーザーモードのアプリケーションまたはサービスからの FSCTL または IOCTL 要求の結果として、ネットワークミニリダイレクターを開始するために呼び出されます。 [**RxRegisterMinirdr**](https://docs.microsoft.com/windows-hardware/drivers/ddi/mrx/nf-mrx-rxregisterminirdr)への呼び出しが成功した後、ネットワークミニリダイレクターの**driverentry**ルーチンから**RxStartMinirdr**を呼び出すことはできません。一部の開始処理では、ドライバーの初期化が必要になるためです。完了. **RxStartMinirdr**呼び出しが受信されると、RDBSS はネットワークミニリダイレクターの**MRxStart**ルーチンを呼び出すことによって開始プロセスを完了します。 **MRxStart**を呼び出すと成功が返された場合、RDBSS は RDBSS 内のミニリダイレクターの内部状態を RDBSS\_開始に設定します。

[**MRxStop**](https://docs.microsoft.com/windows-hardware/drivers/ifs/mrxstop)は、 [**RxStopMinirdr**](https://docs.microsoft.com/windows-hardware/drivers/ddi/mrx/nf-mrx-rxstopminirdr)ルーチンが呼び出されたときに RDBSS によって呼び出されます。 RDBSS **RxStopMinirdr**ルーチンは、通常、ユーザーモードのアプリケーションまたはサービスからの FSCTL または IOCTL 要求の結果として、ネットワークミニリダイレクターを停止するために呼び出されます。 この呼び出しは、ネットワークミニリダイレクターから行うことも、オペレーティングシステムによるシャットダウンプロセスの一部として行うこともできます。 **RxStopMinirdr**呼び出しが受信されると、RDBSS はネットワークミニリダイレクターの**MRxStop**ルーチンを呼び出してプロセスを完了します。

[**MRxDevFcbXXXControlFile**](https://docs.microsoft.com/windows-hardware/drivers/ifs/mrxdevfcbxxxcontrolfile)ルーチンは、デバイス FCB で IOCTL または FSCTL 呼び出しを行うことにより、ユーザーモードのアプリケーションまたはサービスからの要求を受信し、ネットワークミニリダイレクターを制御するために使用されます。

また、driver オブジェクトに対して IOCTL および FSCTL 操作を処理する低 i/o ルーチンが2つあります。 [**MRxLowIOSubmit\[lowio\_OP\_FSCTL\]** ](https://msdn.microsoft.com/library/windows/hardware/ff550709)および[**MRxLowIOSubmit\[LOWIO\_OP\_IOCTL @no__t11_** ](https://msdn.microsoft.com/library/windows/hardware/ff550715)

ネットワークミニリダイレクターは、これらの低 i/o ルーチンを使用して、ユーザーモードのアプリケーションまたはサービスからネットワークミニリダイレクターの制御と管理を行うこともできます。

次の表に、開始、停止、デバイス制御操作のためにネットワークミニリダイレクターで実装できるルーチンを示します。

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
<td align="left"><p>RDBSS はこのルーチンを呼び出して、デバイス FCB コントロール要求をネットワークミニリダイレクターに渡します。 RDBSS は、デバイス FCB で IRP_MJ_DEVICE_CONTROL、IRP_MJ_FILE_SYSTEM_CONTROL、または IRP_MJ_INTERNAL_DEVICE_CONTROL を受け取る応答として、この呼び出しを発行します。</p></td>
</tr>
<tr class="even">
<td align="left"><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/mrx/nc-mrx-pmrx_calldown_ctx" data-raw-source="[&lt;strong&gt;MRxStart&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/mrx/nc-mrx-pmrx_calldown_ctx)"><strong>MRxStart</strong></a></td>
<td align="left"><p>RDBSS は、このルーチンを呼び出してネットワークミニリダイレクターを開始します。</p></td>
</tr>
<tr class="odd">
<td align="left"><a href="https://docs.microsoft.com/windows-hardware/drivers/ifs/mrxstop" data-raw-source="[&lt;strong&gt;MRxStop&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ifs/mrxstop)"><strong>MRxStop</strong></a></td>
<td align="left"><p>RDBSS は、このルーチンを呼び出してネットワークミニリダイレクターを停止します。</p></td>
</tr>
</tbody>
</table>

 

 

 




