---
title: ミニドライバーの初期化
description: ミニドライバーの初期化
ms.assetid: 5aa4e2c6-5848-45fe-8a89-686aae7e85e6
keywords:
- ストリーミング ミニドライバー WDK Windows 2000 のカーネルの初期化
- Stream.sys クラス ドライバー WDK Windows 2000 のカーネル、ミニドライバーの初期化
- ストリーミング ミニドライバー WDK Windows 2000 のカーネルの初期化
- WDK Windows 2000 カーネル ストリーミング、ミニドライバーの初期化
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: b342ce22bf19d69aa5439c0be646a5c5f734556c
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67363300"
---
# <a name="minidriver-initialization"></a>ミニドライバーの初期化





ミニドライバーの呼び出すようにミニドライバーは、まずオペレーティング システムに初期化**DriverEntry**ルーチン。 参照してください[ **Stream クラス ミニドライバーの DriverEntry**](https://docs.microsoft.com/previous-versions/ff558717(v=vs.85))します。 呼び出してにクラス ドライバーを使用した、ミニドライバーを登録する必要があります[ **StreamClassRegisterMinidriver**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/strmini/nf-strmini-streamclassregisteradapter)します。

ミニドライバー パス、 [ **HW\_初期化\_データ**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/strmini/ns-strmini-_hw_initialization_data)クラス ドライバーをデバイス全体にわたるコールバックを含む、暫定的な情報を提供する構造体[ *StrMiniReceiveDevicePacket*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/strmini/nc-strmini-phw_receive_device_srb)、 [ *StrMiniCancelPacket*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/strmini/nc-strmini-phw_cancel_srb)、 [ *StrMiniRequestTimeout*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/strmini/nc-strmini-phw_request_timeout_handler)、および[ *StrMiniInterrupt*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/strmini/nc-strmini-phw_interrupt)します。

クラスのドライバーを使用し、 [ *StrMiniReceiveDevicePacket* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/strmini/nc-strmini-phw_receive_device_srb)デバイスを初期化する必要がありますが、ミニドライバーを通知します。 SRB 送信\_初期化\_デバイスの要求を渡します、 [**ポート\_構成\_情報**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/strmini/ns-strmini-_port_configuration_information)必要な構造体ハードウェアの情報。 この要求を完了すると、ミニドライバーがのバイト単位のサイズを指定、 [ **HW\_ストリーム\_記述子**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/strmini/ns-strmini-_hw_stream_descriptor)構造がそのストリームのすべてを説明するために使用します。

クラスのドライバーを使用して、ミニドライバーは、その要求を完了すると、 [ *StrMiniReceiveDevicePacket* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/strmini/nc-strmini-phw_receive_device_srb) 、SRB を送信する\_取得\_ストリーム\_情報要求。 ミニドライバーは、すべての各ストリームのコールバックを含め、そのストリームに関する情報を提供します。

使用して、クラス ドライバーでは、ストリーム データの処理が完了すると、 [ *StrMiniReceiveDevicePacket* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/strmini/nc-strmini-phw_receive_device_srb) 、SRB を送信する\_初期化\_要求を完了します。 この時点で、ミニドライバーは、各ストリームで要求の処理を開始する準備が。

 

 




