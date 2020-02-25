---
title: CM_PROB_DRIVER_FAILED_LOAD
description: CM_PROB_DRIVER_FAILED_LOAD
ms.assetid: 84d88db9-338b-4318-ba05-696521c96dd6
keywords:
- CM_PROB_DRIVER_FAILED_LOAD
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ef92d58401433ea83bf25600dd2cbb15e20156f1
ms.sourcegitcommit: aa7083b10b34a29a348f4950ced21a8a67a44a0f
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/22/2020
ms.locfileid: "77558414"
---
# <a name="cm_prob_driver_failed_load"></a>CM_PROB_DRIVER_FAILED_LOAD

この関数は、システムで使用するために予約されています。

ドライバーを読み込むことができませんでした。

## <a name="error-code"></a>エラー コード

39

### <a name="display-message"></a>メッセージの表示

"このハードウェアのデバイスドライバーを読み込むことができません。 ドライバーが破損しているか、見つからない可能性があります。 (コード 39) "

### <a name="recommended-resolution"></a>推奨される解決策

新しいドライバを再インストールまたは取得します。

このエラーの理由は次のとおりです。

- 存在しないドライバーファイル、破損しているバイナリファイル、ファイル i/o の問題、または読み込むことができなかった別のバイナリ内のエントリポイントを参照するドライバー。

- ドライバーは、[カーネルモードのコード署名ポリシー](kernel-mode-code-signing-policy--windows-vista-and-later-.md)に準拠していません。

