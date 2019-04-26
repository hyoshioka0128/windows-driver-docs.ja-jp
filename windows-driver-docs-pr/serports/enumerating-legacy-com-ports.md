---
title: レガシ COM ポートを列挙する
description: レガシ COM ポートを列挙する
ms.assetid: 36a73153-0e3e-4b41-9b3d-08b29b5220fe
keywords:
- シリアル ドライバー WDK では、COM ポート
- COM ポートの WDK シリアル デバイス
- COM ポート、シリアル デバイス WDK
- COM ポートの WDK シリアル デバイスを列挙します。
- 従来の COM ポートの WDK シリアル デバイス
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 355d59ab334d70715131ab2605ae39b2b46def07
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63341293"
---
# <a name="enumerating-legacy-com-ports"></a>レガシ COM ポートを列挙する





シリアル関数ドライバーは、レガシ現在を列挙します。 [COM ポート](configuration-of-com-ports.md)レジストリで指定されています。 シリアルを列挙するほとんどの COM ポートは、マイクロ コント ローラーがないマルチポートのボード上の従来のデバイスを使用します。 この列挙関数がシリアルから削除され、将来のリリースのセットアップの一部として含まれていることに注意してください。

シリアルでは、次の手順を実行します。

1.  ドライバー サービスのレジストリ キーのサブキーで識別される COM ポートを確認します **.\\サービス\\シリアル\\パラメーター**\\&lt;*デバイス サブキー&gt;します。*

    シリアル デバイスの各サブキーで説明されているレジストリ情報を取得[従来の COM ポートのレジストリ設定](registry-settings-for-a-legacy-com-port.md)します。

2.  COM ポートのレガシ デバイスを確認します。 場合、 **PnPDeviceID**エントリの値が null、デバイスが従来のデバイス。 シリアルでは、残りの手順のみが COM ポートがレガシ デバイスの場合。 (場合**PnPDeviceID**が null でない場合、ポートは、バス ドライバーで列挙されているプラグ アンド プレイ デバイス)。

3.  COM ポートがレガシ デバイスの場合は、シリアルがかどうか、以前に検出されたことを決定します。

    COM ポートを使用するシリアル**LegacyDiscovered**エントリの値 (REG\_DWORD)。 場合**LegacyDiscovered**が 0 以外の場合、シリアル以前検出ポートと、もう一度列挙をスキップします。 プラグ アンド プレイ マネージャーは、追加し、従来のポートを開始します。

    場合**LegacyDiscovered** 0 の場合は、シリアル以前が検出されませんでした、ポートとプラグ アンド プレイ manager へのレポート、COM ポート。 プラグ アンド プレイ マネージャーは、PDO を返し、そのデバイス ツリー内の COM ポートのエントリを作成します。

4.  各検出された従来の COM ポートの FDO を作成し、デバイス スタックにアタッチします。

5.  従来の COM ポートのプラグ アンド プレイのレジストリ キーの下の COM ポートの情報を設定します。

    シリアルでは、従来の COM ポートをレジストリから読み取られた情報のサブセットを使用します。 詳細については、次を参照してください。[プラグ アンド プレイ シリアル デバイス用のレジストリ設定](registry-settings-for-a-plug-and-play-serial-device.md)します。

6.  従来の COM ポートを開始します。

 

 




