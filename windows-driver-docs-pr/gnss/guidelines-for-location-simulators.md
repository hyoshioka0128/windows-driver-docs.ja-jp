---
title: シミュレーターの場所に関するガイダンス
description: このセクションには、場所シミュレーターのドライバーを実装するためのガイダンスが含まれています。
ms.assetid: 4AA6C3EE-0150-45A8-ACC2-D0267591D33D
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: e2a0ed8722790754db0a02e48cc3509ef9f0d774
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56529413"
---
# <a name="guidance-for-location-simulators"></a>シミュレーターの場所に関するガイダンス


Microsoft Visual Studio 2012 の提供、[位置特定シミュレーター](https://msdn.microsoft.com/library/windows/apps/hh441475.aspx#bkmk-set-the-simulated-geo-location-of-the-device)を作成する場所シミュレーター ドライバーと共にします。 このセクションには、場所シミュレーターのドライバーを実装するためのガイダンスが含まれています。 Visual Studio 2017 以降では、場所シミュレーターの機能が不要になった存在する、センサー ドライバーをシミュレートすることはできませんので注意してください。

## <a name="configure-the-simulator"></a>シミュレーターを構成します。


シミュレーターのドライバーを有効にするには、レジストリ キーを編集`HKLM\Software\Microsoft\Location`をシミュレーターには、ドライバーのセンサー ID に"SimulatorID"をという名前の文字列値を設定します。

## <a name="clear-data-on-simulator-exit"></a>シミュレーターの終了時にデータのクリア


シミュレーターのドライバーがいいえ に状態を変更する必要がありますシミュレータ アプリケーションが終了すると、\_データと送信の状態変更イベント。

## <a name="how-simulator-data-is-used"></a>シミュレーターのデータの使用方法


-   シミュレーター ドライバーからのデータは、位置特定シミュレーター用のエミュレーターのセッションでのみ使用されます。 シミュレーターのデータは、通常のアプリケーションでは使用されません。
-   場合は、シミュレーターのドライバーをシミュレーターで実行されているデータが含まれない、場所シミュレーターで他のソースからデータが使用されます。

## <a name="related-topics"></a>関連トピック
[シミュレーターで UWP アプリの実行](https://msdn.microsoft.com/library/windows/apps/hh441475.aspx)  
[デバイスのシミュレートされる地理的位置情報を設定します。](https://msdn.microsoft.com/library/windows/apps/hh441475.aspx#bkmk-set-the-simulated-geo-location-of-the-device)  



