---
title: 最上位のコレクション
description: 最上位のコレクション
ms.assetid: dcbee8e3-d03a-45c8-92e4-0897b9f55177
keywords:
- WDK を非表示に最上位のコレクション
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: aecf67d9b3ef2e1e242ff26dc865421935e25eb3
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63376760"
---
# <a name="top-level-collections"></a>最上位のコレクション




A*上位レベルのコレクション*特定ソフトウェア コンシューマー (またはコンシューマーの種類) の機能を対象とする機能のグループです。 たとえば、上位レベルのコレクションは、キーボード、マウス、コンシューマー コントロール、センサー、表示などとして記述することがあります。HID 仕様では、これら上位レベルのコレクションも呼びます*アプリケーション コレクション*します。 HID デバイスでは、上位レベルのコレクションにする可能性がある対象を識別するために、HID 機能のコンシューマーを許可するために各上位レベルのコレクションの目的について説明します。 、Windows では、HID デバイス セットアップ クラス (HIDClass) は、レポート記述子によって記述された上位レベルのコレクションごとに一意の物理デバイス オブジェクト (PDO) を生成します。
Microsoft の定義、*最上位のコレクション*として、 [HID コレクション](hid-collections.md)いない別のコレクション内で入れ子になっています。 入れ子になっていないコレクションは、HID 型に関係なく、最上位のコレクションでは常にします。 具体的には、最上位のコレクションは、する必要はありません、**アプリケーション**USB HID 標準で定義されているコレクション。

レポート記述子には、1 つ以上の最上位のコレクションを含めることができます。 HID クラス ドライバーは、入力デバイスの最上位のコレクションを列挙し、物理デバイス オブジェクトを作成します (*PDO*) の各最上位のコレクション。 ユーザー モード アプリケーションまたはカーネル モード ドライバーの PDO を開きを使用して最上位のコレクションにアクセスできる、 [HIDClass サポート ルーチン](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/_hid/#hidclass-support-routines)と[HID クラス ドライバーの Ioctl](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/_hid/#hid-class-driver-ioctls)します。

内部構造と最上位のコレクションの機能は、次のように記載されています。

-   A [ **HIDP\_CAP** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/hidpi/ns-hidpi-_hidp_caps)構造体は、最上位レベルをまとめたものです[コレクションの機能](collection-capability.md)します。

-   [コレクションをリンク](link-collections.md)最上位のコレクションに含まれる入れ子になったサブコレクションの構成について説明します。

-   [配列の機能をボタン](button-capability-arrays.md)と[機能配列値](value-capability-arrays.md)最上位のコレクションでサポートされているコントロールの機能について説明します。

 





