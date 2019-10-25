---
title: SerCx2 オブジェクト ハンドル
description: このトピックでは、シリアルフレームワーク拡張機能 (SerCx2) のバージョン2で特に定義されているオブジェクトハンドル型について説明します。
ms.localizationpriority: medium
ms.date: 12/27/2018
ms.openlocfilehash: 07bfe0538cf3d3e46ee4ee55dfaf1677083ed770
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72845409"
---
# <a name="sercx2-object-handles"></a>SerCx2 オブジェクト ハンドル

このトピックでは、シリアルフレームワーク拡張機能 (SerCx2) のバージョン2で特に定義されているオブジェクトハンドル型について説明します。 SerCx2 device driver interface (DDI) は、これらのハンドルの種類を使用して、SerCx2 に固有の特徴と機能を持つオブジェクトを参照します。

さらに、SerCx2 DDI では、カーネルモードドライバーフレームワーク (KMDF) によって定義されている、WDFDEVICE と WDFDEVICE の2つのジェネリックオブジェクトハンドル型を使用します。 フレームワークのハンドル型の詳細については、「[フレームワークオブジェクトの概要](https://docs.microsoft.com/windows-hardware/drivers/wdf/summary-of-framework-objects)」を参照してください。

このトピックでは、次のオブジェクトハンドルについて説明します。

* [SERCX2CUSTOMRECEIVE オブジェクトハンドル](#sercx2customreceive-object-handle)
* [SERCX2CUSTOMRECEIVETRANSACTION オブジェクトハンドル](#sercx2customreceivetransaction-object-handle)
* [SERCX2CUSTOMTRANSMIT オブジェクトハンドル](#sercx2customtransmit-object-handle)
* [SERCX2CUSTOMTRANSMITTRANSACTION オブジェクトハンドル](#sercx2customtransmittransaction-object-handle)
* [SERCX2PIORECEIVE オブジェクトハンドル](#sercx2pioreceive-object-handle)
* [SERCX2PIOTRANSMIT オブジェクトハンドル](#sercx2piotransmit-object-handle)
* [SERCX2SYSTEMDMARECEIVE オブジェクトハンドル](#sercx2systemdmareceive-object-handle)
* [SERCX2SYSTEMDMATRANSMIT オブジェクトハンドル](#sercx2systemdmatransmit-object-handle)

ヘッダー: 2.0 \ Sercx. h

##  <a name="sercx2customreceive-object-handle"></a>SERCX2CUSTOMRECEIVE オブジェクトハンドル
**SERCX2CUSTOMRECEIVE**オブジェクトハンドルは、serial framework Extension (SerCx2) のバージョン2のカスタム受信オブジェクトへの非透過的な参照です。

**SerCx2CustomReceiveCreate**メソッドは、カスタム受信オブジェクトを作成します。 SerCx2 は、このオブジェクトを使用して、カスタムデータ転送機構を使用してシリアルコントローラーからデータを読み取る i/o トランザクションを管理します。 このオブジェクトはシリアルコントローラードライバーに対して非透過的です。 
**SerCx2CustomReceiveCreate**は、新しく作成されたカスタム受信オブジェクトへの SERCX2CUSTOMRECEIVE ハンドルを出力パラメーターとして提供します。 SerCx2 とシリアルコントローラードライバーは、このハンドルを使用して、SerCx2 メソッドおよびイベントコールバック関数への後続の呼び出しでオブジェクトを参照します。

**SerCx2CustomReceiveCreate**がカスタム受信オブジェクトを作成した後、このオブジェクトは、シリアルコントローラーデバイスを表すフレームワークデバイスオブジェクトの有効期間にわたって存在します。 カスタム受信オブジェクトは、デバイスオブジェクトが削除されると自動的に削除されます。 シリアルコントローラードライバーは、 [Wdfobjectdelete](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfobject/nf-wdfobject-wdfobjectdelete)などのメソッドを呼び出すことによって、カスタム受信オブジェクトを削除し_ない_ようにする必要があります。

シリアルコントローラードライバーは、オプションとしてカスタム受信オブジェクトを作成できますが、そのようなオブジェクトは1つしか作成できません。 ドライバーは、次の条件下でのみこのオブジェクトを作成できます。

* ドライバーにより、以前に PIO 受信オブジェクトが作成されました。
* ドライバーによってシステム DMA 受信オブジェクトが作成され*ていません*。

PIO 受信オブジェクトの詳細については、「 [SERCX2PIORECEIVE Object Handle](#sercx2pioreceive-object-handle)」を参照してください。 システム DMA 受信オブジェクトの詳細については、「 [SERCX2SYSTEMDMARECEIVE Object Handle](#sercx2systemdmareceive-object-handle)」を参照してください。


##  <a name="sercx2customreceivetransaction-object-handle"></a>SERCX2CUSTOMRECEIVETRANSACTION オブジェクトハンドル
**SERCX2CUSTOMRECEIVETRANSACTION**オブジェクトハンドルは、serial framework Extension (SerCx2) のバージョン2のカスタムの受信トランザクションオブジェクトへの非透過的な参照です。

[SerCx2CustomReceiveTransactionCreate](https://docs.microsoft.com/windows-hardware/drivers/ddi/sercx/nf-sercx-sercx2customreceivetransactioncreate)メソッドは、カスタムの受信トランザクションオブジェクトを作成します。 SerCx2 は、このオブジェクトを使用して、シリアルコントローラーによって受信されたデータを読み取るカスタムデータ転送機構を使用する i/o トランザクションを管理します。 このオブジェクトはシリアルコントローラードライバーに対して非透過的です。 
[SerCx2CustomReceiveTransactionCreate](https://docs.microsoft.com/windows-hardware/drivers/ddi/sercx/nf-sercx-sercx2customreceivetransactioncreate)は、新しく作成されたカスタムトランザクションオブジェクトへの SERCX2CUSTOMRECEIVETRANSACTION ハンドルを出力パラメーターとして提供します。 SerCx2 とシリアルコントローラードライバーは、このハンドルを使用して、後続のカスタム受信トランザクションでオブジェクトを参照します。 詳細については、「 [SerCx2 Custom-Receive](https://docs.microsoft.com/windows-hardware/drivers/serports/sercx2-custom-receive-transactions)transaction」を参照してください。

[SerCx2CustomReceiveTransactionCreate](https://docs.microsoft.com/windows-hardware/drivers/ddi/sercx/nf-sercx-sercx2customreceivetransactioncreate)がカスタムの受信トランザクションオブジェクトを作成した後、このオブジェクトは、シリアルコントローラーデバイスを表すフレームワークデバイスオブジェクトの有効期間にわたって存在します。 カスタムの受信トランザクションオブジェクトは、デバイスオブジェクトが削除されると自動的に削除されます。 シリアルコントローラードライバーは、 [Wdfobjectdelete](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfobject/nf-wdfobject-wdfobjectdelete)などのメソッドを呼び出すことによって、カスタムの受信トランザクションオブジェクトを削除し_ない_ようにする必要があります。

シリアルコントローラードライバーは、オプションとしてカスタムの受信トランザクションオブジェクトを作成できますが、そのようなオブジェクトは1つしか作成できません。 ドライバーは、次の条件に当てはまる場合にのみ、このオブジェクトを作成でき </wdcml: p >

* ドライバーにより、以前に PIO 受信オブジェクトが作成されました。
* ドライバーは、以前にカスタム受信オブジェクトを作成しました。

PIO 受信オブジェクトの詳細については、「 [SERCX2PIORECEIVE Object Handle](#sercx2pioreceive-object-handle)」を参照してください。 カスタム受信オブジェクトの詳細については、「 [SERCX2CUSTOMRECEIVE Object Handle](#sercx2customreceive-object-handle)」を参照してください。

カスタム受信トランザクションオブジェクトとカスタムトランザクションオブジェクトの有効期間は同様ですが、これらは個別のオブジェクト型として定義されます (1 つの型には結合されません)。これにより、SerCx2 device driver インターフェイスが将来拡張される可能性があります。

##  <a name="sercx2customtransmit-object-handle"></a>SERCX2CUSTOMTRANSMIT オブジェクトハンドル
SERCX2CUSTOMTRANSMIT オブジェクトハンドルは、serial framework extension (SerCx2) のバージョン2のカスタム送信オブジェクトへの非透過的な参照です。

[SerCx2CustomTransmitCreate](https://docs.microsoft.com/windows-hardware/drivers/ddi/sercx/nf-sercx-sercx2customtransmitcreate)メソッドは、カスタム送信オブジェクトを作成します。 h SerCx2 は、このオブジェクトを使用して、シリアルコントローラーにデータを書き込む i/o トランザクションを管理します。 このオブジェクトはシリアルコントローラードライバーに対して非透過的です。 
[SerCx2CustomTransmitCreate](https://docs.microsoft.com/windows-hardware/drivers/ddi/sercx/nf-sercx-sercx2customtransmitcreate)は、新しく作成されたカスタム送信オブジェクトへの SERCX2CUSTOMTRANSMIT ハンドルを出力パラメーターとして提供します。 SerCx2 とシリアルコントローラードライバーは、このハンドルを使用して、SerCx2 メソッドおよびイベントコールバック関数への後続の呼び出しでオブジェクトを参照します。

[SerCx2CustomTransmitCreate](https://docs.microsoft.com/windows-hardware/drivers/ddi/sercx/nf-sercx-sercx2customtransmitcreate)がカスタム送信オブジェクトを作成した後、このオブジェクトは、シリアルコントローラーデバイスを表すフレームワークデバイスオブジェクトの有効期間にわたって存在します。 カスタム送信オブジェクトは、デバイスオブジェクトが削除されると自動的に削除されます。 シリアルコントローラードライバーは、 [Wdfobjectdelete](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfobject/nf-wdfobject-wdfobjectdelete)などのメソッドを呼び出すことによって、カスタム転送オブジェクトを削除し_ない_ようにする必要があります。

シリアルコントローラードライバーは、オプションとしてカスタム転送オブジェクトを作成できますが、そのようなオブジェクトは1つしか作成できません。 ドライバーは、次の条件下でのみこのオブジェクトを作成できます。

* ドライバーは、以前に PIO 送信オブジェクトを作成しました。
* ドライバーがシステム DMA 転送オブジェクトを作成し_ていません_。

PIO 転送オブジェクトの詳細については、「 [SERCX2PIOTRANSMIT Object Handle](#sercx2piotransmit-object-handle)」を参照してください。 システム DMA 転送オブジェクトの詳細については、「 [SERCX2SYSTEMDMATRANSMIT Object Handle](#sercx2systemdmatransmit-object-handle)」を参照してください。

##  <a name="sercx2customtransmittransaction-object-handle"></a>SERCX2CUSTOMTRANSMITTRANSACTION オブジェクトハンドル
SERCX2CUSTOMTRANSMITTRANSACTION オブジェクトハンドルは、serial framework extension (SerCx2) のバージョン2のカスタム送信トランザクションオブジェクトへの非透過的な参照です。

[SerCx2CustomTransmitTransactionCreate](https://docs.microsoft.com/windows-hardware/drivers/ddi/sercx/nf-sercx-sercx2customtransmittransactioncreate)メソッドは、カスタム送信トランザクションオブジェクトを作成します。 SerCx2 は、このオブジェクトを使用して、カスタムデータ転送メカニズムを使用してシリアルコントローラーにデータを書き込む i/o トランザクションを管理します。 このオブジェクトはシリアルコントローラードライバーに対して非透過的です。 
[SerCx2CustomTransmitTransactionCreate](https://docs.microsoft.com/windows-hardware/drivers/ddi/sercx/nf-sercx-sercx2customtransmittransactioncreate)は、出力パラメーターとして、新しく作成されたカスタム送信トランザクションオブジェクトへの SERCX2CUSTOMTRANSMITTRANSACTION ハンドルを提供します。 SerCx2 とシリアルコントローラードライバーは、このハンドルを使用して、後続のカスタム送信トランザクションでオブジェクトを参照します。 詳細については、「 [SerCx2 Custom-送信トランザクション](https://docs.microsoft.com/previous-versions/dn265320(v=vs.85))」を参照してください。

[SerCx2CustomTransmitTransactionCreate](https://docs.microsoft.com/windows-hardware/drivers/ddi/sercx/nf-sercx-sercx2customtransmittransactioncreate)がカスタム送信トランザクションオブジェクトを作成した後、このオブジェクトは、シリアルコントローラーデバイスを表すフレームワークデバイスオブジェクトの有効期間にわたって存在します。 カスタム送信トランザクションオブジェクトは、デバイスオブジェクトが削除されると自動的に削除されます。 シリアルコントローラードライバーは、 [Wdfobjectdelete](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfobject/nf-wdfobject-wdfobjectdelete)などのメソッドを呼び出すことによって、カスタムの送信トランザクションオブジェクトを削除し_ない_ようにする必要があります。

シリアルコントローラードライバーは、オプションとしてカスタム転送オブジェクトを作成できますが、そのようなオブジェクトは1つしか作成できません。 ドライバーは、次の条件下でのみこのオブジェクトを作成できます。

* ドライバーは、以前に PIO 送信オブジェクトを作成しました。
* ドライバーがシステム DMA 転送オブジェクトを作成し_ていません_。

PIO 転送オブジェクトの詳細については、「 [SERCX2PIOTRANSMIT Object Handle](#sercx2piotransmit-object-handle)」を参照してください。 カスタム転送オブジェクトの詳細については、「 [SERCX2CUSTOMTRANSMIT Object Handle](#sercx2customtransmit-object-handle)」を参照してください。

カスタム送信トランザクションオブジェクトとカスタムトランザクションオブジェクトの有効期間は同様ですが、これらは、SerCx2 device driver インターフェイスを将来拡張できるようにするために、個別のオブジェクト型 (および1つの型に結合されない) として定義されます。

##  <a name="sercx2pioreceive-object-handle"></a>SERCX2PIORECEIVE オブジェクトハンドル
SERCX2PIORECEIVE オブジェクトハンドルは、serial framework extension (SerCx2) のバージョン2の PIO 受信オブジェクトへの非透過参照です。

[SerCx2PioReceiveCreate](https://docs.microsoft.com/windows-hardware/drivers/ddi/sercx/nf-sercx-sercx2pioreceivecreate)メソッドは、PIO 受信オブジェクトを作成します。 SerCx2 は、オブジェクトを使用して、シリアルコントローラーからデータを読み取るプログラム i/o (PIO) トランザクションを管理します。 このオブジェクトはシリアルコントローラードライバーに対して非透過的です。 は、新しく作成された PIO 受信オブジェクトへの SERCX2PIORECEIVE ハンドルを出力パラメーターとして提供します。 SerCx2 とシリアルコントローラードライバーは、このハンドルを使用して、後続の PIO トランザクションでオブジェクトを参照します。 

詳細については、「 [SERCX2 PIO-Receive](https://docs.microsoft.com/previous-versions/dn265332(v=vs.85))transaction」を参照してください。
[SerCx2PioReceiveCreate](https://docs.microsoft.com/windows-hardware/drivers/ddi/sercx/nf-sercx-sercx2pioreceivecreate)が PIO 受信オブジェクトを作成した後、このオブジェクトは、シリアルコントローラーデバイスを表すフレームワークデバイスオブジェクトの有効期間にわたって存在します。 PIO 受信オブジェクトは、デバイスオブジェクトが削除されると自動的に削除されます。 シリアルコントローラードライバーは、 [Wdfobjectdelete](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfobject/nf-wdfobject-wdfobjectdelete)などのメソッドを呼び出すことによって、PIO 受信オブジェクトを削除し_ない_ようにする必要があります。

シリアルコントローラードライバーは、PIO 受信オブジェクトを1つだけ作成する必要があります。 ドライバーは、システム DMA 受信オブジェクトまたはカスタム受信オブジェクトのいずれかを作成する前に、このオブジェクトを作成する必要があります。 システム DMA 受信オブジェクトの詳細については、「 [SERCX2SYSTEMDMARECEIVE Object Handle](#sercx2systemdmareceive-object-handle)」を参照してください。 カスタム受信オブジェクトの詳細については、「 [SERCX2CUSTOMRECEIVE Object Handle](#sercx2customreceive-object-handle)」を参照してください。

##  <a name="sercx2piotransmit-object-handle"></a>SERCX2PIOTRANSMIT オブジェクトハンドル
SERCX2PIOTRANSMIT オブジェクトハンドルは、シリアルフレームワーク拡張機能 (SerCx2) のバージョン2の PIO 送信オブジェクトへの非透過参照です。

[SerCx2PioTransmitCreate](https://docs.microsoft.com/windows-hardware/drivers/ddi/sercx/nf-sercx-sercx2piotransmitcreate)メソッドは、PIO 転送オブジェクトを作成します。 SerCx2 は、このオブジェクトを使用して、プログラムされた i/o (PIO) を使用してシリアルコントローラーにデータを書き込む i/o トランザクションを管理します。 このオブジェクトはシリアルコントローラードライバーに対して非透過的です。 
[SerCx2PioTransmitCreate](https://docs.microsoft.com/windows-hardware/drivers/ddi/sercx/nf-sercx-sercx2piotransmitcreate)は、新しく作成された PIO 送信オブジェクトへの SERCX2PIOTRANSMIT ハンドルを出力パラメーターとして提供します。 SerCx2 とシリアルコントローラードライバーは、このハンドルを使用して、後続の PIO 転送トランザクションでオブジェクトを参照します。 詳細については、「 [SERCX2 PIO-送信トランザクション](https://docs.microsoft.com/previous-versions/dn265336(v=vs.85))」を参照してください。


[SerCx2PioTransmitCreate](https://docs.microsoft.com/windows-hardware/drivers/ddi/sercx/nf-sercx-sercx2piotransmitcreate)が PIO 送信オブジェクトを作成した後、このオブジェクトは、シリアルコントローラーデバイスを表すフレームワークデバイスオブジェクトの有効期間にわたって存在します。 PIO 転送オブジェクトは、デバイスオブジェクトが削除されると自動的に削除されます。 シリアルコントローラードライバーは、 [Wdfobjectdelete](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfobject/nf-wdfobject-wdfobjectdelete)などのメソッドを呼び出すことによって、PIO 転送オブジェクトを削除し_ない_ようにする必要があります。

シリアルコントローラードライバーは、PIO 転送オブジェクトを1つだけ作成する必要があります。 ドライバーは、システム DMA 転送オブジェクトまたはカスタム転送オブジェクトを作成する前に、このオブジェクトを作成する必要があります。 システム DMA 転送オブジェクトの詳細については、「 [SERCX2SYSTEMDMATRANSMIT Object Handle](#sercx2systemdmatransmit-object-handle)」を参照してください。 カスタム転送オブジェクトの詳細については、「 [SERCX2CUSTOMTRANSMIT Object Handle](#sercx2customtransmit-object-handle)」を参照してください。

##  <a name="sercx2systemdmareceive-object-handle"></a>SERCX2SYSTEMDMARECEIVE オブジェクトハンドル
SERCX2SYSTEMDMARECEIVE オブジェクトハンドルは、serial framework extension (SerCx2) のバージョン2のシステム DMA 受信オブジェクトへの非透過的な参照です。

[SerCx2SystemDmaReceiveCreate](https://docs.microsoft.com/windows-hardware/drivers/ddi/sercx/nf-sercx-sercx2systemdmareceivecreate)メソッドは、システム DMA 受信オブジェクトを作成します。 SerCx2 は、このオブジェクトを使用して、シリアルコントローラーからデータを読み取るシステム DMA トランザクションを管理します。 このオブジェクトはシリアルコントローラードライバーに対して非透過的です。 
[SerCx2SystemDmaReceiveCreate](https://docs.microsoft.com/windows-hardware/drivers/ddi/sercx/nf-sercx-sercx2systemdmareceivecreate)は、新しく作成された SERCX2SYSTEMDMARECEIVE ハンドルを出力パラメーターとして提供します。 SerCx2 とシリアルコントローラードライバーは、このハンドルを使用して、その後のシステム DMA-receive トランザクションでオブジェクトを参照します。 詳細については、「 [SerCx2-Receive](https://docs.microsoft.com/previous-versions/dn265343(v=vs.85))transaction」を参照してください。

[SerCx2SystemDmaReceiveCreate](https://docs.microsoft.com/windows-hardware/drivers/ddi/sercx/nf-sercx-sercx2systemdmareceivecreate)によってシステム DMA オブジェクトが作成された後、このオブジェクトは、シリアルコントローラーデバイスを表すフレームワークデバイスオブジェクトの有効期間にわたって存在します。 Device オブジェクトが削除されると、システムの DMA 受信オブジェクトは自動的に削除されます。 シリアルコントローラードライバーは、オプションとして、システム DMA 受信オブジェクトを作成できますが、そのようなオブジェクトは1つしか作成できません。 ドライバーは、次の条件下でのみこのオブジェクトを作成できます。

* ドライバーにより、以前に PIO 受信オブジェクトが作成されました。
* ドライバーにより、カスタム受信オブジェクトが作成され_ていません_。

PIO 受信オブジェクトの詳細については、「 [SERCX2PIORECEIVE Object Handle](#sercx2pioreceive-object-handle)」を参照してください。 カスタム受信オブジェクトの詳細については、「 [SERCX2CUSTOMRECEIVE Object Handle](#sercx2customreceive-object-handle)」を参照してください。

##  <a name="sercx2systemdmatransmit-object-handle"></a>SERCX2SYSTEMDMATRANSMIT オブジェクトハンドル
SERCX2SYSTEMDMATRANSMIT オブジェクトハンドルは、serial framework extension (SerCx2) のバージョン2のシステム DMA 転送オブジェクトへの非透過的な参照です。

[SerCx2SystemDmaTransmitCreate](https://docs.microsoft.com/windows-hardware/drivers/ddi/sercx/nf-sercx-sercx2systemdmatransmitcreate)メソッドは、システムの DMA 送信オブジェクトを作成します。 SerCx2 は、このオブジェクトを使用して、シリアルコントローラーにデータを書き込むシステム DMA トランザクションを管理します。 このオブジェクトはシリアルコントローラードライバーに対して非透過的です。 
[SerCx2SystemDmaTransmitCreate](https://docs.microsoft.com/windows-hardware/drivers/ddi/sercx/nf-sercx-sercx2systemdmatransmitcreate)は、新しく作成されたシステム DMA 送信オブジェクトへの SERCX2SYSTEMDMATRANSMIT ハンドルを出力パラメーターとして提供します。 SerCx2 とシリアルコントローラードライバーは、このハンドルを使用して、その後のシステム DMA 送信トランザクションでオブジェクトを参照します。 詳細については、「 [SerCx2 トランザクション](https://docs.microsoft.com/previous-versions/dn265338(v=vs.85))」を参照してください。

[SerCx2SystemDmaTransmitCreate](https://docs.microsoft.com/windows-hardware/drivers/ddi/sercx/nf-sercx-sercx2systemdmatransmitcreate)によってシステム DMA オブジェクトが作成された後、このオブジェクトは、シリアルコントローラーデバイスを表すフレームワークデバイスオブジェクトの有効期間にわたって存在します。 デバイスオブジェクトが削除されると、システムの DMA 送信オブジェクトが自動的に削除されます。 シリアルコントローラードライバーは、 [Wdfobjectdelete](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfobject/nf-wdfobject-wdfobjectdelete)などのメソッドを呼び出すことによって、システム DMA 転送オブジェクトを削除し_ない_ようにする必要があります。

シリアルコントローラードライバーは、オプションとして、システム DMA 転送オブジェクトを作成できますが、そのようなオブジェクトは1つしか作成できません。 ドライバーは、次の条件に当てはまる場合にのみ、このオブジェクトを作成でき </wdcml: p >

* ドライバーは、以前に PIO 送信オブジェクトを作成しました。
* ドライバーにより、カスタム送信オブジェクトが作成され_ていません_。

PIO 転送オブジェクトの詳細については、「 [SERCX2PIOTRANSMIT Object Handle](#sercx2piotransmit-object-handle)」を参照してください。 カスタム転送オブジェクトの詳細については、「 [SERCX2CUSTOMTRANSMIT Object Handle](#sercx2customtransmit-object-handle)」を参照してください。

## <a name="related-topics"></a>関連トピック

[SerCx2 カスタム-Receive トランザクション](https://docs.microsoft.com/windows-hardware/drivers/serports/sercx2-custom-receive-transactions)

[SerCx2 カスタム送信トランザクション](https://docs.microsoft.com/previous-versions/dn265320(v=vs.85))

[SerCx2 PIO-トランザクションを受信する](https://docs.microsoft.com/previous-versions/dn265332(v=vs.85))

[SerCx2 PIO-送信トランザクション](https://docs.microsoft.com/previous-versions/dn265336(v=vs.85))

[SerCx2-DMA-トランザクションの受信](https://docs.microsoft.com/previous-versions/dn265343(v=vs.85))

[SerCx2-送信トランザクション](https://docs.microsoft.com/previous-versions/dn265338(v=vs.85))

[SerCx2CustomReceiveTransactionCreate](https://docs.microsoft.com/windows-hardware/drivers/ddi/sercx/nf-sercx-sercx2customreceivetransactioncreate)

[SerCx2CustomTransmitCreate](https://docs.microsoft.com/windows-hardware/drivers/ddi/sercx/nf-sercx-sercx2customtransmitcreate)

[SerCx2CustomTransmitTransactionCreate](https://docs.microsoft.com/windows-hardware/drivers/ddi/sercx/nf-sercx-sercx2customtransmittransactioncreate)

[SerCx2PioReceiveCreate](https://docs.microsoft.com/windows-hardware/drivers/ddi/sercx/nf-sercx-sercx2pioreceivecreate)

[SerCx2PioReceiveCreate](https://docs.microsoft.com/windows-hardware/drivers/ddi/sercx/nf-sercx-sercx2pioreceivecreate)

[SerCx2PioTransmitCreate](https://docs.microsoft.com/windows-hardware/drivers/ddi/sercx/nf-sercx-sercx2piotransmitcreate)

[SerCx2SystemDmaReceiveCreate](https://docs.microsoft.com/windows-hardware/drivers/ddi/sercx/nf-sercx-sercx2systemdmareceivecreate)

[SerCx2SystemDmaTransmitCreate](https://docs.microsoft.com/windows-hardware/drivers/ddi/sercx/nf-sercx-sercx2systemdmatransmitcreate)

[フレームワークオブジェクトの概要](https://docs.microsoft.com/windows-hardware/drivers/wdf/summary-of-framework-objects)

[WdfObjectDelete](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfobject/nf-wdfobject-wdfobjectdelete)





