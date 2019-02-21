---
title: ACPI のデバイスのサポート
description: ACPI のデバイスのサポート
ms.assetid: ebaf2e66-4f56-48ca-93ca-f34e694c0d73
keywords:
- Advanced Configuration and Power Interface Specification WDK
- ACPI デバイス WDK
- ACPI デバイス WDK、ACPI デバイスについて
- 定義は、WDK ACPI をブロックします。
- 操作のリージョン WDK ACPI
- 操作リージョン ハンドラー WDK ACPI
- 機能ドライバー WDK ACPI
- WDM 関数ドライバー WDK ACPI
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3d0d544118b6e030ed46b1008fc4116f6a4af724
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56539597"
---
# <a name="supporting-acpi-devices"></a>ACPI のデバイスのサポート


このセクションでは、仕入先 WDM 関数ドライバー内での使い方 Windows Advanced Configuration and Power Interface (ACPI) デバイスの機能を強化するためにについて説明します。

ACPI のデバイスには、バッテリ、熱ゾーンは、システムを ACPI 名前空間で定義されているその他のデバイスなどの低レベルのシステム デバイスが含まれます。 ACPI の名前空間は、ACPI BIOS を使用してオブジェクトを参照する階層の名前空間です。

システム提供の結合操作[ACPI ドライバー](https://msdn.microsoft.com/library/windows/hardware/ff540493)と ACPI BIOS は ACPI デバイスの基本的な機能をサポートし、オペレーティング システムの残りの部分に対して透過的です。 ACPI のデバイスを ACPI システムの説明テーブルの定義のブロックを指定します。 デバイスの定義のブロックには、デバイス データにアクセスするために使用するデバイスのメモリの連続したブロックを指定する操作領域が、特に指定します。

ACPI デバイスの機能を強化するために、ベンダーは WDM 関数ドライバー、ドライバーによって提供される操作のリージョンの ACPI BIOS と通信を指定できます。 ACPI ドライバーでは、関数のドライバーによって提供される操作リージョン ハンドラーを呼び出すことによって操作の領域にアクセスします。

ACPI 操作リージョン経由の通信、によって関数ドライバー直接にアクセスできるは、通常はデバイスのみ、BIOS によって制御され、BIOS は、ドライバーと、ホスト システムの構成に依存しているデバイスに固有の操作を呼び出すことができます。 基本的な動作メカニズムは次のとおりです。

1.  ACPI BIOS では、読み取るか、デバイスの操作のリージョンにデータを書き込みます。

2.  営業地域にアクセスするには、ACPI ドライバーは、function ドライバーの操作のリージョン ハンドラーを呼び出します。

3.  操作のリージョンのハンドラーは任意のアクションへのアクセスは、設定し、アクセスに関連する情報を返します。

次の 2 つの例では、ACPI デバイスの機能を強化するために、仕入先が関数のドライバーを使用する方法を示します。

1.  ACPI、デバイス ドライバーがプレインストールされているソフトウェアのベンダーのサウンド カード ボリューム コントロールを有効にすると、function ドライバーの操作のリージョン内のインデックスにアクセスできます。

2.  ドライバーは、バッテリ、熱のゾーンの温度および他の操作が、通常の残りの容量を監視、BIOS でのみアクセスします。

次のトピックでは、デバイスの ACPI 関数ドライバーを提供する方法について説明します。

[デバイスの ACPI デバイス スタック](device-stacks-for-an-acpi-device.md)

[ACPI 関数デバイスの操作](operation-of-an-acpi-device-function-driver.md)

システム提供についてサポートを参照してください、ACPI デバイス関数のドライバーをサポートするルーチン[ACPI 操作リージョン ハンドラーの参照](https://msdn.microsoft.com/library/windows/hardware/ff536132)します。

ACPI のデバイスと名前空間の詳細については、次を参照してください。、 [Advanced Configuration and Power Interface (ACPI) 仕様](https://go.microsoft.com/fwlink/p/?linkid=866846)します。
