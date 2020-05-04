---
title: 間接的な Display Driver Model の概要
description: 間接ディスプレイドライバーモデルは、従来の GPU 表示出力に接続されていないモニターをサポートする簡易ユーザーモードドライバーモデルを提供するように設計されています。
ms.assetid: E2E64500-5F99-42A7-8945-B496026EA142
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c319e4a330fe5c0bfccd40af2cdd4686a08a8874
ms.sourcegitcommit: 5598b4c767ab56461b976b49fd75e4e5fb6018d2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2020
ms.locfileid: "82104616"
---
# <a name="indirect-display-driver-model-overview"></a>間接的な Display Driver Model の概要


間接ディスプレイドライバーモデルは、従来の GPU 表示出力に接続されていないモニターをサポートする簡易ユーザーモードドライバーモデルを提供するように設計されています。 たとえば、USB を使用して PC に接続されたドングルで、標準 (VGA、DVI、HDMI、DP など) モニターが接続されているとします。

## <a name="span-iddriver_implementationspanspan-iddriver_implementationspanspan-iddriver_implementationspandriver-implementation"></a><span id="Driver_Implementation"></span><span id="driver_implementation"></span><span id="DRIVER_IMPLEMENTATION"></span>ドライバーの実装


間接表示ドライバーモデルは、UMDF クラス拡張として実装されます。 ドライバーはデバイスの UMDF ドライバーであり、IddCx (間接ディスプレイドライバークラス拡張) によって公開されている機能を使用して、windows グラフィックスサブシステムとのインターフェイスを提供します。

## <a name="span-idindirect_display_driver_functionalityspanspan-idindirect_display_driver_functionalityspanspan-idindirect_display_driver_functionalityspanindirect-display-driver-functionality"></a><span id="Indirect_Display_Driver_Functionality"></span><span id="indirect_display_driver_functionality"></span><span id="INDIRECT_DISPLAY_DRIVER_FUNCTIONALITY"></span>ディスプレイドライバーの間接的な機能


間接ディスプレイドライバーは、UMDF ドライバーであるため、デバイス通信、電源管理、プラグアンドプレイなどのすべての UMDF 機能を担当します。IddCx は、次の方法で Windows グラフィックスサブシステムと対話するための間接ディスプレイドライバーへのインターフェイスを提供します。

1. 間接ディスプレイデバイスを表すグラフィックスアダプターを作成する
2. レポートモニターがシステムに接続され、切断されている
3. 接続されているモニターの説明を入力します
4. 使用可能な表示モードを指定する
5. ハードウェアマウスカーソル、ガンマ、I2C 通信、保護されたコンテンツなどの他の表示機能をサポートします。
6. モニターに表示するデスクトップイメージを処理する間接ディスプレイドライバーは、セッション0で実行されている UMDF ドライバーであり、ユーザーセッションで実行されているコンポーネントがないため、ドライバーが不安定になってもシステム全体の安定性に影響しません。

## <a name="span-iduser_mode_modelspanspan-iduser_mode_modelspanspan-iduser_mode_modelspanuser-mode-model"></a><span id="User_Mode_Model"></span><span id="user_mode_model"></span><span id="USER_MODE_MODEL"></span>ユーザーモードモデル


間接表示ドライバーは、カーネルモードコンポーネントがサポートされていないユーザーモードのみのモデルであるため、ドライバーは、デスクトップイメージを処理するために任意の DirectX API を使用できます。 実際、IddCx は DirectX サーフェイスでエンコードするデスクトップイメージを提供します。

**注**  間接ディスプレイドライバーは、複数の windows プラットフォームで使用できるように、ユニバーサル windows ドライバーとしてビルドする必要があります。

 

ビルド時に、UMDF 間接表示ドライバーは、ビルドされた IddCx のバージョンを宣言し、OS はドライバーの読み込み時に正しいバージョンの IddCx が読み込まれることを保証します。

次のセクションでは、間接ディスプレイドライバーモデルについて説明します。

[IddCx オブジェクト](iddcx-objects.md)  
[デバッグ](indirect-display-debugging.md)
 
## <a name="sample-code"></a>サンプル コード

Microsoft では、 [Windows Driver Samples GitHub](https://github.com/microsoft/Windows-driver-samples/tree/master/video/IndirectDisplay)にある間接ディスプレイドライバーの実装例を提供しています。 このサンプルでは、モニターに接続する方法、モードセットに応答する方法、およびフレームを受信する方法を示します。

 





