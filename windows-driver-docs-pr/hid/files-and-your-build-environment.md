---
title: ファイルと、ビルド環境
description: ファイルと、ビルド環境
ms.assetid: 0c85a599-65bb-45e5-a2f8-eefd47e82025
keywords:
- プロパティ シートの WDK DirectInput、ファイル
- ゲーム コント ローラー WDK DirectInput、ファイル
- コントロール パネルの WDK DirectInput、ファイル
- プロパティ シート WDK DirectInput、環境を構築します。
- ゲーム コント ローラー WDK DirectInput、環境を構築
- コントロール パネルの WDK DirectInput、ビルド環境
- WDK DirectInput 環境を構築します。
- WDK DirectInput ファイル
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 5bcc177b9c3c78c2b0ff62f17445c0e4151baa0a
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56580642"
---
# <a name="files-and-your-build-environment"></a>ファイルと、ビルド環境





少なくとも、直接 X 直接 Development Kit (DDK) ヘッダー ファイル Dicpl.h 必要になります。 このファイルには、必要なインターフェイス、構造体、クラス定義、およびエラーを提供します。 DirectInput を使用することをお勧め**IDirectInputJoyConfig8**プロパティ シートを確認するために、すべてのレジストリ アクセス用のインターフェイスは Windows NT 4.0 以降でも機能します。 DirectInput をプロパティ ページで使用する場合は、関連付けられている DirectX SDK ファイルも使用する必要があります。 DirectInput コントロール パネルの すべての構造は、8 バイト境界にパックされます。 プロパティ シートを 8 バイト境界で構造体にパックすることを確認します。

**注**  コントロール パネルをテストするにはときがプライマリ ディスプレイが 640 x 480 ピクセルの解像度に設定されているシステムでテストしてください。 すべてのコントロールがまだこの低解像度で表示されていることを確認します。

 

 

 




