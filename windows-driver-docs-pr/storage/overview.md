---
title: 記憶域サイロのドライバーについて
description: 記憶域サイロのドライバーについて
ms.assetid: e150228e-820f-49ac-bc3f-644e77f3d544
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: eae47543610473920c9deb799ef6a34e28089a7e
ms.sourcegitcommit: e1ff1dd43b87dfb7349cebf70ed2878dc8d7c794
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/02/2020
ms.locfileid: "75606522"
---
# <a name="about-storage-silo-drivers"></a>記憶域サイロのドライバーについて

ここでは、記憶域サイロドライバーシステムコンポーネントの基礎となる設計とアーキテクチャについて説明します。これにより、次の一連のイベントが有効になります。

1. ユーザーは、IEEE 1667 準拠の記憶装置をシステムに接続します。

2. デバイスが認識されます。 適切なドライバー、システムコンポーネント、サードパーティのコンポーネントがインストールされ、構成されている。

3. Windows シェルとインストールされているサードパーティ製のアプリケーションは、IEEE 1667 仕様に従って、デバイスの検出、アクセス、管理、および対話を行うことができます。
