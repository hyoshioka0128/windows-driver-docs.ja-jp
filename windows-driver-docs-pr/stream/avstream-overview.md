---
title: AVStream の概要
description: AVStream の概要
ms.assetid: 305039fe-0a00-4f3e-ae1a-61c50a2f2fb3
keywords:
- AVStream WDK、AVStream ミニドライバーについて
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: bb71dadba059f7a01b5a84743ea7ee3edbd96088
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67386697"
---
# <a name="avstream-overview"></a>AVStream の概要





AVStream は、ビデオのみストリーミングと統合されたオーディオ/ビデオ ストリーミングをサポートする Microsoft 提供のマルチ メディア クラス ドライバーです。 エクスポートのドライバーで、オペレーティング システムの一部として Microsoft から提供 AVStream *Ks.sys*します。 ハードウェア ベンダーの記述の下で実行するミニドライバー *Ks.sys*します。

オーディオ ドライバーの優先クラス ドライバーは、Microsoft から提供されたオーディオ[port クラス](https://docs.microsoft.com/windows-hardware/drivers/audio/introduction-to-port-class)ドライバー。 オーディオのベンダーの下で実行するミニドライバーを書き込む必要があります*Portcls.sys*します。

マイクロソフトは、サポート、[クラスのストリーム](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/_stream/index)ミニドライバーの既存のドライバーのみです。

AVStream ドライバーは 98 の DirectX 8.0 が Gold またはそれ以降のバージョンまたはそれ以降のバージョンがインストールされている Microsoft Windows XP、Microsoft Windows Server 2003、または Windows の任意のプラットフォームでビルドします。

Windows XP より前のオペレーティング システムでビルドする場合は、最新使用可能な DirectX ドライバー開発キット (DDK) を使用することを確認します。 DirectX 9.0 には AVStream、カーネル ストリーミングのコンポーネント、およびストリーム クラスの更新プログラムが含まれています。

AVStream は、ベンダーに重要な利点を提供します。

-   少ないコードを生成するために必要とするミニドライバー ライター。

-   ストリーミング オーディオとビデオの両方のミニドライバーのクラス モデルの統一されたカーネルを提供します。

-   ユーザー モードのプラグインを記述するベンダーのサポートを提供します。これらは、プロパティの値にアクセスするメソッドを提供する COM インターフェイスです。 ミニドライバーの既存のバイナリを変更することがなく、プラグインを行うことができます。 詳細については、次を参照してください。[カーネル ストリーミング プロキシ プラグイン](kernel-streaming-proxy-plug-ins-design-guide.md)します。

AVStream ドライバー モデルで次の図に示すように、ベンダーは Microsoft から提供されたクラスのドライバーと対話するミニドライバーを指定します。

![avstream と ks サービス間の関係を示す図](images/avstream.png)

 

 




