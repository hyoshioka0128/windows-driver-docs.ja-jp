---
title: IEC-61883 プロトコル ドライバー
description: IEC-61883 プロトコル ドライバー
ms.assetid: d1e639f0-a22f-4005-86a7-fdbfe509265b
keywords:
- IEC-61883 クライアントドライバー WDK IEEE 1394 bus
- 61883 WDK IEEE 1394 bus
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d18dcea1667af8def5ae437e283d7ec6f9048077
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72841538"
---
# <a name="iec-61883-protocol-driver"></a>IEC-61883 プロトコル ドライバー





IEC 61883 プロトコルドライバー ( *61883*) は、iec 61883-1 仕様で定義されているように、関数制御プロトコル (FCP)、common アイソクロナスパケット (CIP) 形式、および接続管理プロシージャ (CMP) をサポートしています。 プロトコルドライバーは、要求からストリームパケットヘッダーを取り除き、スキャッター/ギャザーをサポートし、大量のデータを効率的に移動するようにバッファーコピーを制限します。

IEEE 1394 バスに接続されているデバイスに対して IEC 61883 コマンドを発行するには61883、MJ をインクルードし、 [**irp\_\_内部\_デバイス\_制御**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-internal-device-control)irp を i/o 制御コード[**IOCTL\_61883\_クラス**](https://docs.microsoft.com/windows-hardware/drivers/ddi/61883/ni-61883-ioctl_61883_class)を使用して発行し*ます*。 クライアントドライバーは、 [**AV\_61883\_要求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/61883/ns-61883-_av_61883_request)構造のパラメーターをパッケージ化し、そのパラメーターへのポインターを IRP の**引数 1**メンバーに渡します。 AV\_61883\_要求構造の**関数**メンバーによって、操作の種類が決まります。 AV\_61883\_要求構造には、要求の種類ごとに1つのデータ構造体の和集合での要求固有のパラメーターが含まれています。

 

 




