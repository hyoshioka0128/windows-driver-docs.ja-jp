---
title: ACPI デバイスをサポートする
description: ACPI デバイスをサポートする
ms.assetid: ebaf2e66-4f56-48ca-93ca-f34e694c0d73
keywords:
- 高度な構成と電源インターフェイスの仕様 WDK
- ACPI デバイス WDK
- ACPI デバイス WDK、ACPI デバイスについて
- 定義が WDK ACPI をブロックする
- 操作リージョン WDK ACPI
- 操作領域ハンドラー WDK ACPI
- 関数ドライバー WDK ACPI
- WDM 関数ドライバー WDK ACPI
ms.date: 05/19/2020
ms.localizationpriority: medium
ms.openlocfilehash: ff58e1a5e37f3338f76d2837b3dd039318e04556
ms.sourcegitcommit: cbcb712a9f1f62c7d67e1b98097a0d8d24bd0c71
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/21/2020
ms.locfileid: "83769330"
---
# <a name="supporting-acpi-devices"></a>ACPI デバイスをサポートする

このセクションでは、ベンダーが Windows の WDM 関数ドライバーを使用して、Advanced Configuration and Power Interface (ACPI) デバイスの機能を強化する方法について説明します。

ACPI デバイスには、バッテリ、サーマルゾーン、システムの ACPI 名前空間で定義されているその他のデバイスなどの低レベルのシステムデバイスが含まれます。 ACPI 名前空間は、ACPI BIOS がオブジェクトを参照するために使用する階層的な名前空間です。

システム提供の[acpi ドライバー](https://docs.microsoft.com/windows-hardware/drivers/kernel/acpi-driver)と acpi BIOS の組み合わせ操作は、acpi デバイスの基本的な機能をサポートしており、オペレーティングシステムの他の部分に対して透過的です。 Acpi デバイスは、ACPI システムの説明テーブルの定義ブロックによって指定されます。 デバイスの定義ブロックは、特に、デバイスデータへのアクセスに使用されるデバイスメモリの連続したブロックを指定する操作領域を指定します。

ACPI デバイスの機能を強化するために、ベンダーは、ドライバーによって提供される操作領域を通じて ACPI BIOS と通信する WDM 関数ドライバーを提供できます。 ACPI ドライバーは、関数ドライバーによって提供される操作領域ハンドラーを呼び出すことによって、操作領域にアクセスします。

ACPI 操作リージョンを介して通信することにより、関数ドライバーは通常、BIOS によってのみ制御されるデバイスに間接的にアクセスできます。また、BIOS は、ドライバーおよびホストシステムの構成に依存するデバイス固有の操作を呼び出すことができます。 基本的な動作メカニズムは次のとおりです。

1. ACPI BIOS は、デバイスの操作領域内のデータの読み取りまたは書き込みを行います。

1. 操作領域にアクセスするために、ACPI ドライバーは関数ドライバーの操作領域ハンドラーを呼び出します。

1. 操作領域ハンドラーは、アクセスに対してプログラミングされているすべてのアクションを実行し、アクセスに関連付けられている情報を返します。

次の2つの例は、ベンダーが関数ドライバーを使用して、ACPI デバイスの機能を強化する方法を示しています。

1. ACPI デバイスは、ドライバーが製造元のプレインストールされたソフトウェアでサウンドカードのボリューム制御を有効にする関数ドライバーの操作領域内のインデックスにアクセスできます。

1. ドライバーは、バッテリの残りの容量、温度のあるゾーンの温度、および通常 BIOS によってのみアクセスされるその他の処理を監視します。

次のトピックでは、ACPI デバイスの関数ドライバーを指定する方法について説明します。

[ACPI デバイスのデバイス スタック](device-stacks-for-an-acpi-device.md)

[ACPI デバイス機能ドライバーの操作](operation-of-an-acpi-device-function-driver.md)

ACPI デバイス関数ドライバーをサポートするシステム提供のサポートルーチンの詳細については、「 [Acpi 操作領域ハンドラーリファレンス](https://docs.microsoft.com/windows-hardware/drivers/ddi/_acpi/index)」を参照してください。

ACPI デバイスと名前空間の詳細については、「 [Advanced Configuration And Power Interface (acpi) の仕様](https://uefi.org/specifications)」を参照してください。
