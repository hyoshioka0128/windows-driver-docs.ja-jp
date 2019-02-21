---
title: オプションのフィルター ドライバー サービスを構成します。
description: オプションのフィルター ドライバー サービスを構成します。
ms.assetid: 698e1b2a-de1a-435a-bc30-0d27d9e15e19
keywords:
- フィルター ドライバー WDK ネットワー キング、サービス
- NDIS フィルター ドライバー WDK、サービス
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 843e20db3aa8ee01a3ba6105754273993fcb131c
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56539121"
---
# <a name="configuring-optional-filter-driver-services"></a>オプションのフィルター ドライバー サービスを構成します。





NDIS フィルター ドライバーを呼び出す[ *FilterSetOptions* ](https://msdn.microsoft.com/library/windows/hardware/ff549972)オプションのフィルター ドライバー サービスを構成する関数。 NDIS 呼び出し*FilterSetOptions*フィルター ドライバーの呼び出しのコンテキスト内で、 [ **NdisFRegisterFilterDriver** ](https://msdn.microsoft.com/library/windows/hardware/ff562608)関数

*FilterSetOptions*の既定のエントリ ポイントを登録します。 省略可能な*FilterXxx*関数をオプションのサービスに必要なその他のドライバー リソースを割り当てることができます。 省略可能なサービスをフィルター ドライバーの呼び出しを登録する、 [ **NdisSetOptionalHandlers** ](https://msdn.microsoft.com/library/windows/hardware/ff564550)関数をある特性構造体を渡します、 *OptionalHandlers*パラメーター。

現在の Windows バージョンでは、オプションのフィルター ドライバーのサービスはありません。

フィルター ドライバーを呼び出すことも**NdisSetOptionalHandlers** 、いくつか設定する*FilterXxx*関数の特定のフィルター モジュールのエントリ ポイント。 詳細については、次を参照してください。[データ バイパス モード](data-bypass-mode.md)します。

フィルター ドライバーを呼び出す場合**NdisSetOptionalHandlers**から*FilterRestart*構成の変更では、NDIS を再起動するフィルター モジュールのみに影響します。 その他のフィルター モジュールの構成が影響を受けません。

 

 





