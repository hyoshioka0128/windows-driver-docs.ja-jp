---
title: COPP の概要
description: COPP の概要
ms.assetid: a5f77c60-418d-4931-8922-ca2ae080da2e
keywords:
- コピー防止 WDK COPP、バージョン情報
- ビデオコピー防止 WDK COPP, COPP について
- COPP WDK DirectX VA、COPP について
- 保護されたビデオ WDK COPP、バージョン情報
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 78a33f7472170631f34a1011ab0dd8fff636bde0
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72840351"
---
# <a name="introduction-to-copp"></a>COPP の概要


## <span id="ddk_introduction_to_the_certified_output_protection_protocol_gg"></span><span id="DDK_INTRODUCTION_TO_THE_CERTIFIED_OUTPUT_PROTECTION_PROTOCOL_GG"></span>


**このセクションは、Windows Server 2003 SP1 以降、および Windows XP SP2 以降にのみ適用されます。**

COPP は、グラフィックスアダプターによって出力されるビデオにコピー防止を適用するメカニズムを提供します。 COPP は、 [**ioctl\_VIDEO\_HANDLE\_VIDEOPARAMETERS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddvdeo/ni-ntddvdeo-ioctl_video_handle_videoparameters) i/o CONTROL (ioctl) コードを使用するよりも、さまざまなリンク保護要件を、より保護された方法でグラフィックスアダプターに送信するための共通のプロトコルを提供します。

次のトピックでは、COPP について説明します。

[COPP で使用される暗号プリミティブ](cryptographic-primitives-used-by-copp.md)

[セキュリティで保護されたチャネルを介した通信](communicating-through-a-secure-channel.md)

[COPP をサポートするためのグラフィックスアダプターの出力要件](graphics-adapter-output-requirements-to-support-copp.md)

 

 





