---
title: 間接的な Display Driver Model の概要
description: 間接的な表示ドライバー モデルは、従来の GPU 表示出力に接続されていないモニターをサポートするためにシンプルなユーザー モード ドライバー モデルを提供するように設計されました。
ms.assetid: E2E64500-5F99-42A7-8945-B496026EA142
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3be4062bb6e9d2e9664ae6dfacf61507a0a46184
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63325057"
---
# <a name="indirect-display-driver-model-overview"></a>間接的な Display Driver Model の概要


間接的な表示ドライバー モデルは、従来の GPU 表示出力に接続されていないモニターをサポートするためにシンプルなユーザー モード ドライバー モデルを提供するように設計されました。 たとえば、ドングルは、通常 (VGA、DVI、HDMI、配布ポイントなど) モニターに接続されている USB 経由で PC に接続します。

## <a name="span-iddriverimplementationspanspan-iddriverimplementationspanspan-iddriverimplementationspandriver-implementation"></a><span id="Driver_Implementation"></span><span id="driver_implementation"></span><span id="DRIVER_IMPLEMENTATION"></span>ドライバーの実装


間接的なディスプレイ ドライバー モデルは、UMDF クラスの拡張機能として実装されます。 ドライバーは、デバイスの UMDF ドライバーであり、windows グラフィックス サブシステムとのインターフェイス IddCx (間接的なディスプレイ ドライバーのクラスの拡張機能) によって公開される機能を使用します。

## <a name="span-idindirectdisplaydriverfunctionalityspanspan-idindirectdisplaydriverfunctionalityspanspan-idindirectdisplaydriverfunctionalityspanindirect-display-driver-functionality"></a><span id="Indirect_Display_Driver_Functionality"></span><span id="indirect_display_driver_functionality"></span><span id="INDIRECT_DISPLAY_DRIVER_FUNCTIONALITY"></span>間接的なディスプレイ ドライバーの機能


間接的なディスプレイ ドライバーは、UMDF ドライバーでは、デバイス間の通信、電源管理、プラグ アンド プレイなどのすべての UMDF 機能を担当します。IddCx では、次の方法で Windows グラフィックス サブシステムと対話する間接的なディスプレイ ドライバーへのインターフェイスを提供します。

1. 間接的なディスプレイ デバイスを表すグラフィックス アダプターを作成します。
2. レポートで監視される接続し、システムから切断されています。
3. 接続されているモニターを説明します。
4. 使用可能な表示モードします。
5. ハードウェアは、マウスのカーソル、ガンマ、I2C 通信と、保護されたコンテンツと同様に、他の表示機能をサポートします。
6. プロセス、デスクトップが間接的な表示のドライバーがセッション 0 で実行されている UMDF ドライバーであるため、モニターに表示するイメージ、ドライバーが不安定になるの全体として、システムの安定性に影響しませんので、ユーザー セッションで実行されている任意のコンポーネントがありません。

## <a name="span-idusermodemodelspanspan-idusermodemodelspanspan-idusermodemodelspanuser-mode-model"></a><span id="User_Mode_Model"></span><span id="user_mode_model"></span><span id="USER_MODE_MODEL"></span>ユーザー モードのモデル


間接的なディスプレイ ドライバーがカーネル モード コンポーネントはサポートされていないユーザー モードのみモデルの場合、ドライバーが、デスクトップのイメージを処理するために、DirectX API を使用できるためです。 実際には、IddCx DirectX サーフェスでエンコードするデスクトップ イメージを提供します。

**注**  間接的なディスプレイ ドライバーは複数の Windows プラットフォームで使用できるように、ユニバーサル windows ドライバーとしてビルドする必要があります。

 

、ビルド時に、UMDF 間接的なディスプレイ ドライバーが IddCx ビルドされた対象のバージョンを宣言し、オペレーティング システムにより、ドライバーが読み込まれるときに、IddCx の正しいバージョンが読み込まれているようになります。

次のセクションでは、間接 Display Driver Model をについて説明します。

[IddCx オブジェクト](iddcx-objects.md)
 

 





