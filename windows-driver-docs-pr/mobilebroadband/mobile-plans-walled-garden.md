---
title: モバイルプラン walled 庭園
description: モバイルプラン walled 庭園
ms.assetid: fb1566c6-8d47-4aa9-93f4-415ef7070ac6
keywords:
- Windows Mobile プランのモバイルオペレーター walled 庭園
ms.author: windowsdriverdev
ms.date: 07/31/2019
ms.topic: article
ms.prod: windows-hardware
ms.technology: windows-devices
ms.openlocfilehash: 8ca5f96d50d318bf31cfc935ed778b515ff969fa
ms.sourcegitcommit: f89a978ee23b9d2f925b13ea56b2c6cd48b4603a
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/10/2019
ms.locfileid: "68948133"
---
# <a name="mobile-plans-walled-garden"></a>モバイルプラン walled 庭園

Mobile plan *Walled ガーデン*は、データが不足している場合に顧客をサポートするための鍵となります。 Wi-fi などの代替インターネット接続がない場合でも、これらのユーザーは MO ダイレクトポータルに接続できます。 これにより、コンシューマーは追加のデータプランを購入し、サブスクリプションを管理できます。

> [!NOTE]
> モバイルプランのアーキテクチャでは、Walled 庭園エンドポイントの IP 範囲はサポートされていません。 ホスト名は、ホワイトリストに登録するために使用する必要があります。

MO Direct web ポータルと`GetBalance` API エンドポイントも、この Walled 庭園に含まれている必要があります。

## <a name="walled-garden-endpoints"></a>Walled 庭園エンドポイント

エンドユーザーが常にアクセスできる必須エンドポイントはごく少数です。 次の表は、Walled 庭園に必要なエンドポイントを定義しています。

| URL | HTTP/HTTPS |
| --- | --- |
| データマート. windows<span></span>.com | https |
| 社内リリース. データマート<span></span> | https |
| windows. policies<span></span>.net | https |
| ctldl. ある windowsupdate.log<span></span> | http |
| cdp1、<span></span>.com | http |
| omniroot<span></span> | http |
| vassg142. omniroot<span></span> | http |
| vassg142. omniroot<span></span> | http |
| <span></span>mscrl | http |
| crl. microsoft<span></span>.com | http |
| msftconnecttest<span></span> | http |
| crl3 digicert<span></span> | http |
| Digicert<span></span> | http |
| ログインします<span></span>。 | http + https |
| storagetos. データマート<span></span> | http + https |
| データマート. windows<span></span>.com | http + https |
| データマート. windows<span></span>. .com | http + https |
| ステージング. データマート<span></span> | http + https |
| データマート. windows<span></span>. .com | http + https |
