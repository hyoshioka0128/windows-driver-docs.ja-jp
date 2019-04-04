---
title: フラット ベッド スキャナーのアーキテクチャ
description: フラット ベッド スキャナーのアーキテクチャ
ms.assetid: 04f7df17-d289-44a1-8c2d-7d0fa618cc97
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 002946aa4e4678c1c190969697298dc7ce8053ba
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56532168"
---
# <a name="flatbed-scanner-architecture"></a>フラット ベッド スキャナーのアーキテクチャ





スキャナーのデバイスでは、フラット ベッドからプラテン上のスキャンをサポートする場合は、その WIA 項目ツリーで、ルート項目から直接、最初の子項目としてフラット ベッド スキャナーの項目が実装する必要があります。また、 [ **WIA\_IPA\_項目\_カテゴリ**](https://msdn.microsoft.com/library/windows/hardware/ff551581) WIA にプロパティを設定する必要があります\_カテゴリ\_ベッドします。 ベッドは、この項目は、プログラミング可能なデータ ソースを表し、データ転送はこの項目から要求されたときに、スキャナーのフラット ベッドからプラテン上に現在配置されているドキュメントからイメージを生成します。

フラット ベッドのプラテン スキャンのみをサポートするスキャナーには、次の図に示す WIA 項目のツリーがあります。

![プラテン専用のスキャンに関するフラット ベッド スキャナーを示す図](images/art-flatbed1.png)

WIA ベッド項目がルート項目から直接配置されていることに注意してください。

フラット ベッドからプラテン上のスキャンとドキュメント フィーダー付きのスキャンをサポートするスキャナーには、次の図に示す WIA 項目のツリーがあります。

![自動ドキュメント フィーダーのフラット ベッド スキャナーを示す図](images/art-flatbed2.png)

WIA 項目のツリーの最初のルート項目は、他のスキャン データ ソースが実装されている場合、WIA ベッド項目にすることがあります。 この配置では、Microsoft Windows XP および Windows Me のアプリケーションをサポートするやすくなります。 これらのオペレーティング システムとの互換性の詳細については、[WIA フラット ベッド スキャナーの互換性の Windows と Windows XP](wia-flatbed-scanner-compatibility-for-windows-xp-and-windows-me.md)を参照してください。

 

 




