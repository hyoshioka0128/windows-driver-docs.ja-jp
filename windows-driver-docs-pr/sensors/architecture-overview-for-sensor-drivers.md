---
title: センサー ドライバーのアーキテクチャの概要
description: センサー デバイス ドライバーが Windows ユーザー モード ドライバー フレームワーク (UMDF) を使用して実装されている COM オブジェクトです。
ms.assetid: 6d1b15ea-ba27-4bde-8000-d31f014ab47d
ms.date: 07/20/2018
ms.localizationpriority: medium
ms.openlocfilehash: 3617232bcb436851c4302320f2c41a5edd5e50b7
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56582152"
---
# <a name="architecture-overview-for-sensor-drivers"></a>センサー ドライバーのアーキテクチャの概要


センサー デバイス ドライバーは、Windows ユーザー モード ドライバー フレームワーク (UMDF) を使用して実装されている COM オブジェクトです。 センサー ドライバーは、ヘルパー オブジェクトとして、Windows ポータブル デバイス (WPD) インターフェイスおよびその他の型を使用します。 Windows Driver Kit のドキュメントでは、UMDF と WPD の両方が記載されています。 UMDF ドライバーの詳細については、次を参照してください。[ユーザー モード ドライバー フレームワーク](https://msdn.microsoft.com/library/windows/hardware/ff561365)します。 WPD 種類の詳細については、次を参照してください。[ポータブル デバイス](https://msdn.microsoft.com/library/windows/hardware/ff597901)します。

センサー ドライバーは、特殊な**クラスの拡張機能**オブジェクト。 センサー クラスの拡張機能であり、標準の COM オブジェクトは、センサー デバイス ドライバの I/O 要求を処理するための標準実装を提供します。 センサー ドライバーでは、ドライバーのプロセスでクラスの拡張機能オブジェクトを作成し、I/O 要求を転送し、クラスの拡張機能からイベントを受信するデバイス ドライバー インターフェイス (DDI) を使用します。 次の図は、センサー、ドライバー、およびセンサー クラスの拡張機能間の関係を示します。 (センサー ドライバーは、各センサー デバイス クラスの拡張機能の新しいインスタンスを作成します)。

![センサー クラスの拡張機能を使用する umdf ベースのセンサー ドライバー](images/sensordriver-cxt.jpg)

クラスの拡張オブジェクトの詳細については、次を参照してください。[センサー クラス拡張について](about-the-sensor-class-extension.md)します。

>[!IMPORTANT]
> センサー ドライバーでは、フリー スレッド化される必要があり、スレッド セーフです。










