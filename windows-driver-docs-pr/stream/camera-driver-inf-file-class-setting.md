---
title: カメラのドライバーのカメラ クラス INF ファイルの設定
description: ユニバーサル カメラ ドライバーの INF ファイルにカメラ クラスの設定を追加する方法について説明します。
ms.date: 01/30/2018
ms.localizationpriority: medium
ms.openlocfilehash: eb833199746b0367efef8dfa2edba9177859f303
ms.sourcegitcommit: 68bfa1f69229b7ac29d0e98f049734f5bc566a30
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/19/2019
ms.locfileid: "58187465"
---
# <a name="camera-class-inf-file-setting-for-universal-camera-drivers"></a>ユニバーサル カメラ ドライバーのカメラ クラス INF ファイルの設定

Windows 10 バージョン 1709 以降と、ユニバーサル カメラ ドライバーの INF ファイルに次のカメラ クラス設定を追加する必要があります。

次の追加**クラス**と**ClassGuid**エントリを**バージョン**ドライバーを確保するため、ユニバーサル カメラ ドライバーの INF ファイルのセクションが将来のカメラ ドライバー HLK テストに合格されます。

```INF
[Version]

...

Class=Camera
ClassGuid={ca3e7ab9-b4c3-4ae6-8251-579ef933890f}

...
```

カメラ クラス INF ファイルの設定の HLK 要件の詳細については、次を参照してください**Device.Streaming.Camera.Base.AVStreamClassInterfaceAndWDM**のコンポーネントと周辺機器のドキュメントで、 [Windows。Windows 10 用のハードウェア互換性仕様](https://docs.microsoft.com/windows-hardware/design/compatibility/whcp-specifications-policies)します。
