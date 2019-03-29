---
title: CM_PROB_PARTIAL_LOG_CONF
description: CM_PROB_PARTIAL_LOG_CONF
ms.assetid: 1e8b10e8-c2c6-4a71-9af5-575206098148
keywords:
- CM_PROB_PARTIAL_LOG_CONF
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 94d46655e164f54f415e4ee3fa87b3ac6ba03065
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56570969"
---
# <a name="cmprobpartiallogconf"></a>CM_PROB_PARTIAL_LOG_CONF

この関数は、システムの使用に予約されています。

デバイスの構成が部分的にのみです。

## <a name="error-code"></a>エラー コード

16

### <a name="display-message"></a>メッセージを表示します。

"Windows は、このデバイスを使用してすべてのリソースを識別できません。 (コードは 16)"

"このデバイスの他のリソースを指定するには、リソース タブをクリックし、不足している設定を入力します。 使用するには、どのような設定を確認する、ハードウェアのマニュアルを確認します。"

### <a name="recommended-resolution"></a>推奨される解決方法

デバイスに必要なリソースを手動で構成します。

デバイス リソースを構成するには、次の手順を実行します。

1. [デバイス マネージャーを開く](using-device-manager.md)します。

2. デバイス マネージャー ウィンドウでデバイスを表すアイコンをダブルクリックします。

3. 表示される、デバイスのプロパティ シートには、をクリックして、**リソース**タブ。デバイス リソースが一覧表示、**リソース設定**ボックスの一覧、**リソース**ページ。

4. 内のリソースの場合、**リソース設定**リストが横にある疑問符 () で、デバイスに割り当てるには、そのリソースを選択します。

5. リソースは変更できない場合はクリックして**設定の変更**します。 場合**設定の変更**が使用できないのクリアを試す、**自動設定を使用して**チェック ボックスを使用できるようにします。

デバイス、プラグ アンド プレイ デバイスではない場合は、詳細、デバイスのリソースを構成する方法については、デバイスのドキュメントで検索します。
