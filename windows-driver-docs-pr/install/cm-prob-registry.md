---
title: CM_PROB_REGISTRY
description: CM_PROB_REGISTRY
ms.assetid: 162586c4-f67f-40e8-bbbb-2b5c574732f4
keywords:
- CM_PROB_REGISTRY
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d7a21238d980709b39dcf3d76b892f1532540b67
ms.sourcegitcommit: 6f165a03303b7e4950b37d4b992f0f481b14f3ca
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/04/2020
ms.locfileid: "78279491"
---
# <a name="code-19---cm_prob_registry"></a>コード 19-CM_PROB_REGISTRY

このデバイスマネージャーエラーメッセージは、レジストリの問題が検出されたことを示します。

## <a name="error-code"></a>エラー コード

19

### <a name="display-message"></a>メッセージの表示

"その構成情報 (レジストリ内) が不完全であるか破損しているため、Windows はこのハードウェアデバイスを起動できません。 (コード 19) "

### <a name="recommended-resolution"></a>推奨される解決策

このエラーは、デバイスに対して複数のサービスが定義されている場合、サービスキーを開くときにエラーが発生した場合、またはサービスキーからドライバー名を取得できない場合に発生する可能性があります。

ドライバーをアンインストールしてから再インストールするか、レジストリの最新の構成にシステムをロールバックしてみてください。

デバイスドライバをアンインストールして再インストールするには、次の手順を実行します。

1. [デバイスマネージャーを開き](using-device-manager.md)ます。

2. [デバイスマネージャー] ウィンドウで、デバイスを表すアイコンを右クリックします。

3. 表示されるメニューで、 **[アンインストール]** をクリックして、デバイスドライバーをアンインストールします。

4. デバイスマネージャーのメニューバーで **[アクション]** をクリックします。

5. **[操作]** メニューの **[ハードウェア変更のスキャン]** をクリックして、デバイスドライバーを再インストールします。

レジストリの最新の正常な構成にシステムをロールバックするには、コンピューターをセーフモードで再起動し、前回正常起動時の構成オプションを選択します。
