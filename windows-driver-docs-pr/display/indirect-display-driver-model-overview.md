---
title: 間接ディスプレイドライバーモデルの概要
description: 間接ディスプレイドライバーモデルは、従来の GPU 表示出力に接続されていないモニターをサポートする簡易ユーザーモードドライバーモデルを提供するように設計されています。
ms.assetid: E2E64500-5F99-42A7-8945-B496026EA142
ms.date: 07/17/2020
ms.localizationpriority: medium
ms.openlocfilehash: 162732b980b5970b90459ccd53f4d1d97ffc1d29
ms.sourcegitcommit: 0d89fc46058efb2ebc6ed9bd8f638c3f8cc1a678
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/18/2020
ms.locfileid: "86459211"
---
# <a name="indirect-display-driver-model-overview"></a>間接ディスプレイドライバーモデルの概要

間接ディスプレイドライバー (IDD) モデルは、従来の GPU 表示出力に接続されていないモニターをサポートするためのシンプルなユーザーモードドライバーモデルを提供するように設計されています。 たとえば、USB を使用して PC に接続されたドングルは、通常の (VGA、DVI、HDMI、DP など) モニターが接続されています。

## <a name="idd-implementation"></a>IDD 実装

IDD は、 [UMDF](/windows-hardware/drivers/wdf/getting-started-with-umdf-version-2)クラス拡張として実装されます。 IDD は、開発者が指定したデバイス用の UMDF ドライバーであり、 [IddCx](/windows-hardware/drivers/ddi/iddcx/) (間接ディスプレイドライバークラス拡張) によって公開されている機能を使用して、windows グラフィックスサブシステムとのインターフェイスを提供します。

![UMDF アーキテクチャ内の間接ディスプレイドライバー](images/idd_umdf_arch.png)

## <a name="idd-functionality"></a>IDD の機能

IDD は UMDF ドライバーであるため、デバイス通信、電源管理、プラグアンドプレイなどのすべての UMDF 機能を担当します。IDD は、次の方法で、IddCx インターフェイスを使用して、Windows グラフィックスサブシステムと対話します。

* 間接ディスプレイデバイスを表すグラフィックスアダプターを作成する
* レポートモニターがシステムに接続され、切断されている
* 接続されているモニターの説明を入力します
* 使用可能な表示モードを指定する
* ハードウェアマウスカーソル、ガンマ、I2C 通信、保護されたコンテンツなどの他の表示機能をサポートします。
* モニターに表示するデスクトップイメージを処理する

IDD は、[セッション 0](/windows-hardware/drivers/wdf/session-zero-guidelines-for-umdf-drivers)で、ユーザーセッションで実行されているコンポーネントなしで実行されるため、すべてのドライバーが不安定になると、システム全体の安定性に影響を与えることはありません。

## <a name="user-mode-model"></a>ユーザーモードモデル

IDD は、カーネルモードコンポーネントがサポートされていない、ユーザーモードのみのモデルです。 そのため、ドライバーは、デスクトップイメージを処理するために任意の DirectX Api を使用できます。 実際、IddCx は DirectX サーフェイスでエンコードするデスクトップイメージを提供します。 ドライバーでは、GDI、ウィンドウ Api、OpenGL、Vulkan など、ドライバーの使用に適していないユーザーモード Api を呼び出すことはできません。

> [!NOTE]
>
> IDD は、複数の Windows プラットフォームで使用できるように、[ユニバーサル windows ドライバー](/windows-hardware/drivers/gettingstarted/writing-a-umdf-driver-based-on-a-template)として構築する必要があります。

ビルド時に、UMDF IDD は構築された IddCx のバージョンを宣言し、OS はドライバーが読み込まれるときに正しいバージョンの IddCx が読み込まれることを保証します。

次のセクションでは、IDD モデルについて説明します。

[IddCx オブジェクト](iddcx-objects.md)  
[デバッグ](indirect-display-debugging.md)

## <a name="sample-code"></a>サンプル コード

Microsoft では、 [Windows Driver Samples GitHub](https://github.com/microsoft/Windows-driver-samples/tree/master/video/IndirectDisplay)でサンプルの IDD 実装を提供しています。 このサンプルでは、モニターに接続する方法、モードセットに応答する方法、およびフレームを受信する方法を示します。
