---
title: テレビ コネクタおよびコピー防止ハードウェアの設定
description: テレビ コネクタおよびコピー防止ハードウェアの設定
ms.assetid: 2de45c31-6a44-4a57-84b9-3cb21c905f4b
keywords:
- テレビ コネクタ WDK ビデオのミニポート
- 保護設定の WDK ビデオ ミニポートをコピーします。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d6a28489f700f13d9fb6aef336d8324fc30a9dcc
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67365526"
---
# <a name="setting-tv-connector-and-copy-protection-hardware"></a>テレビ コネクタおよびコピー防止ハードウェアの設定


## <span id="ddk_setting_tv_connector_and_copy_protection_hardware_gg"></span><span id="DDK_SETTING_TV_CONNECTOR_AND_COPY_PROTECTION_HARDWARE_GG"></span>


設定のミニポート ドライバーでいずれかのビットを**dwFlags**のメンバー [ **VIDEOPARAMETERS** ](https://docs.microsoft.com/windows/desktop/api/tvout/ns-tvout-_videoparameters) VP の\_コマンド\_GET、ミニポート ドライバーできますVP のセットを実行\_コマンド\_を設定します。 呼び出し元の責任をミニポート ドライバーには、担当副社長でサポートが示される機能だけを設定するミニポート ドライバーを呼び出す\_コマンド\_を取得します。 ミニポート ドライバーは、担当副社長に応答する必要があります\_コマンド\_設定で、対応するビットを設定するには、各 VIDEOPARAMETERS フィールドの値を持つハードウェアを設定して**dwFlags**します。 次に、例を示します。

-   ミニポート ドライバーの設定、担当副社長場合\_フラグ\_テレビ\_モード ビットを担当副社長に\_コマンド\_取得、ミニポート ドライバーがで指定された値にテレビ モードを変更する必要があります**寸法**と担当副社長\_フラグ\_テレビ\_VP のモードが設定されている\_コマンド\_を設定します。

-   ミニポート ドライバー、担当副社長を設定する場合は\_フラグ\_テレビ\_標準ビット VP\_コマンド\_取得、ミニポート ドライバーは、テレビを変更する必要がありますし、標準で指定された値に**dwTVStandard**と担当副社長\_フラグ\_テレビ\_VP の標準が設定されて\_コマンド\_を設定します。

-   ミニポート ドライバー、担当副社長を設定する場合は\_フラグ\_ビット VP にコントラスト\_コマンド\_取得、ミニポート ドライバーがで指定された値にコントラストを設定する必要があります**dwContrast**と担当副社長\_フラグ\_コントラストが設定されて、担当副社長\_コマンド\_を設定します。

対応するビットが設定されていない場合、未定義のデータを含む VIDEOPARAMETERS フィールド**dwFlags**します。

 

 





