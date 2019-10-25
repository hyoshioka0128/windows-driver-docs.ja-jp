---
title: ミニドライバーの制御フロー
description: ミニドライバーの制御フロー
ms.assetid: c3c23d32-4023-445b-bd89-e0b454bec1ed
keywords:
- .Sys クラスドライバー WDK Windows 2000 カーネル、制御フロー
- streaming ミニドライバー WDK Windows 2000 カーネル、制御フロー
- ミニドライバー WDK Windows 2000 カーネルストリーミング、制御フロー
- 初期化されていない streaming ミニドライバー WDK streaming ミニドライバー
- streaming ミニドライバー WDK Windows 2000 カーネルを初期化しています
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 38e6a1eb3b114cebe51eb41d59f8a8781064ec95
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72842136"
---
# <a name="minidriver-flow-of-control"></a>ミニドライバーの制御フロー





次の一連の手順は、通常、ストリーミングミニドライバーの初期化、使用、および初期化解除に従います。 参照される次のコマンドと構造体については、このドキュメントの他の部分で説明します。

**ストリーミングミニドライバーの初期化、使用、および初期化解除の手順は次のとおりです。**

1.  ミニドライバーによってサポートされるハードウェアアダプターは、プラグアンドプレイ列挙子によって検出されます。 列挙子は、シンボリック参照を解決するためにレジストリをチェックし、i/o サブシステムに要求を渡します。

2.  I/o サブシステムは、ミニドライバーを読み込み、ミニドライバーの**driverentry**ルーチン ( [**Stream クラスミニドライバーの driverentry**](https://docs.microsoft.com/previous-versions/ff558717(v=vs.85))を参照) を呼び出します。ここでは、 [**HW\_初期化\_データ**](https://docs.microsoft.com/windows-hardware/drivers/ddi/strmini/ns-strmini-_hw_initialization_data)構造が割り当てられ、初期化されます。 **Driverentry**ルーチンの情報からファイルオブジェクトが作成されます。

3.  次に、ミニドライバーの**Driverentry**ルーチンは、stream クラスドライバーの[**StreamClassRegisterMinidriver**](https://docs.microsoft.com/windows-hardware/drivers/ddi/strmini/nf-strmini-streamclassregisteradapter)関数を呼び出し、 [**HW\_初期化\_データ**](https://docs.microsoft.com/windows-hardware/drivers/ddi/strmini/ns-strmini-_hw_initialization_data)構造体をパラメーターとして渡します。 HW\_初期化\_データ構造には、SRBs を処理するミニドライバー関数のアドレスが含まれます。 これにより、ミニドライバーはクラスドライバーによって送信された SRBs に応答できるようになります。

4.  初期化中、stream クラスドライバーは、 [**HW\_初期化\_データ**](https://docs.microsoft.com/windows-hardware/drivers/ddi/strmini/ns-strmini-_hw_initialization_data)構造体の**HwReceivePacket**メンバーに指定された関数を呼び出します (「 [*strminireceivedevicepacket*](https://docs.microsoft.com/windows-hardware/drivers/ddi/strmini/nc-strmini-phw_receive_device_srb)」を参照)。 **コマンド**メンバーが SRB に設定され、\_デバイス\_初期化されます。 次に、ミニドライバーはハードウェアアダプターを初期化します。

5.  Stream クラスドライバーは、 [**HW\_初期化\_データ**](https://docs.microsoft.com/windows-hardware/drivers/ddi/strmini/ns-strmini-_hw_initialization_data)構造体の**HwReceivePacket**メンバーに指定された関数を呼び出します。このメンバーは、SRB によって\_ストリーム\_情報を取得\_ます。 次に、ミニドライバーは、サポートしているストリームに関する情報を返します。

6.  Stream クラスドライバーは、hw **\_初期化\_データ**構造体の**HwReceivePacket**メンバーに指定された関数を呼び出します。このメンバーには、SRB\_OPEN\_stream と、 [**hw\_stream\_オブジェクト**](https://docs.microsoft.com/windows-hardware/drivers/ddi/strmini/ns-strmini-_hw_stream_object)があります。データ. ミニドライバーは、指定されたストリームを開くために必要なハードウェアアクションを実行します。

7.  Stream クラスドライバーは、\_SRB を渡すことによってストリームからデータを送信または要求します。または、\_データの読み取りまたは\_データの書き込みコマンド\_、HW\_ストリームの**ReceiveDataPacket**メンバーに指定されている関数に渡し\_ストリームのオブジェクト構造。

8.  Stream クラスドライバーは、適切なストリーム要求ブロック ([**HW\_stream\_request\_block**](https://docs.microsoft.com/windows-hardware/drivers/ddi/strmini/ns-strmini-_hw_stream_request_block)) を指定された関数に渡すことによって、ストリームのプロパティおよびその他のコントロール情報を取得して設定します **。** \_ストリームのオブジェクト構造\_HW ストリームのメンバー。

9.  システムがストリームを使用しているときに、stream クラスドライバーは、 [**HW\_初期化\_データ**](https://docs.microsoft.com/windows-hardware/drivers/ddi/strmini/ns-strmini-_hw_initialization_data)構造体の**HwReceivePacket**\_メンバーに指定された関数を呼び出し\_ストリームを閉じます。 次に、ミニドライバーは指定されたストリームを閉じます。

10. アダプターの初期化を解除する時間が経過すると、stream クラスのドライバーは、 [**HW\_初期化\_データ**](https://docs.microsoft.com/windows-hardware/drivers/ddi/strmini/ns-strmini-_hw_initialization_data)構造体の**HwReceivePacket**メンバーに指定された関数を呼び出して、SRB\_非初期化\_デバイスで呼び出します。 その後、ミニドライバーはデバイスを初期化前します。

 

 




