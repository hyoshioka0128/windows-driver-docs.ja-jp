---
title: SerCx2 オブジェクト ハンドル
description: このトピックでは、シリアル フレームワークの拡張機能 (SerCx2) のバージョン 2 を具体的には定義されているオブジェクトのハンドルの種類について説明します。
ms.localizationpriority: medium
ms.date: 12/27/2018
ms.openlocfilehash: ae9a734f41f3c15b36fde8f2daf456b77525f4d8
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67356778"
---
# <a name="sercx2-object-handles"></a>SerCx2 オブジェクト ハンドル

このトピックでは、シリアル フレームワークの拡張機能 (SerCx2) のバージョン 2 を具体的には定義されているオブジェクトのハンドルの種類について説明します。 SerCx2 デバイス ドライバー インターフェイス (DDI) はこれらは、機能と SerCx2 に固有の機能を持つオブジェクトを参照する型を処理します。

さらに、SerCx2 DDI を使用して 2 つのジェネリック オブジェクト ハンドルの種類を WDFDEVICE と WDFREQUEST、カーネル モード ドライバー フレームワーク (KMDF) では定義されています。 フレームワークのハンドルの種類の詳細については、次を参照してください。 [Framework オブジェクトの概要](https://docs.microsoft.com/windows-hardware/drivers/wdf/summary-of-framework-objects)します。

このトピックでは、次のオブジェクト ハンドルをについて説明します。

* [SERCX2CUSTOMRECEIVE オブジェクト ハンドル](#sercx2customreceive-object-handle)
* [SERCX2CUSTOMRECEIVETRANSACTION オブジェクト ハンドル](#sercx2customreceivetransaction-object-handle)
* [SERCX2CUSTOMTRANSMIT オブジェクト ハンドル](#sercx2customtransmit-object-handle)
* [SERCX2CUSTOMTRANSMITTRANSACTION オブジェクト ハンドル](#sercx2customtransmittransaction-object-handle)
* [SERCX2PIORECEIVE オブジェクト ハンドル](#sercx2pioreceive-object-handle)
* [SERCX2PIOTRANSMIT オブジェクト ハンドル](#sercx2piotransmit-object-handle)
* [SERCX2SYSTEMDMARECEIVE オブジェクト ハンドル](#sercx2systemdmareceive-object-handle)
* [SERCX2SYSTEMDMATRANSMIT オブジェクト ハンドル](#sercx2systemdmatransmit-object-handle)

ヘッダー:2.0\Sercx.h

##  <a name="sercx2customreceive-object-handle"></a>SERCX2CUSTOMRECEIVE オブジェクト ハンドル
A **SERCX2CUSTOMRECEIVE**オブジェクト ハンドルは、シリアル フレームワーク拡張機能 (SerCx2) のバージョン 2 で custom-receive オブジェクトに非透過的な参照です。

**SerCx2CustomReceiveCreate**メソッド custom-receive オブジェクトを作成します。 SerCx2 では、このオブジェクトを使用して、カスタムのデータ転送機構を使用してシリアル コント ローラーからデータを読み取る I/O トランザクションを管理します。 このオブジェクトは、コント ローラーのシリアル ドライバーに対して非透過的です。 
**SerCx2CustomReceiveCreate**装置、出力パラメーター、新しく作成した SERCX2CUSTOMRECEIVE ハンドルとしてカスタムのオブジェクトを受け取ります。 SerCx2 とシリアル コント ローラー ドライバーは、このハンドルを使用して、SerCx2 メソッドおよびイベントのコールバック関数への後続の呼び出しでオブジェクトを参照してください。

後**SerCx2CustomReceiveCreate** custom-receive を作成します。 コント ローラーのシリアル デバイスを表す framework デバイス オブジェクトの有効期間は、このオブジェクトが存在するオブジェクト。 デバイス オブジェクトが削除されたときに、custom-receive オブジェクトが自動的に削除します。 シリアル コント ローラー ドライバーにする必要があります_いない_などのメソッドを呼び出すことによって、custom-receive オブジェクトを削除しようとしています。 [WdfObjectDelete](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfobject/nf-wdfobject-wdfobjectdelete)します。

シリアル コント ローラー ドライバーは、オプションとして、オブジェクトを作成できます custom-receive が、このような 1 つのオブジェクトを作成できます。 ドライバーは、次の条件下でのみ、このオブジェクトを作成できます。

* ドライバーは、以前 PIO 受信オブジェクトを作成します。
* ドライバーは*いない*DMA 受信システム オブジェクトを作成します。

PIO 受信オブジェクトの詳細については、次を参照してください。 [SERCX2PIORECEIVE オブジェクト処理](#sercx2pioreceive-object-handle)します。 DMA 受信システム オブジェクトの詳細については、次を参照してください。 [SERCX2SYSTEMDMARECEIVE オブジェクト処理](#sercx2systemdmareceive-object-handle)します。


##  <a name="sercx2customreceivetransaction-object-handle"></a>SERCX2CUSTOMRECEIVETRANSACTION オブジェクト ハンドル
A **SERCX2CUSTOMRECEIVETRANSACTION**オブジェクト ハンドルは、シリアル フレームワーク拡張機能 (SerCx2) のバージョン 2 でカスタム受信トランザクション オブジェクトに非透過的な参照です。

[SerCx2CustomReceiveTransactionCreate](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/sercx/nf-sercx-sercx2customreceivetransactioncreate)メソッドは、カスタム受信トランザクション オブジェクトを作成します。 SerCx2 では、このオブジェクトを使用して、カスタムのデータ転送機構を使用してシリアル コント ローラーで受信したデータの読み取り I/O トランザクションを管理します。 このオブジェクトは、コント ローラーのシリアル ドライバーに対して非透過的です。 
[SerCx2CustomReceiveTransactionCreate](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/sercx/nf-sercx-sercx2customreceivetransactioncreate)出力パラメーターとして、新しく作成されたカスタム受信トランザクション オブジェクトへの SERCX2CUSTOMRECEIVETRANSACTION ハンドルを提供します。 SerCx2 およびそれ以降にオブジェクトを参照するこの処理コント ローラーのシリアル ドライバーの使用カスタム受信トランザクション。 詳細については、次を参照してください。 [SerCx2 カスタム受信トランザクション](https://docs.microsoft.com/windows-hardware/drivers/serports/sercx2-custom-receive-transactions)です。

後[SerCx2CustomReceiveTransactionCreate](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/sercx/nf-sercx-sercx2customreceivetransactioncreate)トランザクションを作成、カスタムの受信-コント ローラーのシリアル デバイスを表す framework デバイス オブジェクトの有効期間は、このオブジェクトが存在するオブジェクトします。 カスタム受信トランザクション オブジェクトは、デバイス オブジェクトが削除されたときに自動的に削除します。 シリアル コント ローラー ドライバーにする必要があります_いない_などのメソッドを呼び出すことによって、カスタム受信トランザクション オブジェクトを削除しようとしています。 [WdfObjectDelete](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfobject/nf-wdfobject-wdfobjectdelete)します。

シリアル コント ローラー ドライバーは、オプションとして、カスタム受信トランザクション オブジェクトを作成しますが、このような 1 つのオブジェクトを作成できます。 ドライバーは、次の条件下でのみ、このオブジェクトを作成できます </wdcml:p >。

* ドライバーは、以前 PIO 受信オブジェクトを作成します。
* ドライバーは、以前 custom-receive オブジェクトを作成します。

PIO 受信オブジェクトの詳細については、次を参照してください。 [SERCX2PIORECEIVE オブジェクト処理](#sercx2pioreceive-object-handle)します。 詳細については、カスタムの受信オブジェクトを参照してください[SERCX2CUSTOMRECEIVE オブジェクト処理](#sercx2customreceive-object-handle)します。

Custom-receive とカスタム受信トランザクション オブジェクトのような有効期間に関係なくこれらは個別のオブジェクト型として定義されている (および 1 つの型に結合されません)、SerCx2 デバイス ドライバー インターフェイスの考えられる将来の拡張をサポートするためにします。

##  <a name="sercx2customtransmit-object-handle"></a>SERCX2CUSTOMTRANSMIT オブジェクト ハンドル
SERCX2CUSTOMTRANSMIT オブジェクト ハンドルは、シリアル フレームワークの拡張機能 (SerCx2) のバージョン 2 で custom-transmit オブジェクトに非透過的な参照です。

[SerCx2CustomTransmitCreate](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/sercx/nf-sercx-sercx2customtransmitcreate)メソッドを作成、シリアル コント ローラーにデータを書き込む I/O トランザクションを管理するオブジェクトのこの object.h SerCx2 使用のカスタム送信します。 このオブジェクトは、コント ローラーのシリアル ドライバーに対して非透過的です。 
[SerCx2CustomTransmitCreate](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/sercx/nf-sercx-sercx2customtransmitcreate)装置、出力パラメーター、新しく作成した SERCX2CUSTOMTRANSMIT ハンドルとしてカスタムの送信オブジェクト。 SerCx2 とシリアル コント ローラー ドライバーは、このハンドルを使用して、SerCx2 メソッドおよびイベントのコールバック関数への後続の呼び出しでオブジェクトを参照してください。

後[SerCx2CustomTransmitCreate](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/sercx/nf-sercx-sercx2customtransmitcreate) custom-transmit を作成します。 コント ローラーのシリアル デバイスを表す framework デバイス オブジェクトの有効期間は、このオブジェクトが存在するオブジェクト。 デバイス オブジェクトが削除されたときに、custom-transmit オブジェクトが自動的に削除します。 シリアル コント ローラー ドライバーにする必要があります_いない_などのメソッドを呼び出すことによって、custom-transmit オブジェクトを削除しようとしています。 [WdfObjectDelete](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfobject/nf-wdfobject-wdfobjectdelete)します。

シリアル コント ローラー ドライバーは、オプションとして、オブジェクトを作成できます custom-transmit が、このような 1 つのオブジェクトを作成できます。 ドライバーは、次の条件下でのみ、このオブジェクトを作成できます。

* ドライバーは、以前 PIO 送信オブジェクトを作成します。
* ドライバーは_いない_システム DMA 送信オブジェクトを作成します。

PIO 送信オブジェクトの詳細については、次を参照してください。 [SERCX2PIOTRANSMIT オブジェクト処理](#sercx2piotransmit-object-handle)します。 DMA 送信システム オブジェクトの詳細については、次を参照してください。 [SERCX2SYSTEMDMATRANSMIT オブジェクト処理](#sercx2systemdmatransmit-object-handle)します。

##  <a name="sercx2customtransmittransaction-object-handle"></a>SERCX2CUSTOMTRANSMITTRANSACTION オブジェクト ハンドル
SERCX2CUSTOMTRANSMITTRANSACTION オブジェクト ハンドルは、シリアル フレームワークの拡張機能 (SerCx2) のバージョン 2 カスタム送信トランザクション オブジェクトに非透過的な参照です。

[SerCx2CustomTransmitTransactionCreate](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/sercx/nf-sercx-sercx2customtransmittransactioncreate)メソッドは、カスタム送信トランザクション オブジェクトを作成します。 SerCx2 では、このオブジェクトを使用して、カスタムのデータ転送メカニズムを使用してシリアル コント ローラーにデータを書き込む I/O トランザクションを管理します。 このオブジェクトは、コント ローラーのシリアル ドライバーに対して非透過的です。 
[SerCx2CustomTransmitTransactionCreate](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/sercx/nf-sercx-sercx2customtransmittransactioncreate)出力パラメーターとして、新しく作成されたカスタム送信トランザクション オブジェクトへの SERCX2CUSTOMTRANSMITTRANSACTION ハンドルを提供します。 SerCx2 およびそれ以降にオブジェクトを参照するこの処理コント ローラーのシリアル ドライバーの使用カスタム-送信トランザクション。 詳細については、次を参照してください。 [SerCx2 カスタム送信トランザクション](https://docs.microsoft.com/previous-versions/dn265320(v=vs.85))です。

後[SerCx2CustomTransmitTransactionCreate](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/sercx/nf-sercx-sercx2customtransmittransactioncreate)トランザクションを作成、カスタムの送信-コント ローラーのシリアル デバイスを表す framework デバイス オブジェクトの有効期間は、このオブジェクトが存在するオブジェクトします。 デバイス オブジェクトが削除されたときに、カスタム送信トランザクション オブジェクトが自動的に削除します。 シリアル コント ローラー ドライバーにする必要があります_いない_などのメソッドを呼び出すことによって、カスタム送信トランザクション オブジェクトを削除しようとしています。 [WdfObjectDelete](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfobject/nf-wdfobject-wdfobjectdelete)します。

シリアル コント ローラー ドライバーは、オプションとして、オブジェクトを作成できます custom-transmit が、このような 1 つのオブジェクトを作成できます。 ドライバーは、次の条件下でのみ、このオブジェクトを作成できます。

* ドライバーは、以前 PIO 送信オブジェクトを作成します。
* ドライバーは_いない_システム DMA 送信オブジェクトを作成します。

PIO 送信オブジェクトの詳細については、次を参照してください。 [SERCX2PIOTRANSMIT オブジェクト処理](#sercx2piotransmit-object-handle)します。 詳細については、オブジェクトのカスタムの送信を参照してください[SERCX2CUSTOMTRANSMIT オブジェクト処理](#sercx2customtransmit-object-handle)します。

Custom-transmit とカスタム送信トランザクション オブジェクトのような有効期間に関係なくこれらは個別のオブジェクト型として定義されている (および 1 つの型に結合されません)、SerCx2 デバイス ドライバー インターフェイスの考えられる将来の拡張をサポートするためにします。

##  <a name="sercx2pioreceive-object-handle"></a>SERCX2PIORECEIVE オブジェクト ハンドル
SERCX2PIORECEIVE オブジェクト ハンドルは、シリアル フレームワークの拡張機能 (SerCx2) のバージョン 2 で PIO 受信オブジェクトに非透過的な参照です。

[SerCx2PioReceiveCreate](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/sercx/nf-sercx-sercx2pioreceivecreate)メソッド PIO 受信オブジェクトを作成します。 SerCx2 シリアル コント ローラーからデータを読み取る下手順の I/O (PIO) トランザクションを管理するのにオブジェクトを使用します。 このオブジェクトは、コント ローラーのシリアル ドライバーに対して非透過的です。 新しく作成された PIO 受信オブジェクトを識別する SERCX2PIORECEIVE ハンドルを出力パラメーターとして提供します。 SerCx2 とシリアル コント ローラー ドライバーは、このハンドルを使用して、後続の PIO 受信トランザクション内のオブジェクトを参照してください。 

詳細については、次を参照してください。 [SerCx2 PIO 受信トランザクション](https://docs.microsoft.com/previous-versions/dn265332(v=vs.85))です。
後[SerCx2PioReceiveCreate](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/sercx/nf-sercx-sercx2pioreceivecreate) PIO 受信を作成します。 コント ローラーのシリアル デバイスを表す framework デバイス オブジェクトの有効期間は、このオブジェクトが存在するオブジェクト。 デバイス オブジェクトが削除されたときに、PIO 受信オブジェクトが自動的に削除します。 シリアル コント ローラー ドライバーにする必要があります_いない_などのメソッドを呼び出すことによって、PIO 受信オブジェクトを削除しようとしています。 [WdfObjectDelete](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfobject/nf-wdfobject-wdfobjectdelete)します。

シリアル コント ローラー ドライバーでは、1 つだけの PIO 受信オブジェクトを作成する必要があります。 ドライバーは、DMA 受信システム オブジェクトか custom-receive オブジェクトを作成する前に、このオブジェクトを作成する必要があります。 DMA 受信システム オブジェクトの詳細については、次を参照してください。 [SERCX2SYSTEMDMARECEIVE オブジェクト処理](#sercx2systemdmareceive-object-handle)します。 詳細については、カスタムの受信オブジェクトを参照してください[SERCX2CUSTOMRECEIVE オブジェクト処理](#sercx2customreceive-object-handle)します。

##  <a name="sercx2piotransmit-object-handle"></a>SERCX2PIOTRANSMIT オブジェクト ハンドル
SERCX2PIOTRANSMIT オブジェクト ハンドルは、シリアル フレームワークの拡張機能 (SerCx2) のバージョン 2 で PIO 送信オブジェクトに非透過的な参照です。

[SerCx2PioTransmitCreate](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/sercx/nf-sercx-sercx2piotransmitcreate)メソッド PIO 送信オブジェクトを作成します。 SerCx2 では、このオブジェクトを使用して、I/O (PIO) シリアル コント ローラーにデータを書き込むように使用してプログラミング I/O トランザクションを管理します。 このオブジェクトは、コント ローラーのシリアル ドライバーに対して非透過的です。 
[SerCx2PioTransmitCreate](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/sercx/nf-sercx-sercx2piotransmitcreate)出力パラメーターとして、新しく作成された PIO 送信オブジェクトを識別する SERCX2PIOTRANSMIT ハンドルを提供します。 SerCx2 とシリアル コント ローラー ドライバーは、このハンドルを使用して、後続の PIO 送信トランザクション内のオブジェクトを参照してください。 詳細については、次を参照してください。 [SerCx2 PIO 送信トランザクション](https://docs.microsoft.com/previous-versions/dn265336(v=vs.85))です。


後[SerCx2PioTransmitCreate](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/sercx/nf-sercx-sercx2piotransmitcreate) PIO 転送を作成します。 コント ローラーのシリアル デバイスを表す framework デバイス オブジェクトの有効期間は、このオブジェクトが存在するオブジェクト。 デバイス オブジェクトが削除されたときに、PIO 転送オブジェクトが自動的に削除します。 シリアル コント ローラー ドライバーにする必要があります_いない_などのメソッドを呼び出すことによって、PIO 送信オブジェクトを削除しようとしています。 [WdfObjectDelete](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfobject/nf-wdfobject-wdfobjectdelete)します。

シリアル コント ローラー ドライバーでは、1 つだけの PIO 送信オブジェクトを作成する必要があります。 ドライバーは、DMA 送信システム オブジェクトか custom-transmit オブジェクトを作成する前に、このオブジェクトを作成する必要があります。 DMA 送信システム オブジェクトの詳細については、次を参照してください。 [SERCX2SYSTEMDMATRANSMIT オブジェクト処理](#sercx2systemdmatransmit-object-handle)します。 詳細については、オブジェクトのカスタムの送信を参照してください[SERCX2CUSTOMTRANSMIT オブジェクト処理](#sercx2customtransmit-object-handle)します。

##  <a name="sercx2systemdmareceive-object-handle"></a>SERCX2SYSTEMDMARECEIVE オブジェクト ハンドル
SERCX2SYSTEMDMARECEIVE オブジェクト ハンドルは、シリアル フレームワークの拡張機能 (SerCx2) のバージョン 2 で DMA 受信システム オブジェクトに非透過的な参照です。

[SerCx2SystemDmaReceiveCreate](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/sercx/nf-sercx-sercx2systemdmareceivecreate)メソッドは、DMA 受信システム オブジェクトを作成します。 SerCx2 では、このオブジェクトを使用して、シリアル コント ローラーからデータを読み取るシステム DMA のトランザクションを管理します。 このオブジェクトは、コント ローラーのシリアル ドライバーに対して非透過的です。 
[SerCx2SystemDmaReceiveCreate](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/sercx/nf-sercx-sercx2systemdmareceivecreate)出力パラメーターとして、新しく作成されたシステム DMA 受信オブジェクトを識別する SERCX2SYSTEMDMARECEIVE ハンドルを提供します。 SerCx2 とシリアル コント ローラー ドライバーは、このハンドルを使用して、後続の DMA 受信システムのトランザクション内のオブジェクトを参照してください。 詳細については、次を参照してください。 [SerCx2 システム DMA 受信トランザクション](https://docs.microsoft.com/previous-versions/dn265343(v=vs.85))です。

後[SerCx2SystemDmaReceiveCreate](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/sercx/nf-sercx-sercx2systemdmareceivecreate)システムの DMA の受信を作成します。 コント ローラーのシリアル デバイスを表す framework デバイス オブジェクトの有効期間は、このオブジェクトが存在するオブジェクト。 デバイス オブジェクトが削除されたときに、DMA 受信システム オブジェクトが自動的に削除します。 シリアル コント ローラー ドライバー、オプションとして、作成できます、DMA 受信システム オブジェクトがこのような 1 つのオブジェクトを作成できます。 ドライバーは、次の条件下でのみ、このオブジェクトを作成できます。

* ドライバーは、以前 PIO 受信オブジェクトを作成します。
* ドライバーは_いない_custom-receive オブジェクトを作成します。

PIO 受信オブジェクトの詳細については、次を参照してください。 [SERCX2PIORECEIVE オブジェクト処理](#sercx2pioreceive-object-handle)します。 詳細については、カスタムの受信オブジェクトを参照してください[SERCX2CUSTOMRECEIVE オブジェクト処理](#sercx2customreceive-object-handle)します。

##  <a name="sercx2systemdmatransmit-object-handle"></a>SERCX2SYSTEMDMATRANSMIT オブジェクト ハンドル
SERCX2SYSTEMDMATRANSMIT オブジェクト ハンドルは、シリアル フレームワークの拡張機能 (SerCx2) のバージョン 2 でシステム DMA 送信オブジェクトに非透過的な参照です。

[SerCx2SystemDmaTransmitCreate](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/sercx/nf-sercx-sercx2systemdmatransmitcreate)メソッドは、システム DMA 送信オブジェクトを作成します。 SerCx2 では、このオブジェクトを使用して、シリアル コント ローラーにデータを書き込むシステム DMA のトランザクションを管理します。 このオブジェクトは、コント ローラーのシリアル ドライバーに対して非透過的です。 
[SerCx2SystemDmaTransmitCreate](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/sercx/nf-sercx-sercx2systemdmatransmitcreate)出力パラメーターとして、新しく作成されたシステム DMA 送信オブジェクトを識別する SERCX2SYSTEMDMATRANSMIT ハンドルを提供します。 SerCx2 とシリアル コント ローラー ドライバーは、このハンドルを使用して、後続のシステム DMA 送信トランザクション内のオブジェクトを参照してください。 詳細については、次を参照してください。 [SerCx2 システム DMA 送信トランザクション](https://docs.microsoft.com/previous-versions/dn265338(v=vs.85))です。

後[SerCx2SystemDmaTransmitCreate](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/sercx/nf-sercx-sercx2systemdmatransmitcreate)システムの DMA の転送を作成します。 コント ローラーのシリアル デバイスを表す framework デバイス オブジェクトの有効期間は、このオブジェクトが存在するオブジェクト。 デバイス オブジェクトが削除されたときに、システム DMA 転送オブジェクトが自動的に削除します。 シリアル コント ローラー ドライバーにする必要があります_いない_などのメソッドを呼び出すことによってシステム DMA 送信オブジェクトを削除しようとしています。 [WdfObjectDelete](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfobject/nf-wdfobject-wdfobjectdelete)します。

シリアル コント ローラー ドライバー、オプションとして、作成できます、DMA 送信システム オブジェクトがこのような 1 つのオブジェクトを作成できます。 ドライバーは、次の条件下でのみ、このオブジェクトを作成できます </wdcml:p >。

* ドライバーは、以前 PIO 送信オブジェクトを作成します。
* ドライバーは_いない_custom-transmit オブジェクトを作成します。

PIO 送信オブジェクトの詳細については、次を参照してください。 [SERCX2PIOTRANSMIT オブジェクト処理](#sercx2piotransmit-object-handle)します。 詳細については、オブジェクトのカスタムの送信を参照してください[SERCX2CUSTOMTRANSMIT オブジェクト処理](#sercx2customtransmit-object-handle)します。

## <a name="related-topics"></a>関連トピック

[SerCx2 カスタム受信トランザクション](https://docs.microsoft.com/windows-hardware/drivers/serports/sercx2-custom-receive-transactions)

[SerCx2 カスタム送信トランザクション](https://docs.microsoft.com/previous-versions/dn265320(v=vs.85))

[SerCx2 PIO 受信トランザクション](https://docs.microsoft.com/previous-versions/dn265332(v=vs.85))

[SerCx2 PIO 送信トランザクション](https://docs.microsoft.com/previous-versions/dn265336(v=vs.85))

[SerCx2 DMA 受信システム トランザクション](https://docs.microsoft.com/previous-versions/dn265343(v=vs.85))

[SerCx2 DMA 送信システム トランザクション](https://docs.microsoft.com/previous-versions/dn265338(v=vs.85))

[SerCx2CustomReceiveTransactionCreate](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/sercx/nf-sercx-sercx2customreceivetransactioncreate)

[SerCx2CustomTransmitCreate](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/sercx/nf-sercx-sercx2customtransmitcreate)

[SerCx2CustomTransmitTransactionCreate](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/sercx/nf-sercx-sercx2customtransmittransactioncreate)

[SerCx2PioReceiveCreate](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/sercx/nf-sercx-sercx2pioreceivecreate)

[SerCx2PioReceiveCreate](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/sercx/nf-sercx-sercx2pioreceivecreate)

[SerCx2PioTransmitCreate](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/sercx/nf-sercx-sercx2piotransmitcreate)

[SerCx2SystemDmaReceiveCreate](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/sercx/nf-sercx-sercx2systemdmareceivecreate)

[SerCx2SystemDmaTransmitCreate](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/sercx/nf-sercx-sercx2systemdmatransmitcreate)

[Framework のオブジェクトの概要](https://docs.microsoft.com/windows-hardware/drivers/wdf/summary-of-framework-objects)

[WdfObjectDelete](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfobject/nf-wdfobject-wdfobjectdelete)





