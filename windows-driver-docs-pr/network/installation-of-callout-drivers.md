---
title: コールアウト ドライバーのインストール
description: コールアウト ドライバーのインストール
ms.assetid: 3baefd81-04bc-4a34-b4cd-afa544308a90
keywords:
- Windows Filtering Platform コールアウト ドライバー WDK をインストールします。
- コールアウト ドライバー WDK Windows フィルタ リング プラットフォームをインストールします。
- コールアウト ドライバー WDK Windows フィルタ リング プラットフォームをインストールします。
- WDK Windows フィルタ リング プラットフォーム ドライバーの読み込み
- INF ファイル WDK Windows フィルタ リング プラットフォーム
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 12200ae5547499daf0dfc284ccf50df25da619b2
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63324928"
---
# <a name="installation-of-callout-drivers"></a>コールアウト ドライバーのインストール


コールアウト ドライバーをドライバーのセットアップ情報ファイル (INF) ファイルを右クリックしてインストールできます**インストール**からポップアップ メニューが表示されます。

コールアウト ドライバーが正常にインストールされると、読み込むことができます (開始済み)、コマンド プロンプトで次を入力しています。

```cpp
net start drivername
```

指定された値に応じて、 **StartType**内のエントリ、 \[ *drivername*します。サービス\]、コールアウト ドライバーの INF ファイルのセクションで読み込まれることが自動的に、次回のシステムを再起動します。 コールアウト ドライバーでは、0 を指定する必要があります、通常は (サービス\_ブート\_開始) この値のドライバーが読み込まれ、吹き出しが前に登録されているように、フィルター エンジンが起動します。 参照してください、 [ **INF AddService ディレクティブ**](https://msdn.microsoft.com/library/windows/hardware/ff546326)詳細についてはします。

現在読み込まれているコールアウト ドライバーをアンロードできるコマンド プロンプトで次を入力して (停止)。

```cpp
net stop drivername
```

コールアウト ドライバーをすることもできますインストールされている、ロード (起動)、アンロード (停止) や、サービス コントロール マネージャーの Win32 API を呼び出すユーザー モード アプリケーションを記述することでアンインストールします。 Win32 サービスの詳細については、制御など、関数、 **CreateService**、 **OpenService**、 **StartService**、 **controlserviceによる認証**、および**DeleteService**を参照してください、 [Microsoft Windows SDK](https://go.microsoft.com/fwlink/p/?linkid=122165)します。

> [!NOTE]
> 以降では、Windows 8 以降、コールアウト ドライバーできません表示したりするプラグ アンド プレイ (PnP) マネージャーが不要になった (レガシ) デバイスの非 PnP デバイスの表現を作成するため、デバイス マネージャーを管理します。
