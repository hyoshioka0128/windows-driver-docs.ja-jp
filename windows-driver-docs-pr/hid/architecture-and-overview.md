---
title: I ² C トランスポートにおける HID のアーキテクチャと概要
description: このセクションでは、I ² C トランスポートで HID をサポートするデバイスのドライバースタックについて説明します。
ms.assetid: 99384729-552C-4847-AA35-E0D413018104
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: df411e628dc8937c3d8cad6214758aa3c46b5d69
ms.sourcegitcommit: 188596c90e03a5619b5cbf0bff4276fc94777253
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/08/2020
ms.locfileid: "84519847"
---
# <a name="architecture-and-overview-for-hid-over-the-ic-transport"></a>I ² C トランスポートにおける HID のアーキテクチャと概要


このセクションでは、I ² C トランスポートで HID をサポートするデバイスのドライバースタックについて説明します。

## <a name="architecture-and-overview"></a>アーキテクチャと概要


HID I ² C ドライバースタックは、Microsoft によって提供される既存のコンポーネントと新しいコンポーネントと、I ² C シリコンの製造元によって提供されるコンポーネントで構成されています。 次の図は、スタックとこれらのコンポーネントを示しています。

![i2c ドライバースタック経由の hid](images/hid-i2c-arch.png)

Windows 8 では、オペレーティングシステムと効果的に通信する低電力の単純なバス用のインターフェイスが提供されています。 このインターフェイスは、単純な周辺機器バス (SPB) と呼ばれ、クロス統合回線 (I ² C) とシリアル周辺装置インターフェイス (SPI) のようなバスをサポートします。 SPB の詳細については、「単純な周辺機器」を参照してください。

Windows 8 には、KMDF ベースの HID ミニポートドライバーが用意されています。これは、I ² C で HID 用のプロトコル仕様のバージョン1.0 を実装しています。 このドライバーには HIDI2C という名前が付けられています。 Windows は、互換性のある ID の一致に基づいてこのドライバーを読み込みます。これは、Advanced Configuration and Power Interface (ACPI) によって公開されます。 このドライバーにより、hid ioctl と API セットを利用するソフトウェアに対して、HID Ioctl を使用するアプリのアプリケーションレベルの互換性が確保されます。 デバイスは、要注意またはデータがある場合に、ホストをアサートします。 ただし、アサーションが発生する前に、GPIO 接続が存在している必要があります。

**メモ**   HIDI2C デバイスドライバーは、I ² C バスだけをサポートしています。 Windows 8 では、SPI、SM、またはその他の低電力のバスはサポートされていません。

 

## <a name="the-ic-controller-driver"></a>I ² C コントローラードライバー


I ² C コントローラードライバーは、シリアル周辺機器バス (SPB) の IOCTL インターフェイスを公開して、読み取りと書き込みの操作を実行します。 このドライバーは、実際のコントローラーの組み込み (たとえば、I ² C) を提供します。 SPB クラス拡張は、コントローラードライバーの代わりに、リソースハブとのすべての対話を処理し、同時ターゲットを管理するために必要なキューを実装します。

**メモ**   HID I ² C ドライバーは、SPB プラットフォームと互換性のある I ² C バスを搭載していないシステムでは機能しません。 システムの製造元に問い合わせて、デバイスシステムの I ² C バスが SPB プラットフォームと互換性があるかどうかを確認します。

 

## <a name="the-gpio-controller-driver"></a>GPIO コントローラードライバー


General Purpose 入出力 (GPIO) コントローラーは、GPIO 経由でデバイスから割り込みを配信します。 これは多くの場合、GPIO ピンを使用して新しいデータやその他のイベントのウィンドウを通知する単純な下位コンポーネントです。 GPIO は、I ² C チャネル以外の方法でデバイスを制御することもできます。

## <a name="the-resource-hub"></a>リソースハブ


Soc プラットフォームでの接続は、通常、検出できません。これは、SoC で使用されるバス上のデバイス列挙の標準が存在しないためです。 そのため、これらのデバイスは、Advanced Configuration and Power Interface (ACPI) で静的に定義されている必要があります。 さらに、コンポーネントは、厳密な分岐ツリー構造ではなく、複数のバスにまたがる複数の依存関係を持つことがよくあります。

リソースハブは、すべてのデバイスとバスコントローラーの間の接続を管理するプロキシです。 HIDI ² C ドライバーは、リソースハブを使用して、デバイスが開いている要求を適切なコントローラードライバーに再ルーティングします。 リソースハブの詳細については、「 [sp 接続デバイスの接続 id](https://docs.microsoft.com/windows-hardware/drivers/spb/connection-ids-for-spb-connected-peripheral-devices) 」を参照してください。

 

 




