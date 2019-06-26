---
title: Bluetooth 電源管理処理用トランスポート バス ドライバーのガイドライン
description: Ihv は、多くの場合、チップ (SoC) システム上のシステムに統合されている多機能コント ローラーの Bluetooth 機能をサポートするためにトランスポート バス ドライバーを実装する必要があります。
ms.assetid: 00792128-320E-45C1-9F58-343B72565CA7
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 447c19151d1f2a61f23d29c42ab1ce6b3c4a9df8
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67353998"
---
# <a name="transport-bus-driver-for-bluetooth-power-control-handling-guidelines"></a>Bluetooth 電源管理処理用トランスポート バス ドライバーのガイドライン


Ihv は、多くの場合、チップ (SoC) システム上のシステムに統合されている多機能コント ローラーの Bluetooth 機能をサポートするためにトランスポート バス ドライバーを実装する必要があります。

[Bluetooth シリアル HCI バス ドライバー](https://go.microsoft.com/fwlink/p/?linkid=256088)サンプルは ihv 向けの開発を促進に役立つ、そのトランスポート バス ドライバー。 サンプルでは、上位層から IOCTL (入出力制御) 要求を処理する方法とその下位の層では、そのシリアル コント ローラー ドライバーに HCI パケットを配信する方法を示します。 ただし、以外、独自の IO トランスポート (UART WDK サンプルの場合) を使用して、帯域外のコントロールをアイドル状態のサポートし、復帰のコントロールを使用多くの場合、このようなメカニズムは必須であり電力消費量を最適化するために使用します。 については、このセクションと各サブトピックでは、電源コントロールを処理するためのガイドラインとサンプル コードを提供することで、バス ドライバーのサンプルを補足します。

このセクションと各サブトピックで情報に適用されます。

-   Windows 8.1

ワイヤレス、Bluetooth はチップ (SoC) システム上のシステムに統合されている多機能コント ローラー内の関数では多くの場合、短い範囲。 まで、Windows 7、Windows の以前のバージョンでは、唯一のトランスポート オプションとして、USB で Bluetooth のインボックス クラス ドライバーを提供します。 Windows 8 が導入された、 [Bluetooth 拡張可能なトランスポート Ioctl](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/index)します。 USB のトランスポートとトランスポートの拡張可能なモデルは、Windows 8.1 でサポートされなければならない続けます。 DDI 拡張モデルは、システム インテグレーター UART (Universal Asynchronous Receiver/transmitter) などの SoC のプラットフォーム用の適切なトランスポートを選択できる柔軟性を提供する Windows に変更されません。 GPIOs より簡単かつ低電力コント ローラーを使用して、電源管理を処理するための「側波帯」メカニズムとしてさらに、(Bluetooth 無線の有効化などとスリープ/ウェイク信号として)。

このセクションと各サブトピックでは、電源管理のようなバス ドライバーによって処理のためのガイドラインとサンプル コードを提供し、Bluetooth コア ドライバーとの相互作用について説明します。 コントロールには、: アイドル状態の機能、取り組まと disarming ウェイク、アイドル状態とスリープ解除がシグナル通知、およびデバイスの電源状態変更。 ドライバー開発者は、代替 (USB 以外) トランスポートを介して Bluetooth をサポートするために開発作業を簡略化する Bluetooth シリアル HCI バス ドライバーのサンプルを採用できます。

Bluetooth をサポートするために複数の異なるトランスポートを使用しているときに、Bluetooth Ddi が Bluetooth プロファイル ドライバーを同じになります。 これは、Bluetooth プロファイル ドライバーとアプリケーションは引き続き処理に実装されているトランスポートや電源管理に依存しないことを意味します。

 

 





