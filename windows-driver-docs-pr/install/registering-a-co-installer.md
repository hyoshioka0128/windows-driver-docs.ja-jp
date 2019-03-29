---
title: 共同インストーラーの登録
description: 共同インストーラーの登録
ms.assetid: a585bb06-d65f-4e14-a205-dc0d6523363e
keywords:
- 共同インストーラー WDK デバイスのインストール、登録します。
- co-installer を登録します。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: f8df7332e52584a50df06f6ac54f62503d366b3c
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56574033"
---
# <a name="registering-a-co-installer"></a>共同インストーラーの登録





共同インストーラーは、単一のデバイス、または特定のセットアップ クラスのすべてのデバイスを登録できます。 デバイスに固有の共同インストーラーは、そのデバイスのいずれかがインストールされているときに INF ファイルを動的に登録されます。 クラスの共同インストーラーは、手動でまたはによってカスタム デバイスのインストール アプリケーションと、INF 登録されます。

詳しくは、

[デバイスに固有の共同インストーラーを登録します。](registering-a-device-specific-co-installer.md)

[クラスの共同インストーラーを登録します。](registering-a-class-co-installer.md)

共同インストーラーを更新するには、DLL 通常使用しているため、ユーザーがデバイスのプロパティ ページで、ドライバーの更新ボタンをクリックすると、新しい各バージョンの DLL で新しいファイル名が必要です。

 

 





