---
title: PnP シリアル ポートと COM ポートをインストールする
description: PnP シリアル ポートと COM ポートをインストールする
ms.assetid: 48a489a1-6ed9-4e17-a7b5-0f2325486ab6
keywords:
- シリアル ドライバー WDK、プラグ アンド プレイ デバイス
- プラグ アンド プレイ シリアル デバイス WDK
- シリアル デバイス WDK、プラグ アンド プレイ
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: a54ad46994756effe287f65ea4ac87802511a8ef
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63331180"
---
# <a name="installing-plug-and-play-serial-ports-and-com-ports"></a>PnP シリアル ポートと COM ポートをインストールする





既定では、ポートのクラスのインストーラーと関数のシリアル ドライバーの結合操作は、COM ポートとしてシリアル ポートを構成します。 シリアル インターフェイスを作成します COM ポート デバイス シリアル ポートの場合、 **SerialSkipExternalNaming**デバイスのエントリの値が存在しないか、0 に設定されます。 シリアルが COM ポートの COM ポート デバイス インターフェイスを作成する方法と、この操作を上書きする方法の詳細については、次を参照してください。[外部名前付けの COM ポート](external-naming-of-com-ports.md)します。

ポート クラスのインストーラーは、シリアル ポートをインストールするときに、次のタスクを実行します。

1. COM ポート番号を選択し、ポート名を設定、 **PortName**デバイスのハードウェア キーの下のエントリの値。 ポート名が形式 COM<em>&lt;n&gt;</em>ここで、 *&lt;n&gt;* のポート番号です。 シリアルの値を使用してシリアル シリアル ポートの COM ポートのインターフェイスを作成した場合**PortName**として COM ポートのシンボリック リンクの名前。

2. 既定プロパティ ページ ダイアログ ボックス、ポートの設定を選択すると、表示します。 カスタム プロパティ ページをインストールする方法については、次を参照してください。 [COM ポートを、高度なプロパティ ページをインストールする](installing-an-advanced-properties-page-for-a-com-port.md)します。

3. デバイスのデバイスのフレンドリ名を設定します。 SPDRP を使用して名前を取得する\_FRIENDLYNAME フラグを**SetupDiGetDeviceRegistryProperty**します。

設定する共同インストーラーを指定する[プラグ アンド プレイ シリアル デバイス用のレジストリ設定](registry-settings-for-a-plug-and-play-serial-device.md)します。 エントリの値がレジストリに存在しない場合は、シリアル ポートの既定値を使用します。

 

 




