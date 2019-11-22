---
title: Bluetooth 低エネルギーの概要
description: このセクションでは、Windows 8 で導入された Bluetooth 低エネルギーの概要について説明します。
ms.assetid: 8783E31B-99A3-40EB-8A67-647AFAB7D4D3
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: f53360e52b078b6383f0608e3a584efd81d785aa
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72833885"
---
# <a name="bluetooth-low-energy-overview"></a>Bluetooth 低エネルギーの概要


Windows 8 では、Bluetooth 低エネルギーテクノロジのサポートが導入されています。

Bluetooth 低エネルギーには、Bluetooth 基本レートと同じ頻度の領域を共有する新しい物理レイヤーが導入されています。 このテクノロジで開発されたプロファイルは、汎用属性プロファイル (または GATT) に編成されます。

各プロファイルは、1つまたは複数のサービスを使用してユースケースまたはシナリオを作成することを定義します。 準拠サービスの実装は、Bluetooth の特別な関心事グループ[開発者向け web サイト](https://www.bluetooth.com/specifications/gatt/services/)で定義されたスキーマに準拠した方法で編成された特性から構築されます。

次の図は、一般的な GATT サービス内でオブジェクトがどのように構成されているかを示しています。

![bluetooth low energy gatt サービスの宣言](images/bthleservicedeclaration.png)

Bluetooth 低エネルギーデバイスと Windows 8 コンピューターがペアリングされている場合、デバイスはシステムの一部になり、Windows はデバイスオブジェクトを提供して、デバイスによって報告されたデバイスとプライマリサービスの両方を表します。

![windows 8 bluetooth 低エネルギー実装のデバイスオブジェクト構造](images/bthlewin8supt.png)

各デバイスとそのプライマリサービスは Windows のデバイスオブジェクトとして表されます。これらのデバイスオブジェクトは、 [**SetupDiEnumDeviceInfo**](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdienumdeviceinfo)や[**Setupdigetdeviceproperty**](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdigetdevicepropertyw)などの[デバイスのインストール機能](https://docs.microsoft.com/previous-versions/ff549791(v=vs.85))を使用してクエリおよび管理できます。

Windows 8 では、標準の[Bluetooth プロファイルドライバー機能](https://docs.microsoft.com/windows-hardware/drivers/ddi/index)に加えて、bluetooth GATT クライアントアプリケーションの開発を可能にする新しい[bluetooth 低エネルギー機能](https://docs.microsoft.com/windows-hardware/drivers/ddi/index)が導入されています。

これらの関数を使用すると、サービスとそのオブジェクト (サービス、特性、およびその記述子を含む) の列挙、および読み取りおよび書き込み機能を使用できます。

 

 





