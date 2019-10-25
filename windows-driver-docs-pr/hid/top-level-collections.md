---
title: 最上位のコレクション
description: 最上位のコレクション
ms.assetid: dcbee8e3-d03a-45c8-92e4-0897b9f55177
keywords:
- 最上位のコレクション WDK HID
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c81669a91100c57fb5a5449c4f8e9aeca11f0a67
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72841546"
---
# <a name="top-level-collections"></a>最上位のコレクション




*最上位レベルのコレクション*は、機能の特定のソフトウェアコンシューマー (またはコンシューマーの種類) を対象とする機能をグループ化したものです。 たとえば、最上位レベルのコレクションは、キーボード、マウス、コンシューマーコントロール、センサー、ディスプレイなどとして記述できます。HID 仕様では、これらの最上位レベルのコレクションは*アプリケーションコレクション*とも呼ばれます。 Hid デバイスは、必要になる可能性のある最上位レベルのコレクションを HID 機能のコンシューマーが特定できるように、最上位レベルのコレクションの目的を説明します。 Windows では、HID デバイスセットアップクラス (HIDClass) によって、レポート記述子によって記述される最上位レベルのコレクションごとに一意の物理デバイスオブジェクト (PDO) が生成されます。
Microsoft では、*最上位のコレクション*を、別のコレクション内で入れ子になっていない[HID コレクション](hid-collections.md)として定義しています。 入れ子になっていないコレクションは、その HID 型に関係なく、常に最上位レベルのコレクションです。 特に、最上位レベルのコレクションは、USB HID 標準で定義されているように、**アプリケーション**コレクションである必要はありません。

レポート記述子には、複数の最上位レベルのコレクションを含めることができます。 HID クラスドライバーは、入力デバイスの最上位のコレクションを列挙し、最上位レベルのコレクションごとに物理デバイスオブジェクト (*PDO*) を作成します。 ユーザーモードアプリケーションまたはカーネルモードドライバーは、その PDO を開き、 [HIDClass サポートルーチン](https://docs.microsoft.com/windows-hardware/drivers/ddi/_hid/#hidclass-support-routines)と[HID クラスドライバー ioctl](https://docs.microsoft.com/windows-hardware/drivers/ddi/_hid/#hid-class-driver-ioctls)を使用して、最上位のコレクションにアクセスできます。

最上位レベルのコレクションの内部構造と機能については、次の説明を参照してください。

-   [**Hidp\_CAPS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/hidpi/ns-hidpi-_hidp_caps)構造体は、最上位レベルの[コレクションの機能](collection-capability.md)をまとめたものです。

-   [リンクコレクション](link-collections.md)は、最上位のコレクション内に含まれる入れ子になったサブコレクションの編成を表します。

-   [ボタン機能配列](button-capability-arrays.md)と[値機能配列](value-capability-arrays.md)は、最上位のコレクションでサポートされているコントロールの機能を記述します。

 





