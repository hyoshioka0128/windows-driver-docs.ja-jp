---
title: SRB\_不明な\_デバイス\_コマンド
description: SRB\_不明な\_デバイス\_コマンド
ms.assetid: 89bc2176-e384-48bf-82d8-4a8ab2bd5159
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6701f014b637320d4c681c0fe67b164881738444
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63364817"
---
# <a name="srbunknowndevicecommand"></a>SRB\_不明な\_デバイス\_コマンド


## <span id="ddk_srb_unknown_device_command_ks"></span><span id="DDK_SRB_UNKNOWN_DEVICE_COMMAND_KS"></span>


クラスのドライバーでは、ミニドライバーに処理する方法が不明に Irp を渡すには、この要求を送信します。 *pSrb*-&gt;**Irp**未処理 IRP を指します。 参照してください[ **HW\_ストリーム\_要求\_ブロック**](https://msdn.microsoft.com/library/windows/hardware/ff559702)します。

この要求は、ストリーム クラスが認識しないが、ミニドライバーが Irp の IRP のパススルー メカニズムとして使用できます。 1394 カメラのドライバーが、そのストリーム クラスを処理しません、いくつかのプラグ アンド プレイ (PnP) Irp があるなど。

ミニドライバーは SRB をサポートしていない場合\_不明な\_デバイス\_コマンドまたは IRP を処理しないを設定する必要があります pSRB -&gt;状態の状態を\_いない\_実装されていません。

 

 





