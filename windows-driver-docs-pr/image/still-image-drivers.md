---
title: 静止画像ドライバー
description: 静止画像ドライバー
ms.assetid: e207f76e-ff35-4a0d-a4bf-744931055eb8
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0792f031ff8962d849cac0c0d960796db67e2b08
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63364352"
---
# <a name="still-image-drivers"></a>静止画像ドライバー





Microsoft Windows Driver Kit (WDK) には、Windows Image Acquisition (WIA) と呼ばれるアーキテクチャが含まれています。 WIA が静止画像を Microsoft のアーキテクチャ (Microsoft STI) の基盤に構築された、WIA を STI に簡単に構築されたドライバーを移行するためです。

このセクションでは、Microsoft STI に開発された従来のドライバーに対して提供されます。 これには、カメラが静止画像フラット ベッド スキャナーやデジタル Microsoft STI で定義され、このような静止画像ハードウェアのベンダーに利用可能なの COM インターフェイスについて説明します。 このセクションで説明されている COM インターフェイスは、によって呼び出されます。 または、次のベンダーから提供されたソフトウェアで定義されています。

-   TWAIN API は、特定の静止画像デバイスをサポートできるように必要とされる TWAIN データ ソースなどのイメージの取得 API ソフトウェアのデバイス固有のコンポーネント。

-   ユーザー モード静止画像ミニドライバー、イメージの購入ソフトウェアから下位レベルのデバイスとバス ドライバーへの通信パスを提供します。

セクションには、次のセクションが含まれています。

[Microsoft STI と Microsoft WIA の概要](overview-of-microsoft-sti-and-microsoft-wia.md)

[Microsoft STI の概要](introduction-to-microsoft-sti.md)

[Microsoft STI コンポーネント](microsoft-sti-components.md)

[COM インターフェイスを静止画像します。](still-image-com-interfaces.md)

[プッシュ モデル対応のアプリケーションを作成します。](creating-push-model-aware-applications.md)

[イメージの取得 Api 用のデバイス固有のコンポーネントの作成](creating-device-specific-components-for-image-acquisition-apis.md)

[ユーザー モードの静止画像ミニドライバーを作成します。](creating-a-user-mode-still-image-minidriver.md)

[インストールと構成もイメージのコンポーネント](installing-and-configuring-still-image-components.md)

[開始と停止、静止イメージ サービス](starting-and-stopping-the-still-image-service.md)

[デバッグ イメージのコンポーネントではまだ](debugging-still-image-components.md)

 

 




