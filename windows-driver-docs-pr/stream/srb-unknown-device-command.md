---
title: SRB\_不明な\_デバイス\_コマンド
description: SRB\_不明な\_デバイス\_コマンド
ms.assetid: 89bc2176-e384-48bf-82d8-4a8ab2bd5159
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0b7864c4ee05783fbb261ebb4b45c1b47fa9ee5a
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72837702"
---
# <a name="srb_unknown_device_command"></a>SRB\_不明な\_デバイス\_コマンド


## <span id="ddk_srb_unknown_device_command_ks"></span><span id="DDK_SRB_UNKNOWN_DEVICE_COMMAND_KS"></span>


クラスドライバーは、ミニドライバーに対する処理方法がわからないことを示す Irp を渡すために、この要求を送信します。 *pSrb*-&gt;**irp**がハンドルされていない irp をポイントしています。 「 [**HW\_STREAM\_REQUEST\_BLOCK**](https://docs.microsoft.com/windows-hardware/drivers/ddi/strmini/ns-strmini-_hw_stream_request_block)」を参照してください。

この要求は、stream クラスが理解していない irp の IRP パススルーメカニズムとして使用できますが、ミニドライバーになる可能性があります。 たとえば、ストリームクラスで処理されないプラグアンドプレイ (PnP) Irp がいくつかありますが、1394カメラドライバーでは処理されません。

ミニドライバーが SRB\_不明な\_デバイス\_コマンドをサポートしていない場合、または IRP を処理しない場合は、pSRB-&gt;Status を STATUS\_\_実装されていない状態に設定する必要があります。

 

 





