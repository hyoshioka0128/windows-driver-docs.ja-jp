---
title: CM_PROB_DRIVER_FAILED_LOAD
description: CM_PROB_DRIVER_FAILED_LOAD
ms.assetid: 84d88db9-338b-4318-ba05-696521c96dd6
keywords:
- CM_PROB_DRIVER_FAILED_LOAD
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4475a6a03a90d34ed1a8af2fe862f42021bfebb3
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63391485"
---
# <a name="cmprobdriverfailedload"></a>CM_PROB_DRIVER_FAILED_LOAD

この関数は、システムの使用に予約されています。

ドライバーを読み込むことができませんでした。

## <a name="error-code"></a>エラー コード

39

### <a name="display-message"></a>メッセージを表示します。

"Windows は、このハードウェアのデバイス ドライバーを読み込むことができません。 ドライバーが破損しているか、不足している可能性があります。 (コード 39)"

### <a name="recommended-resolution"></a>推奨される解決方法

再インストールするか、新しいドライバーを入手します。

このエラーの原因として、次のとおりです。

- ドライバー ファイルが存在しないを破損しているバイナリ ファイル、ファイル I/O の問題、または読み込まれていない別のバイナリのエントリ ポイントを参照するドライバー。

- ドライバーは準拠していない[カーネル モード コードの署名ポリシー](kernel-mode-code-signing-policy--windows-vista-and-later-.md)します。
