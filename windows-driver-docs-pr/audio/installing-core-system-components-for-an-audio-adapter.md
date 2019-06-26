---
title: オーディオ アダプター用のコア システム コンポーネントのインストール
description: オーディオ アダプター用のコア システム コンポーネントのインストール
ms.assetid: fc14867e-cae8-4381-bcd3-ec2230050cf6
keywords:
- オーディオ アダプター WDK、システム コンポーネント
- アダプターのドライバー WDK オーディオ、システム コンポーネント
- ポート クラス オーディオ アダプター WDK、システム コンポーネント
ms.date: 10/27/2017
ms.localizationpriority: medium
ms.openlocfilehash: d859d977c824f930de7e3dde9b59c8519fdad2b5
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67359878"
---
# <a name="installing-core-system-components-for-an-audio-adapter"></a>オーディオ アダプター用のコア システム コンポーネントのインストール


## <span id="installing_core_system_components_for_an_audio_adapter"></span><span id="INSTALLING_CORE_SYSTEM_COMPONENTS_FOR_AN_AUDIO_ADAPTER"></span>


このセクションには、ポート クラス オーディオ アダプターのコアのシステム コンポーネントのインストールの詳細については、次のトピックが含まれています。

[Windows でのインストール](installing-in-windows.md)

[ **INF DDInstall セクション**](https://docs.microsoft.com/windows-hardware/drivers/install/inf-ddinstall-section)製造元ので、各ハードウェア ID が指定されて**モデル**セクションを含めることを指定する必要があります、 **KS します。登録**Ks.inf」セクションおよび**WDMAUDIO します。登録**Wdmaudio.inf」セクション。 Ks.inf ファイルは、ストリーミング コンポーネント core カーネルをインストールします。 Wdmaudio.inf ファイルには、コア WDM オーディオ コンポーネントがインストールされます。 ベンダーは、変更またはこれらのシステム INF ファイルを置換する必要がありますできません。

 

 




