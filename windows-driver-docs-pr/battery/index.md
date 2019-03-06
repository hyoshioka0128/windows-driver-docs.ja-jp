---
title: バッテリ デバイス設計ガイド
description: バッテリ デバイス設計ガイド
ms.assetid: d8eecfcb-6c06-40d1-8c78-b8c88eb890f2
ms.date: 04/20/2017
ms.topic: article
ms.prod: windows-hardware
ms.technology: windows-devices
---

# <a name="battery-devices-design-guide"></a>バッテリ デバイス設計ガイド


## <span id="ddk_design_guide_battery_devices_dg"></span><span id="DDK_DESIGN_GUIDE_BATTERY_DEVICES_DG"></span>


通常、バッテリには 1 組のドライバーがあります。Microsoft が提供する汎用的なバッテリ クラス ドライバーと、そのバッテリの種類専用に作成されたミニクラス ドライバーです。

クラス ドライバーはシステム内のバッテリの全体的な機能を定義し、電源マネージャーとやり取りします。

この設計ガイドでは、[バッテリ ミニクラス ドライバーの作成](writing-battery-miniclass-drivers.md)に焦点を当てます。

さらに、このセクションでは、以前のバージョンの Windows で使用されていた [UPS ミニドライバーの作成](writing-ups-minidrivers.md)についても説明します。

 

 




