---
title: Microsoft Bluetooth テストプラットフォームでサポートされているハードウェア
description: Bluetooth テストプラットフォーム (BTP) でサポートされているハードウェア。
ms.assetid: a6beeecb-5967-4e08-bfe2-b8aae26861ad
ms.date: 2/14/2020
ms.localizationpriority: medium
ms.openlocfilehash: ed8c7f2740469a236330f4cff5bf090a0fff72d5
ms.sourcegitcommit: 7a7ce6070ed16673108cc64c33b3ddb894453cfb
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/29/2020
ms.locfileid: "87412533"
---
# <a name="bluetooth-testing-platform-supported-hardware"></a>Bluetooth テストプラットフォームでサポートされているハードウェア

Bluetooth テストプラットフォーム (BTP) では、Bluetooth テストを容易にするために特殊なハードウェアを利用しています。 Traduci board は、ホストデバイス (PC など) 上のソフトウェアに対して、sideband を介して外部無線との通信を容易にするために使用されます。

たとえば、LE ペアリングテストでは、周辺無線の電源をオンにし、特定の IO 機能を使用し、をとペアリングする前に接続可能/検出可能としてアドバタイズする必要があります。 周辺無線には、このような動作を可能にする適切に定義されたコマンドがあります。そのため、ホスト上の BTP ソフトウェアは、これらのコマンドを USB 経由で Traduci に送信し、さらに適切なラジオにルーティングします。 コマンドが正常に完了したら、そのホストペアを周辺無線に要求することによって、このテストを実行します。これにより、ペアリングを受け入れる準備ができました。

上記のシナリオでは、Traduci によっていくつかのことが簡単になります。無線に対して電源を供給し、電源を切ることができ、さまざまなコマンドをさまざまな無線にルーティングできます。また、この通信は、正しいプロトコルとボーレートを使用して仲介ます。

また、BTP テストには、Traduci に対する密接な依存関係がないことに注意する必要があります。 テストに他の外部ハードウェアが必要な場合は、そのシナリオをサポートするための拡張性を容易にするように、BTP が設計されています。

## <a name="traduci-board"></a>Traduci board
Traduci board は、 [Mcci](https://mcci.com/usb/dev-tools/model-2411/)によって提供されます。

![Traduci ボードの写真](images/Traduci_Overhead.jpg)

- 4 12-4 つのラジオを同時にサポートするためにポートをピン留めする
- 複数のラジオにデータを同時にルーティングできる
- 3 FPGAs はそれぞれポート1、2、3に接続されています。
- 統合オーディオコーデックを使用したオーディオテストをサポートする
- ポートに接続しているラジオのニーズに応じて、ピン留めされていない pin を高または低に簡単に静的に割り当てることができます。
- 現在、Traduci では、CTS と RTS を使用したハードウェアハンドシェイクはサポートされていません。

## <a name="supported-radios"></a>サポートされているラジオ

現時点では、公式にサポートされているのは RN42 (BR) 無線と Bluefruit (LE) ラジオのみです。 これらは両方とも、ペアリングテストと HID テストを実行できます。 これらのラジオの詳細については、「 [HID 対応の周辺機器無線](testing-BTP-hw-hid.md)reviwed」を参照してください。

オーディオテストは開発中です。 使用されるオーディオラジオの詳細については、「[オーディオ対応の周辺機器無線](testing-BTP-hw-audio.md)」を参照してください。