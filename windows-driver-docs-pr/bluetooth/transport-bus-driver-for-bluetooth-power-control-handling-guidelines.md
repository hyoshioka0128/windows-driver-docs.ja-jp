---
title: Bluetooth 電源管理処理用トランスポート バス ドライバーのガイドライン
description: Ihv は、システムオンチップ (SoC) システムに統合されることが多い多機能コントローラーの Bluetooth 機能をサポートするために、トランスポートバスドライバーを実装する必要があります。
ms.assetid: 00792128-320E-45C1-9F58-343B72565CA7
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 52ce7ae24931875f18e3568ca169891ebffc0ed9
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72834531"
---
# <a name="transport-bus-driver-for-bluetooth-power-control-handling-guidelines"></a>Bluetooth 電源管理処理用トランスポート バス ドライバーのガイドライン


Ihv は、システムオンチップ (SoC) システムに統合されることが多い多機能コントローラーの Bluetooth 機能をサポートするために、トランスポートバスドライバーを実装する必要があります。

[Bluetooth シリアル HCI バスドライバー](https://go.microsoft.com/fwlink/p/?linkid=256088)のサンプルを使用すると、転送バスドライバーの開発を促進するのに役立ちます。 このサンプルでは、上位層からの IOCTL (IO 制御) 要求を処理する方法と、HCI パケットを下位層でシリアルコントローラードライバーに配信する方法を示します。 ただし、専用の IO トランスポート (WDK サンプルの場合は UART) を使用する以外の帯域外制御は、アイドル状態のコントロールとウェイクコントロールをサポートするためによく使用されます。このようなメカニズムは必須であり、電力消費を最適化するために使用されます。 このセクションとサブトピックの情報は、電源管理を処理するためのガイドラインとサンプルコードを提供することで、バスサンプルドライバーを補足します。

このセクションとサブトピックの情報は、次のものに適用されます。

-   Windows 8.1

Bluetooth は、短い範囲のワイヤレスラジオとして、多くの場合、システム上のシステム (SoC) システムに統合されている多機能コントローラー内で機能します。 Windows 7 以前のバージョンの Windows では、Bluetooth 用の受信トレイクラスドライバーが唯一のトランスポートオプションとして提供されていました。 Windows 8 では、 [Bluetooth 拡張可能なトランスポートの ioctl](https://docs.microsoft.com/windows-hardware/drivers/ddi/index)が導入されました。 USB トランスポートと拡張可能なトランスポートモデルは、引き続き Windows 8.1 でサポートされます。 拡張モデル DDI は Windows で変更されていません。システムインテグレーターは、たとえば、UART (Universal 非同期レシーバー/トランスミッタ) などの SoC プラットフォームに適したトランスポートを選択できる柔軟性を備えています。 さらに、単純で低電力のコントローラー (GPIOs など) を、電源管理を処理するための "sideband" メカニズムとして使用することもできます (たとえば、Bluetooth ラジオやスリープ/ウェイク信号として有効にするなど)。

このセクションとサブトピックの情報は、このようなバスドライバーによる電源管理処理のガイドラインとサンプルコードと、Bluetooth コアドライバーとの対話について説明しています。 これらのコントロールには、wake、idle、およびウェイクシグナの取り組まと disarming、およびデバイスの電源状態の変更が含まれます。 ドライバー開発者は、Bluetooth シリアル HCI バスドライバーのサンプルを採用して、代替 (非 USB) 転送で Bluetooth をサポートする開発作業を簡略化できます。

Bluetooth のサポートには異なるトランスポートが使用されていますが、bluetooth プロファイルドライバーでは、Bluetooth DDIs は変わりません。 これは、Bluetooth プロファイルのドライバーとアプリケーションは、実装されているトランスポートまたは電源管理の処理に依存しないことを意味します。

 

 





