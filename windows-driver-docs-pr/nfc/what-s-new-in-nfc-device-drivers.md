---
title: NFC デバイス ドライバーの新機能
description: このトピックでは、Windows 10 での NFC デバイスドライバーの新機能と機能強化について説明します。
ms.assetid: 07E0E7F4-9D2B-423F-925C-D6923D8D9A4A
keywords:
- NFC
- 近距離無線通信
- proximity
- 近距離近接通信
- NFP
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 978f98b4bda778ba6aab4950f654ba243a61e1c8
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72829029"
---
# <a name="whats-new-for-nfc-device-drivers-in-windows-10"></a>Windows 10 での NFC デバイスドライバーの新機能


このトピックでは、Windows 10 での NFC デバイスドライバーの新機能と機能強化について説明します。

* NFC デバイスドライバーモデルは、ユニバーサル NFC デバイスドライバーモデルを作成するために、デスクトップデバイスとモバイルデバイスの両方に収束されています。 ハードウェアパートナーは、すべての Windows デバイスプラットフォームで実行できる1つのドライバーを作成できるようになりました。

* NFC クラス拡張 (CX) は、Windows で定義されているデバイスドライバーインターフェイスを実装して、NFC コントローラー、セキュリティで保護された要素、およびリモートの RF エンドポイントと対話します。

* NFC の機内モードの管理を行うために、インボックス NFC ラジオマネージャーが追加されました。 IHV が提供した NFC ラジオマネージャーを NFC ドライバーでパッケージ化しないでください (以前のバージョンの Windows で行ったように)。 Windows 10 NFC ラジオマネージャーと共に IHV が提供する NFC ラジオマネージャーをインストールすると、これらのソフトウェアコンポーネント間で競合が発生します。

 
## <a name="related-topics"></a>関連トピック
 [NFC デバイス ドライバー インターフェイス (DDI) リファレンス](https://docs.microsoft.com/windows-hardware/drivers/ddi/index)  
 
