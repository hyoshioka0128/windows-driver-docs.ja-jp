---
title: CM_PROB_PARTIAL_LOG_CONF
description: CM_PROB_PARTIAL_LOG_CONF
ms.assetid: 1e8b10e8-c2c6-4a71-9af5-575206098148
keywords:
- CM_PROB_PARTIAL_LOG_CONF
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: a78ae518332b258b2ca143bd29ab9e56e0ff4fd2
ms.sourcegitcommit: 6f165a03303b7e4950b37d4b992f0f481b14f3ca
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/04/2020
ms.locfileid: "78279505"
---
# <a name="code-16---cm_prob_partial_log_conf"></a>コード 16-CM_PROB_PARTIAL_LOG_CONF

このデバイスマネージャーエラーメッセージは、デバイスが部分的に構成されていることを示します。

## <a name="error-code"></a>エラー コード

16

### <a name="display-message"></a>メッセージの表示

"このデバイスで使用されているすべてのリソースを識別できません。 (コード 16) "

"このデバイスの追加リソースを指定するには、[リソース] タブをクリックし、不足している設定を入力します。 使用する設定を確認するには、ハードウェアのドキュメントを参照してください。 "

### <a name="recommended-resolution"></a>推奨される解決策

デバイスに必要なリソースを手動で構成します。

デバイスリソースを構成するには、次の手順を実行します。

1. [デバイスマネージャーを開き](using-device-manager.md)ます。

2. [デバイスマネージャー] ウィンドウで、デバイスを表すアイコンをダブルクリックします。

3. 表示されるデバイスプロパティシートで、 **[リソース]** タブをクリックします。デバイスリソースは、 **[リソース]** ページの **[リソース設定]** の一覧に表示されます。

4. **リソース設定**リストのリソースの横に疑問符が表示されている場合は、そのリソースを選択してデバイスに割り当てます。

5. リソースを変更できない場合は、 **[設定の変更]** をクリックします。 **[設定の変更]** が使用できない場合は、 **[自動設定を使用]** する チェックボックスをオフにして使用できるようにします。

デバイスがプラグアンドプレイデバイスでない場合は、デバイスのドキュメントを参照して、デバイスのリソースを構成する方法の詳細を確認してください。
