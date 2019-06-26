---
title: MB ラジオ電源状態操作
description: MB ラジオ電源状態操作
ms.assetid: 9b745ff3-c00b-4a43-9bf3-52f9bf61e062
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: aad2618143ccf6d88ab957f66e82ce46fce813a6
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67374034"
---
# <a name="mb-radio-power-state-operations"></a>MB ラジオ電源状態操作


このトピックでは、設定し、MB デバイスの無線電源状態の読み取りに使用する操作について説明します。 次の値を WWAN\_ラジオ列挙 MB サービスによってサポートされている 2 つの電源状態を説明します。

-   *WwanRadioOn*: オプションは、スタックが読み込まれ、デバイスを携帯電話の手順を実行できるだけでなく、ホストのコマンドを答えることができます。

-   *WwanRadioOff*: オプションは無効になります。 この状態で、デバイスの電源が入ってし、コマンドに応答する必要があります。 ただしラジオ関連の操作の実行しないオプションを有効にするホストのコマンドを除く。

電源状態のオプションには、(ある場合) MB サービス、またはハードウェアのスイッチのいずれかが制御されます。

理由は次ポータブル コンピューター (ラップトップ) の電源状態のオプションを変更可能性があることに注意します。

-   最もポータブル コンピューターには、オプションを有効または無効にするために使用できるスイッチは装備されています。 実質的に、ボタンをオフは、コンピューターのバック プレーンから MB モジュールの電源を切り取ります。 最終的には、無線は完全に電源がオフです。

-   MB サービスは電源を節約するために、または、環境でのラジオ干渉を避けるためには、低電力状態に無線ミニポート ドライバーにコマンドを送信することがあります (など、飛行機に)。

ラジオ電源の状態の操作の詳細については、次を参照してください。 [OID\_WWAN\_ラジオ\_状態](https://docs.microsoft.com/windows-hardware/drivers/network/oid-wwan-radio-state)します。

 

 





