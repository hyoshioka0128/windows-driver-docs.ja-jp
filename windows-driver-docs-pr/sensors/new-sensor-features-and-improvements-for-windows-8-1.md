---
title: センサーの新機能と Windows 8.1 の機能強化
description: このトピックでは、新機能と WindowsWindows 8.1 でのセンサーの機能強化をまとめたものです。
ms.assetid: F52BC6D1-DF67-4DE7-BEEC-D18C2A90B4CF
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7ec1985eaaeca713d1ea898fc2c8ebcef74a47cc
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63330106"
---
# <a name="new-sensor-features-and-improvements-for-windows-81"></a>センサーの新機能と Windows 8.1 の機能強化


このトピックでは、新機能と WindowsWindows 8.1 でのセンサーの機能強化をまとめたものです。

## <a name="support-for-hid-devices"></a>HID デバイスのサポート


Windows 8.1 には、HID トランスポート上で実行されるすべてのセンサー用インボックス サポートが含まれています。 このサポートは、HID クラス ドライバーによって提供されます。

クラス ドライバーは、次の一覧で、11 個のセンサーをサポートします。

-   加速度計 3D
-   アンビエント ライト
-   大気温度
-   大気圧
-   コンパス 3D
-   デバイスの向き
-   3D のジャイロスコープなどがあります。
-   湿度
-   傾斜計 3D
-   プレゼンス
-   近接通信

これらの 11 個のセンサーだけでなく HID クラス ドライバーは、デバイス ベンダーは、リストにない任意のセンサーをサポートするために使用できるカスタム クラスをサポートします。

## <a name="testing-sensor-functionality-with-the-sensor-diagnostic-tool"></a>センサー診断ツールを使用したセンサー機能をテストします。


センサー ドライバー、ファームウェア、ハードウェアをテストするため、センサー診断ツールを使用することができます。 このツールについては、「[センサー診断ツールは、](the-sensor-diagnostic-tool.md)トピック。

## <a name="sensor-driver-logic"></a>センサー ドライバー ロジック


新しいプログラミング ガイドには、センサー デバイス ドライバーのドライバーのロジックが記述されたセクションが含まれています。 このロジックはカバーする擬似コードとして表示されます: ドライバーの初期化、ドライバー インターフェイス、ドライバーの更新プログラム、デバイスの更新プログラム、およびドライバーの内部メソッド。 この新しいセクションの先頭で見つかります、[センサー ドライバー ロジック](driver-logic--pseudo-code-.md)トピック。

## <a name="sensors-geolocation-driver-sample"></a>センサー地理位置情報ドライバー サンプル


地理的位置情報ドライバーのサンプルでは、グローバル配置 System (GPS) デバイスをエミュレートする最小限の UMDF ドライバーを示します。 このサンプル ドライバーは、新しいで詳しく説明[プログラミング ガイド](programming-guide.md)します。

地理的位置情報ドライバーのサンプルには、ラジオの管理 API のサポートを追加で示すコードも含まれています。 「、[ラジオの管理をサポートしている](https://msdn.microsoft.com/library/windows/hardware/jj200337)トピック。

## <a name="related-topics"></a>関連トピック
[プログラミング ガイド](programming-guide.md)  
[センサー ドライバー ロジック](driver-logic--pseudo-code-.md)  
[センサー診断ツール](the-sensor-diagnostic-tool.md)  



