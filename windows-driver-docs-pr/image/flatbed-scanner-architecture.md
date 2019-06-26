---
title: フラットベッド スキャナーのアーキテクチャ
description: フラットベッド スキャナーのアーキテクチャ
ms.assetid: 04f7df17-d289-44a1-8c2d-7d0fa618cc97
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6ab8f111acdbcd44ef0e7472adf3df40d41ddd47
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67380036"
---
# <a name="flatbed-scanner-architecture"></a>フラットベッド スキャナーのアーキテクチャ





スキャナーのデバイスでは、フラット ベッドからプラテン上のスキャンをサポートする場合は、その WIA 項目ツリーで、ルート項目から直接、最初の子項目としてフラット ベッド スキャナーの項目が実装する必要があります。また、 [ **WIA\_IPA\_項目\_カテゴリ**](https://docs.microsoft.com/windows-hardware/drivers/image/wia-ipa-item-category) WIA にプロパティを設定する必要があります\_カテゴリ\_ベッドします。 ベッドは、この項目は、プログラミング可能なデータ ソースを表し、データ転送はこの項目から要求されたときに、スキャナーのフラット ベッドからプラテン上に現在配置されているドキュメントからイメージを生成します。

フラット ベッドのプラテン スキャンのみをサポートするスキャナーには、次の図に示す WIA 項目のツリーがあります。

![プラテン専用のスキャンに関するフラット ベッド スキャナーを示す図](images/art-flatbed1.png)

WIA ベッド項目がルート項目から直接配置されていることに注意してください。

フラット ベッドからプラテン上のスキャンとドキュメント フィーダー付きのスキャンをサポートするスキャナーには、次の図に示す WIA 項目のツリーがあります。

![自動ドキュメント フィーダーのフラット ベッド スキャナーを示す図](images/art-flatbed2.png)

WIA 項目のツリーの最初のルート項目は、他のスキャン データ ソースが実装されている場合、WIA ベッド項目にすることがあります。 この配置では、Microsoft Windows XP および Windows Me のアプリケーションをサポートするやすくなります。 これらのオペレーティング システムとの互換性の詳細については、次を参照してください。 [WIA フラット ベッド スキャナーの互換性の Windows と Windows XP](wia-flatbed-scanner-compatibility-for-windows-xp-and-windows-me.md)します。

 

 




