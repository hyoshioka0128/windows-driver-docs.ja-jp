---
title: Bluetooth 低エネルギーの概要
description: このセクションでは、Windows 8 で導入された Bluetooth 低エネルギーの概要を示します
ms.assetid: 8783E31B-99A3-40EB-8A67-647AFAB7D4D3
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 407eae063303e1cd8725bd55d4ce07889b32970d
ms.sourcegitcommit: f663c383886d87ea762e419963ff427500cc5042
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67391562"
---
# <a name="bluetooth-low-energy-overview"></a>Bluetooth 低エネルギーの概要


Windows 8 には、Bluetooth 低エネルギー テクノロジのサポートが導入されています。

Bluetooth 低エネルギーでは、Bluetooth の基本的なレートと同じ周波数領域を共有する新しい物理レイヤーについて説明します。 このテクノロジで開発されたプロファイルは、汎用の属性のプロファイル (または GATT) に編成されます。

各プロファイルは、ユース ケースやシナリオを作成する 1 つまたは複数のサービスの使用を定義します。 準拠しているサービスの実装が Bluetooth 特別利益団体で定義されている確立されたスキーマに準拠した方法で整理の特徴から構築された[developer web サイト](https://www.bluetooth.com/specifications/gatt/services/)します。

次の図は、オブジェクトが、一般的な GATT サービス内で構造化方法を示しています。

![bluetooth 低エネルギー gatt サービスの宣言](images/bthleservicedeclaration.png)

Bluetooth 低エネルギー デバイスは、Windows 8 コンピューターと組み合わせると、デバイス、システムの一部になります、Windows は、デバイスと、デバイスによって報告された、プライマリ サービスの両方を表すデバイス オブジェクトを提供します。

![windows 8 の bluetooth 低エネルギー実装のデバイス オブジェクトの構造](images/bthlewin8supt.png)

各デバイスとそのプライマリ サービスが Windows のデバイス オブジェクトとして表されると、これらのデバイス オブジェクトは、クエリを実行できるしを使用して管理、[デバイスのインストール機能](https://docs.microsoft.com/previous-versions/ff549791(v=vs.85))など[ **SetupDiEnumDeviceInfo**](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdienumdeviceinfo)、および[ **SetupDiGetDeviceProperty**](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdigetdevicepropertyw)します。

だけでなく、標準[Bluetooth プロファイル ドライバー関数](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/index)、新しい Windows 8 が導入されています[Bluetooth 低エネルギー関数](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/index)Bluetooth GATT クライアント アプリケーションの開発のことができます。

これらの関数は、サービスとそれらのオブジェクト (サービス、特性の記述子を含む) の列挙体では、だけでなく読み取りおよび書き込み機能。

 

 





