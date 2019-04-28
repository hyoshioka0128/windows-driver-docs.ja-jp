---
title: DirectX VA COPP デバイス
description: DirectX VA COPP デバイス
ms.assetid: f9268b38-3317-4c4f-b9c1-e0ad3c88f92e
keywords:
- COPP デバイス WDK DirectX VA
- WDK COPP、COPP デバイス保護をコピーします。
- ビデオのコピー防止 WDK COPP、COPP デバイス
- COPP WDK DirectX VA、COPP デバイス
- ビデオの WDK COPP COPP デバイスを保護
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c70743891b3a1c48dc327e6a9f5186ab093edf54
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63380416"
---
# <a name="directx-va-copp-device"></a>DirectX VA COPP デバイス


## <span id="ddk_directx_va_copp_device_gg"></span><span id="DDK_DIRECTX_VA_COPP_DEVICE_GG"></span>


このセクションには、Windows Server 2003 SP1 にのみ以降が適用されますおよび Windows XP SP2 以降。

DirectX VA COPP デバイスがビデオ セッションごとに作成されるように、ディスプレイ ドライバーを実装する必要があります。 COPP デバイスは、COPP コマンドおよび状態要求を受信するエンドポイントを表します。 COPP デバイスには、関連付けられている物理コネクタの保護の設定も格納されます。 物理的なコネクタでは、複数のコンテンツ保護の種類をサポートできます。 など、s-ビデオ コネクタはアナログの (A CGMS) 保護のコンテンツ生成管理システムに加えて、アナログ コンテンツ保護 (ACP) をサポートできます。 詳細については、次を参照してください。 [COPP デバイス クラスを定義する](defining-the-copp-device-class.md)します。

別のプロセスが COPP を通じてグラフィックス アダプターの出力の設定を構成できるようにするため、COPP デバイスの複数のインスタンスが必要です。 そのため、複数のビデオ セッションは、システム上でアクティブなときに各 COPP デバイスが適切に動作できるように、COPP デバイス クラスを実装する必要があります。

**注**  可能性がある 1 つまたは複数のビデオ サブストリームを組み合わせて、ビデオ ストリームのビデオ セッションで構成されます。 ビデオのセッションが特定のグラフィックス アダプターの出力のコネクタに関連付けられています。 複数のビデオ セッションは、システムには、1 つのプロセスはアクティブにすることはできます。

 

 

 





