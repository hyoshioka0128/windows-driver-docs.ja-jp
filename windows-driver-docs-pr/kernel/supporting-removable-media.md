---
title: リムーバブル メディアのサポート
description: リムーバブル メディアのサポート
ms.assetid: f70c404c-8a38-4f53-8681-6efb52b30656
keywords:
- リムーバブル メディアの WDK カーネル
- リムーバブル メディア デバイスについて、リムーバブル メディアの WDK カーネル
- Irp WDK カーネルでは、リムーバブル メディア
- カーネル モード ドライバー WDK、リムーバブル メディア
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: e45fd807106ac6f798386430d834798e5efccae7
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56573384"
---
# <a name="supporting-removable-media"></a>リムーバブル メディアのサポート





ファイル システムとリムーバブル メディア デバイス ドライバーは、正しいメディアがリムーバブル メディア デバイスでファイルを開くし、メディアにアクセスする操作中にマウントすること、適切なメディアを引き続きマウントされていることを確認する責任を共有します。 ファイル システムとリムーバブル メディア デバイス ドライバーの間に階層化された中間ドライバーでは、この責任も共有します。

リムーバブル メディア デバイスで動作するドライバーのためは、次の 1 つ以上の処理を実行できます。

[応答チェック - ファイル システムからの要求を確認するには](responding-to-check-verify-requests-from-the-file-system.md)

[変更の可能性があるメディアのファイル システムへの通知](notifying-the-file-system-of-possible-media-changes.md)

[デバイス オブジェクトのフラグをチェック](checking-flags-in-the-device-object.md)

[中間ドライバーに Irp のセットアップ](setting-up-irps-in-intermediate-drivers.md)

 

 




