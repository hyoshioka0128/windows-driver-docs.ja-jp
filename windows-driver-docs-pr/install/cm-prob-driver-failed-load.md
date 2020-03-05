---
title: CM_PROB_DRIVER_FAILED_LOAD
description: CM_PROB_DRIVER_FAILED_LOAD
ms.assetid: 84d88db9-338b-4318-ba05-696521c96dd6
keywords:
- CM_PROB_DRIVER_FAILED_LOAD
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 07297f6ce47c7f3580420bf7cd2bdc7c749cf8f2
ms.sourcegitcommit: 6f165a03303b7e4950b37d4b992f0f481b14f3ca
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/04/2020
ms.locfileid: "78279583"
---
# <a name="code-39---cm_prob_driver_failed_load"></a>コード 39-CM_PROB_DRIVER_FAILED_LOAD

このデバイスマネージャーエラーメッセージは、ドライバーを読み込むことができなかったことを示します。

## <a name="error-code"></a>エラー コード

39

### <a name="display-message"></a>メッセージの表示

"このハードウェアのデバイスドライバーを読み込むことができません。 ドライバーが破損しているか、見つからない可能性があります。 (コード 39) "

### <a name="recommended-resolution"></a>推奨される解決策

新しいドライバを再インストールまたは取得します。

このエラーの理由は次のとおりです。

- 存在しないドライバーファイル、破損しているバイナリファイル、ファイル i/o の問題、または読み込むことができなかった別のバイナリ内のエントリポイントを参照するドライバー。

- ドライバーは、[カーネルモードのコード署名ポリシー](kernel-mode-code-signing-policy--windows-vista-and-later-.md)に準拠していません。

