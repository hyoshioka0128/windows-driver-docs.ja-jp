---
title: IEC-61883 プロトコル ドライバー
description: IEC-61883 プロトコル ドライバー
ms.assetid: d1e639f0-a22f-4005-86a7-fdbfe509265b
keywords:
- IEC 61883 クライアント ドライバー WDK IEEE 1394 バス
- 61883 WDK IEEE 1394 バス
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: b367d0090ae956e0ae3f20bdeb5cd9afae8a3cd8
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67385778"
---
# <a name="iec-61883-protocol-driver"></a>IEC-61883 プロトコル ドライバー





IEC 61883 プロトコル ドライバー、 *61883.sys*、IEC 61883 1 の仕様で定義されている関数制御プロトコル (FCP)、共通 isochronous パケット (CIP) の形式、および接続管理の手順 (CMP) をサポートしています。 プロトコル ドライバーは、要求からのパケット ヘッダーのストリームを削除し、スキャッター/ギャザーをサポートし、大量のデータを効率的に移動するバッファーのコピーを制限します。

IEC 61883 クライアント ドライバーは、IEEE 1394 バスに接続されるデバイスに IEC 61883 コマンドを発行する*61883.h*を発行し、 [ **IRP\_MJ\_内部\_デバイス\_コントロール**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-internal-device-control) I/O 制御コードに IRP [ **IOCTL\_61883\_クラス**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/61883/ni-61883-ioctl_61883_class)します。 クライアント ドライバーでは、パラメーターをパッケージ化、 [ **AV\_61883\_要求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/61883/ns-61883-_av_61883_request)内でポインターを渡します構造体であり、 **Parameters.Others.Argument1** IRP のメンバー。 **関数**AV のメンバー\_61883\_要求の構造は、操作の種類を決定します。 AV\_61883\_構造体には、データの共用体の要求固有のパラメーターが含まれています。 要求が構造要求の種類ごとに 1 つ。

 

 




