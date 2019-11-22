---
title: ミニドライバーの初期化
description: ミニドライバーの初期化
ms.assetid: 5aa4e2c6-5848-45fe-8a89-686aae7e85e6
keywords:
- streaming ミニドライバー WDK Windows 2000 カーネルを初期化しています
- ミニドライバーを初期化する .sys クラスドライバー WDK Windows 2000 カーネル
- streaming ミニドライバー WDK Windows 2000 カーネル, 初期化
- ミニドライバー WDK Windows 2000 カーネルストリーミング, 初期化
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: e2e561bfc937c39a9d4987a754ad2b7ecd236b3c
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72842135"
---
# <a name="minidriver-initialization"></a>ミニドライバーの初期化





オペレーティングシステムは、最初にミニドライバーを初期化するときに、ミニドライバーの**Driverentry**ルーチンを呼び出します。 [**ストリームクラスミニドライバーの Driverentry を**](https://docs.microsoft.com/previous-versions/ff558717(v=vs.85))参照してください。 ミニドライバーは、 [**StreamClassRegisterMinidriver**](https://docs.microsoft.com/windows-hardware/drivers/ddi/strmini/nf-strmini-streamclassregisteradapter)を呼び出すことによって、それ自体をクラスドライバーに登録する必要があります。

ミニドライバーは、[**ハードウェア\_初期化\_データ**](https://docs.microsoft.com/windows-hardware/drivers/ddi/strmini/ns-strmini-_hw_initialization_data)構造体を渡します。これにより、デバイス全体のコールバック、 [*Strminireceivedevicepacket*](https://docs.microsoft.com/windows-hardware/drivers/ddi/strmini/nc-strmini-phw_receive_device_srb)、 [*StrMiniCancelPacket*](https://docs.microsoft.com/windows-hardware/drivers/ddi/strmini/nc-strmini-phw_cancel_srb)、 [*Strminirequesttimeout*](https://docs.microsoft.com/windows-hardware/drivers/ddi/strmini/nc-strmini-phw_request_timeout_handler)、 [*strminiinterrupt*](https://docs.microsoft.com/windows-hardware/drivers/ddi/strmini/nc-strmini-phw_interrupt)などの暫定情報がクラスドライバーに提供されます。

次に、クラスドライバーは[*Strminireceivedevicepacket*](https://docs.microsoft.com/windows-hardware/drivers/ddi/strmini/nc-strmini-phw_receive_device_srb)を使用して、デバイスを初期化する必要があることをミニドライバーに通知します。 このメソッドは、SRB\_INITIALIZE\_DEVICE 要求を送信し、必要なハードウェア情報を含む[**ポート\_構成\_情報**](https://docs.microsoft.com/windows-hardware/drivers/ddi/strmini/ns-strmini-_port_configuration_information)構造体を渡します。 この要求を完了すると、ミニドライバーは、すべてのストリームを記述するために使用する[**HW\_ストリーム\_記述子**](https://docs.microsoft.com/windows-hardware/drivers/ddi/strmini/ns-strmini-_hw_stream_descriptor)構造のバイト単位のサイズを提供します。

ミニドライバーが要求を完了すると、クラスドライバーは[*Strminireceivedevicepacket*](https://docs.microsoft.com/windows-hardware/drivers/ddi/strmini/nc-strmini-phw_receive_device_srb)を使用して SRB\_GET\_STREAM\_INFO 要求を送信します。 その後、ミニドライバーは、各ストリームのコールバックを含む、すべてのストリームに関する情報を提供します。

クラスドライバーは、ストリームデータの処理を終了した後、 [*Strminireceivedevicepacket*](https://docs.microsoft.com/windows-hardware/drivers/ddi/strmini/nc-strmini-phw_receive_device_srb)を使用して、SRB\_初期化\_要求の完了を送信します。 この時点で、ミニドライバーは各ストリームで要求の処理を開始する準備ができています。

 

 




