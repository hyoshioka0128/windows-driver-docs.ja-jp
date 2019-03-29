---
title: USB デバイスでコンテナー ID をサポートするためのベスト プラクティス
description: USB デバイスでコンテナー ID をサポートするためのベスト プラクティス
ms.assetid: 58086d52-196f-4ea3-9ce6-62d3fcb43f9e
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: e971f39e21b655de026db86486e14f17838a6aa9
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56573893"
---
# <a name="best-practices-for-supporting-container-ids-on-usb-devices"></a>USB デバイスでコンテナー ID をサポートするためのベスト プラクティス


USB デバイス ノードのコンテナー ID の生成に使用されるヒューリスティック (*devnode*) で説明したこの[方法の USB デバイスが割り当てられたコンテナー Id](how-usb-devices-are-assigned-container-ids.md)は複雑でありから取得した情報に依存しています複数のソース。

Windows 7 以降のオペレーティング システムのデバイスのコンテナーを誤って判断して、デバイスの最適なユーザー エクスペリエンスを提供できるようにするこのセクションで説明されている推奨事項に従ってください。

このセクションには、これらの推奨事項を説明する次のトピックが含まれています。

[Microsoft OS ContainerID 記述子を使用してください。](using-microsoft-os-containerid-descriptors.md)

[デバイス コンテナーのグループ化のため USB リムーバブル機能を使用します。](using-the-usb-removable-capability-for-device-container-grouping.md)

[デバイス コンテナーの競合を避ける](avoiding-device-container-conflicts.md)

 

 





