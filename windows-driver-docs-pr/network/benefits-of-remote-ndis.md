---
title: リモート NDIS の利点
description: リモート NDIS の利点
ms.assetid: ca559f2e-c7e3-4b8e-a04d-f3a544d33a68
keywords:
- リモートの NDIS WDK のネットワーク接続の利点があります。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 101186eaf0d6017731111d74fd02a6358f01b675
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63367691"
---
# <a name="benefits-of-remote-ndis"></a>リモート NDIS の利点





リモートの NDIS は、十分に理解して、実績のある NDIS アーキテクチャの拡張です。 NDIS は、NDIS ミニポート ドライバーのデバイスに固有の関数呼び出しのインターフェイスを定義します。 このインターフェイスは、ネットワークのデータを送受信するクエリを実行し、構成パラメーターと統計情報を設定してプリミティブを定義します。 リモートの NDIS は、そのため、NDIS 処理コードをミニポート ドライバーから、デバイス自体に移動、NDIS ミニポート ドライバー インターフェイスのメッセージの折り返しを定義することで NDIS を活用します。 これと他の方法のリモート NDIS により、デバイスの機能とパフォーマンス レベルのさまざまな種類。 リモートの NDIS モデルでは、多くの利点があります。

-   バスに固有のメッセージのトランスポート メカニズムを変更しなくても機能拡張

-   短時間で複数のバス経由で複数のプロトコルをサポートする機能

-   ネットワークと外部の両方のバス デバイス モデルの実証されているドライバーのアーキテクチャ

NDIS リモート デバイスでは、NDIS ネットワーク スタックに既に存在する付加価値の高いメカニズムはサポートされます。

 

 





