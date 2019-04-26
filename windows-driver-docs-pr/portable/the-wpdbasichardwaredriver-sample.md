---
Description: WpdBasicHardwareDriver サンプル
title: WpdBasicHardwareDriver サンプル
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2d01f448d5fd25800c1c37c15eab1f17f3c976f3
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63340915"
---
# <a name="the-wpdbasichardwaredriver-sample"></a>WpdBasicHardwareDriver サンプル


WpdBasicHardwareDriver は、9 つのデバイスをサポートする WPD ドライバーです。 これらのデバイスは、その簡素性のために選択されました。 このわかりやすくするためには、ハードウェアの複雑さで行き詰まることがなくポータブル デバイスに共通するタスクに重点をサンプルが許可されています。

このサンプル ドライバーは、Windows Driver Kit (WDK) で含まれている WpdHelloWorldDriver に基づいています。 「The WPD インフラストラクチャをサポートする」セクションでは、このドライバーは、基本的なハードウェア デバイスと通信できるように、WpdHelloWorldDriver ソースに加えられた変更を表示します。 ドキュメントのこのセクションのトピックを操作する前に、WpdHelloWorldDriver を理解します。

Windows 8 とセンサーを統合するドライバーを開発する場合、センサー API とドライバー モデル (なく WPD) を使用します。 Windows Vista または Windows XP とセンサーを統合するドライバーを開発する場合、WPD は実用的なソリューションを提供します。

WpdBasicHardwareDriver でサポートされているセンサーは、次の表で説明します。

| センサー                                         | 説明                                         |
|------------------------------------------------|-----------------------------------------------------|
| Memsic 2125 の加速度計                      | X 軸と y 軸に沿って 2 g +/-感覚です。          |
| Sensiron 温度と湿度センサー       | 温度と相対湿度を検出します。           |
| Flexiforce センサー                              | 0-25 lbs からの負荷を意味します。                      |
| PING Ultrasonic センサー                         | 2 ~ 300 cm からの距離を検出します。                     |
| パッシブ赤外線 (PIR) センサー                  | モーションを意味します。                                      |
| 日立 HM55B Compass                          | 磁気関係の検出 (0 ~ 360 度)。            |
| 日立 H48C トライ軸加速度計            | X 軸、y 軸および z 軸に沿って 3 g +/-感覚です。 |
| Piezo フィルム振動センサー QTI (光) センサー | 振動を検出します。                                   |
| QTI (光) センサー                             | 感覚はライトの強度です。                             |

 

これら 9 つのセンサーが販売、[視差 Corporation](https://go.microsoft.com/fwlink/p/?linkid=154730) Rocklin、カリフォルニア州にします。 これらで購入できる、個別にまたは組み合わせてセンサー サンプル キット。

で、WpdBasicHardwareDriver をこれらのセンサーを使用するには、センサーをプログラミング可能なマイクロ コント ローラー (視差 BS2)、(BASIC スタンプを視差宿題ボード) のようなテストの掲示板、RS232 ケーブルの場合、およびその他の部分を購入する必要があります。 すべてのハードウェアが視差から使用可能なと、Web サイトで注文することができます。

回路の設計は、parallax、センサー データ シートで提供されるサンプルの回線に基づいています。 視差 BS2 プログラミング可能なマイクロ コント ローラーと各センサーの統合には、これらの回線が設計されています。

Src マイクロ コント ローラーのファームウェアを 9 つの回線のそれぞれが含まれている\\wpd\\WpdBasicHardwareDriver\\ファームウェア サブディレクトリ Windows Driver Kit (WDK) にします。

 

 




