---
title: CM_PROB_NEED_CLASS_CONFIG
description: CM_PROB_NEED_CLASS_CONFIG
ms.assetid: e9604fcb-61c2-4b94-af53-c9278bc05dd0
keywords:
- CM_PROB_NEED_CLASS_CONFIG
ms.date: 02/28/2020
ms.localizationpriority: medium
ms.openlocfilehash: 28860c16bee71e2045790b780d2511060cbb63a0
ms.sourcegitcommit: f63852446e614c985a65f599cdfe788bdb0c6089
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/30/2020
ms.locfileid: "87425735"
---
# <a name="code-56---cm_prob_need_class_config"></a>Code 56 - CM_PROB_NEED_CLASS_CONFIG

このデバイスマネージャーエラーメッセージは、Windows がこのデバイスのクラス構成をまだセットアップしていることを示しています。


## <a name="error-code"></a>エラー コード

56

### <a name="display-message"></a>メッセージの表示

"Windows は、このデバイスのクラス構成をまだセットアップしています。 (コード 56) "


## <a name="for-driver-developers"></a>ドライバー開発者向け

この問題コードは、多くの場合、一時的なものです。

デバイスのセットアップクラスによっては、デバイスをドライバーパッケージと共にインストールした後に、デバイスを動作させるために追加のクラス構成操作が必要になります。  構成が完了すると、デバイスが再起動され、この問題コードを使用できなくなります。

たとえば、NET class デバイスは `*IfType` 、、 `UpperRange` 、およびその他のネットワーク固有の INF ディレクティブに基づいて追加の構成を受け取ります。

NET クラスデバイスでこの問題コードが引き続き発生する場合、ドライバー INF に無効なネットワーク固有の INF ディレクティブが含まれているか、システムのネットワーク状態が破損している可能性があり、リセットする必要があります。

これを行うには、設定アプリの [ネットワークリセット] ボタンを使用します。
