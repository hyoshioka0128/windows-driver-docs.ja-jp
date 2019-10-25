---
title: I/O 要求に関する情報の取得
description: I/O 要求に関する情報の取得
ms.assetid: a686ea00-6987-480a-a4ce-892e1efbed87
keywords:
- WDK KMDF の処理を要求し、情報を取得しています
- I/o 要求 WDK KMDF、に関する情報の取得
- 状態情報 WDK KMDF
- 状態情報 WDK KMDF、i/o 要求
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8f3948d53a3e6645a6e6d2102c05b2330ab28ade
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72843137"
---
# <a name="obtaining-information-about-an-io-request"></a>I/O 要求に関する情報の取得


I/o 要求を処理する前に、ドライバーは要求の種類を決定する必要があります。 フレームワークベースのドライバーによってデバイスの i/o[キューが作成さ](creating-i-o-queues.md)れると、通常は、各キューまたは要求ハンドラーが特定の種類 (読み取り、書き込み、またはデバイスの i/o 制御) の要求を受信するように、i/o キューと要求ハンドラーが設定されます。

要求の種類を決定したら、必要に応じて、ドライバーが要求の入力バッファーと出力バッファーを取得する必要があります。 要求のバッファーを取得する方法の詳細については、「[フレームワークベースのドライバーでのデータバッファーへのアクセス](https://docs.microsoft.com/windows-hardware/drivers/wdf/accessing-data-buffers-in-wdf-drivers)」を参照してください。

ドライバーによって受信された i/o 要求に関する追加情報を提供するために、framework request オブジェクトは次のメソッドを定義します。

-   [**Wdfrequestgetioqueue**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfrequest/nf-wdfrequest-wdfrequestgetioqueue)。 i/o 要求の配信元の i/o キューへのハンドルを返します。

-   [**WdfRequestGetRequestorMode**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfrequest/nf-wdfrequest-wdfrequestgetrequestormode)。要求の発信元のプロセッサアクセスモード (ユーザーまたはカーネル) を返します。

-   [**Wdfrequestgetfileobject**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfrequest/nf-wdfrequest-wdfrequestgetfileobject)。要求に関連付けられているフレームワークファイルオブジェクトへのハンドルを返します。

-   [**Wdfrequestwdmgetirp**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfrequest/nf-wdfrequest-wdfrequestwdmgetirp)。要求に関連付けられている WDM [**IRP**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_irp)構造体を返します。

-   [**Wdfrequestgetparameters**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfrequest/nf-wdfrequest-wdfrequestgetparameters)。これは、WDM 形式の非 IRP 要求パラメーターを取得します。

ドライバーが i/o 要求を完了した後、ドライバースタック内の他のドライバーは、要求の完了情報を取得するために、追加の要求オブジェクトメソッドを呼び出すことができます。 これらの追加の方法の詳細については、「 [I/o 要求の完了](completing-i-o-requests.md)」を参照してください。

 

 





