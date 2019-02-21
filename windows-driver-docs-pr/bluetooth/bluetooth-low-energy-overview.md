---
title: Bluetooth 低エネルギーの概要
description: このセクションでは、Windows 8 で導入された Bluetooth 低エネルギーの概要を示します
ms.assetid: 8783E31B-99A3-40EB-8A67-647AFAB7D4D3
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 50458e93c187ba76c38986045ab43282dbe8c032
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56548654"
---
# <a name="bluetooth-low-energy-overview"></a>Bluetooth 低エネルギーの概要


Windows 8 には、Bluetooth 低エネルギー テクノロジのサポートが導入されています。

Bluetooth 低エネルギーでは、Bluetooth の基本的なレートと同じ周波数領域を共有する新しい物理レイヤーについて説明します。 このテクノロジで開発されたプロファイルは、汎用の属性のプロファイル (または GATT) に編成されます。

各プロファイルは、ユース ケースやシナリオを作成する 1 つまたは複数のサービスの使用を定義します。 準拠しているサービスの実装が Bluetooth 特別利益団体で定義されている確立されたスキーマに準拠した方法で整理の特徴から構築された[developer web サイト](http://developer.bluetooth.org/gatt/services/Pages/ServicesHome.aspx)します。

次の図は、オブジェクトが、一般的な GATT サービス内で構造化方法を示しています。

![bluetooth 低エネルギー gatt サービスの宣言](images/bthleservicedeclaration.png)

Bluetooth 低エネルギー デバイスは、Windows 8 コンピューターと組み合わせると、デバイス、システムの一部になります、Windows は、デバイスと、デバイスによって報告された、プライマリ サービスの両方を表すデバイス オブジェクトを提供します。

![windows 8 の bluetooth 低エネルギー実装のデバイス オブジェクトの構造](images/bthlewin8supt.png)

各デバイスとそのプライマリ サービスが Windows のデバイス オブジェクトとして表されると、これらのデバイス オブジェクトは、クエリを実行できるしを使用して管理、[デバイスのインストール機能](https://msdn.microsoft.com/library/windows/hardware/ff549791)など[ **SetupDiEnumDeviceInfo**](https://msdn.microsoft.com/library/windows/hardware/ff551010)、および[ **SetupDiGetDeviceProperty**](https://msdn.microsoft.com/library/windows/hardware/ff551963)します。

だけでなく、標準[Bluetooth プロファイル ドライバー関数](https://msdn.microsoft.com/library/windows/hardware/hh450828)、新しい Windows 8 が導入されています[Bluetooth 低エネルギー関数](https://msdn.microsoft.com/library/windows/hardware/hh450825)Bluetooth GATT クライアント アプリケーションの開発のことができます。

これらの関数は、サービスとそれらのオブジェクト (サービス、特性の記述子を含む) の列挙体では、だけでなく読み取りおよび書き込み機能。

 

 





