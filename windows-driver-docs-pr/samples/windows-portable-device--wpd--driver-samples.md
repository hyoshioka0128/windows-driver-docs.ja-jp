---
title: Windows ポータブル デバイス (WPD) ドライバーのサンプル
description: このディレクトリにドライバーのサンプルでは、デバイスのカスタム WPD ドライバーを記述するための開始点を提供します。
ms.assetid: 5EB5B820-A29A-4A93-BBB9-6F4CDF101E3B
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6c36c16098cdc7d8b85252e2032ff034648d4561
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63342844"
---
# <a name="windows-portable-device-wpd-driver-samples"></a>Windows ポータブル デバイス (WPD) ドライバーのサンプル


このディレクトリにドライバーのサンプルでは、デバイスのカスタム WPD ドライバーを記述するための開始点を提供します。

## <a name="windows-portable-device-wpd"></a>Windows ポータブル デバイス (WPD)


| サンプル名                               | ソリューション                                                                   | 説明                                                                                                                                                                                                                                                           |
|-------------------------------------------|----------------------------------------------------------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| WPD ハードウェアの基本的なサンプル ドライバー (UMDF 1) | [WpdBasicHardwareDriver](https://go.microsoft.com/fwlink/p/?LinkId=620318)  | 視差 BS2 プログラミング可能なマイクロ コント ローラーと統合される 9 つのセンサー デバイスをサポートしている WPD サンプル ドライバー。                                                                                                                                              |
| Hello World の例                       | [WpdHelloWorldDriver](https://go.microsoft.com/fwlink/p/?LinkId=618008)     | このサンプルのドライバーが 4 つのオブジェクトをサポートしています: デバイス オブジェクト、ストレージ オブジェクト、フォルダー オブジェクト、およびファイル オブジェクト。 各オブジェクトは、一連のプロパティをサポートします。                                                                                                            |
| 複数のトランスポート ドライバー                    | [WpdMultiTransportDriver](https://go.microsoft.com/fwlink/p/?LinkId=618009) | 複数のトランスポートをサポートするデバイスの WpdHelloWorldDriver を拡張する方法を示します。 トランスポートは、ポータブル デバイスがコンピューターと通信するプロトコルです。 トランスポートの例には、インターネット プロトコル (IP)、Bluetooth、USB などがあります。 |
| WPD サービス サンプル ドライバー                 | [WpdServiceSampleDriver](https://go.microsoft.com/fwlink/p/?LinkId=618010)  | 連絡先のデバイス サービスでシミュレートされたデバイスをサポートするように、WpdHelloWorldDriver サンプルを拡張する方法を示します。                                                                                                                                      |
| WUDF ドライバー                               | [WpdWudfSampleDriver](https://go.microsoft.com/fwlink/p/?LinkId=618011)     | WPD デバイス ドライバー インターフェイス (DDI) のほぼすべての側面を包括的な WPD サンプル ドライバーに示します。                                                                                                                                                        |

 

 

 




