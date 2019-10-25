---
title: AVStream の概要
description: AVStream の概要
ms.assetid: 305039fe-0a00-4f3e-ae1a-61c50a2f2fb3
keywords:
- AVStream WDK、AVStream ミニドライバーについて
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6f5fe45f865f4c08dc04a458f61e3d478f2e8f67
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72845283"
---
# <a name="avstream-overview"></a>AVStream の概要





AVStream は、ビデオのみのストリーミングと統合オーディオ/ビデオストリーミングをサポートする、Microsoft が提供するマルチメディアクラスのドライバーです。 Microsoft では、エクスポートドライバー *Ks*のオペレーティングシステムの一部として avstream を提供しています。 ハードウェアベンダーは、 *Ks*で実行されるミニドライバーを書き込みます。

オーディオドライバー用の優先クラスドライバーは、Microsoft が提供するオーディオ[ポートクラス](https://docs.microsoft.com/windows-hardware/drivers/audio/introduction-to-port-class)ドライバーです。 オーディオベンダーは、 *Portcls*で実行されるミニドライバーを作成する必要があります。

Microsoft では、既存のミニドライバーに対してのみ[stream クラス](https://docs.microsoft.com/windows-hardware/drivers/ddi/_stream/index)ドライバーをサポートしています。

AVStream ドライバーは、Microsoft Windows XP、Microsoft Windows Server 2003、または DirectX 8.0 以降のバージョンがインストールされているプラットフォームの Windows 98 Gold 以降のバージョンでビルドされます。

Windows XP より前のオペレーティングシステムでビルドする場合は、利用可能な最新の DirectX Driver Development Kit (DDK) を使用していることを確認してください。 DirectX 9.0 には、AVStream、カーネルストリーミングコンポーネント、およびストリームクラスの更新プログラムが含まれています。

AVStream は、次の方法でベンダーに大きな利点をもたらします。

-   ミニドライバーライターにより少ないコードを生成する必要があります。

-   オーディオとビデオミニドライバーの両方に対応する、統一されたカーネルストリーミングクラスモデルを提供します。

-   ユーザーモードのプラグインを作成するためのベンダーのサポートを提供します。これらは、プロパティ値にアクセスするメソッドを提供する COM インターフェイスです。 既存のミニドライバーバイナリを変更せずにプラグインを提供できます。 詳細については、「[カーネルストリーミングプロキシプラグイン](kernel-streaming-proxy-plug-ins-design-guide.md)」を参照してください。

AVStream ドライバーモデルでは、ベンダーは、次の図に示すように、Microsoft が提供するクラスドライバーと対話するミニドライバーを提供します。

![avstream と ks サービスの関係を示す図](images/avstream.png)

 

 




