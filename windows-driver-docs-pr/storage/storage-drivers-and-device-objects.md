---
title: ストレージ ドライバーとデバイス オブジェクト
description: ストレージ ドライバーとデバイス オブジェクト
ms.assetid: dbadebe6-b2ae-4dc2-837b-5ca9634d45d0
keywords:
- ストレージドライバー WDK、デバイスオブジェクト
- デバイスオブジェクト WDK ストレージ
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 12295a676b489f194b03b118466845b3de3d699b
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72844483"
---
# <a name="storage-drivers-and-device-objects"></a>ストレージ ドライバーとデバイス オブジェクト


## <span id="ddk_storage_drivers_and_device_objects_kg"></span><span id="DDK_STORAGE_DRIVERS_AND_DEVICE_OBJECTS_KG"></span>


記憶装置スタックは、システム上の記憶装置への i/o 処理に関係するドライバーによって作成されたデバイスオブジェクトのツリーで構成されます。 このツリーのルートは、記憶域アダプターまたは記憶域スタックと統合された別のドライバースタックの機能デバイスオブジェクト (FDO) です。 このツリーのリーフは、ファイルシステムおよびユーザーモードアプリケーションが使用するデバイスオブジェクトです。

任意の PnP ドライバーと同様に、ストレージクラスまたは記憶域フィルタードライバーは、 **IoCreateDevice**を使用してデバイスオブジェクトを作成し、 **Ioattachdevicetodevicestack**を使用してデバイススタックにアタッチすることによって、AddDevice ルーチンのツリーにそれ自体を追加します。初期化時に PnP マネージャーによってドライバーの AddDevice ルーチンに渡されたデバイスオブジェクトへのポインター。 **Ioattachdevicetodevicestack**新しいデバイスオブジェクトをデバイススタックの現在の上にアタッチします。

Tape miniclass、medium チェンジャー miniclass、または SCSI ミニポートドライバーは、デバイスオブジェクトを作成し、デバイススタックに接続するためには必要ありません。 代わりに、システムによって提供されるテープクラス、チェンジャークラス、または SCSI ポートドライバーが、miniclass/ミニポートに代わってこれらのタスクを処理し、miniclass/ミニポートドライバールーチンを呼び出して、デバイスオブジェクトを作成するために必要なデータを収集します。

記憶域ポートドライバーは、種類が FILE\_デバイス\_大容量\_記憶装置の物理デバイスオブジェクト (PDOs) を作成します。 ディスククラス、CD-ROM クラス、テープクラス、およびチェンジャークラスのドライバーは、種類がファイル\_デバイス\_ディスク、ファイル\_デバイス\_CD\_ROM、ファイル\_デバイス\_テープの FDOs を作成します。、およびファイルはそれぞれ、デバイス\_チェンジャーを\_します。

PnP ドライバーの設計の詳細については、 [Pnp ドライバーの設計ガイドライン](https://docs.microsoft.com/windows-hardware/drivers/kernel/pnp-driver-design-guidelines)を参照してください。 PnP 関連の **Io * * Xxx*ルーチンの詳細については、[プラグアンドプレイルーチン](https://docs.microsoft.com/windows-hardware/drivers/ddi/index)を参照してください。

 

 




