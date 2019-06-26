---
title: COPP の概要
description: COPP の概要
ms.assetid: a5f77c60-418d-4931-8922-ca2ae080da2e
keywords:
- コピー防止 COPP についての WDK COPP
- ビデオのコピー防止 COPP についての WDK COPP
- COPP WDK DirectX VA、COPP について
- COPP についてのビデオの WDK COPP の保護
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: fc211133b3b750103df74f29b38fdb3565f4b7d8
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67379883"
---
# <a name="introduction-to-copp"></a>COPP の概要


## <span id="ddk_introduction_to_the_certified_output_protection_protocol_gg"></span><span id="DDK_INTRODUCTION_TO_THE_CERTIFIED_OUTPUT_PROTECTION_PROTOCOL_GG"></span>


**このセクションでは、Windows Server 2003 SP1 以降、および Windows XP SP2 以降にのみ適用されます。**

COPP は、コピー防止をグラフィックス アダプターによって出力されるビデオに適用するメカニズムを提供します。 COPP を使用してさまざまなリンク保護要件をよりもより確実に保護の方法でグラフィックス アダプターに送信するための一般的なプロトコルを提供する、 [ **IOCTL\_ビデオ\_処理\_VIDEOPARAMETERS** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddvdeo/ni-ntddvdeo-ioctl_video_handle_videoparameters) I/O 制御 (IOCTL) コード。

次のトピックでは、COPP について説明します。

[COPP で使用される暗号プリミティブ](cryptographic-primitives-used-by-copp.md)

[セキュリティで保護されたチャネル経由の通信](communicating-through-a-secure-channel.md)

[COPP をサポートするグラフィックス アダプターの出力の要件](graphics-adapter-output-requirements-to-support-copp.md)

 

 





