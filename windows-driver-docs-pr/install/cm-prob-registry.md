---
title: CM_PROB_REGISTRY
description: CM_PROB_REGISTRY
ms.assetid: 162586c4-f67f-40e8-bbbb-2b5c574732f4
keywords:
- CM_PROB_REGISTRY
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 137aa07742d31511d872312a7d4b2f78f5e31194
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56558329"
---
# <a name="cmprobregistry"></a>CM_PROB_REGISTRY

この関数は、システムの使用に予約されています。

レジストリの問題が検出されました。

## <a name="error-code"></a>エラー コード

19

### <a name="display-message"></a>メッセージを表示します。

"Windows を開始できませんこのハードウェア デバイス (レジストリ) 内には、その構成情報が不完全または破損しているためです。 (コード 19)"

### <a name="recommended-resolution"></a>推奨される解決方法

このエラーは、複数のデバイスの 1 つのサービスが定義されている、サービス キーを開く障害が発生したまたはドライバー名は、サービスのキーから取得できない場合に発生します。

いずれかをアンインストールして、ドライバの再インストールやレジストリの成功した最新の構成に、システムをロールバックしています。

デバイス ドライバを再インストールをアンインストールしては、これらの手順に従います。

1. [デバイス マネージャーを開く](using-device-manager.md)します。

2. デバイス マネージャー ウィンドウでデバイスを表すアイコンを右クリックします。

3. 表示されるメニューで、**アンインストール**デバイス ドライバーをアンインストールします。

4. クリックして**アクション**デバイス マネージャーのメニュー バーにします。

5. **アクション** メニューのをクリックして**ハードウェア変更のスキャン**デバイス ドライバーを再インストールします。

レジストリの成功した最新の構成に、システムをロールバック、セーフ モードでコンピューターを再起動し、前回正常起動時の構成オプションを選択します。
