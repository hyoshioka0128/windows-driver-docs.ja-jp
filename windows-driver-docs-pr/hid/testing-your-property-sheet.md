---
title: プロパティ シートのテスト
description: プロパティ シートのテスト
ms.assetid: 9886a758-392b-451d-874d-5ffcc5f9f5cd
keywords:
- プロパティ シートの WDK DirectInput のテスト
- ゲーム コント ローラー WDK DirectInput、プロパティ シートのテスト
- コントロール パネルの WDK DirectInput、プロパティ シートのテスト
- テストのプロパティ シートの WDK DirectInput
- コントロール パネル アプリケーション WDK DirectInput のデバッグ
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 3f8d4af0e5af9d0b1884d01277fcaf1980bec0e9
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56570962"
---
# <a name="testing-your-property-sheet"></a>プロパティ シートのテスト





プロパティ シート ページのテスト中に、DirectInput と DirectInput コントロール パネル の両方のデバッグ バージョンを実行することを強くお勧めします。 DirectX のコンポーネントは、デバッグ ウィンドウ/端末に便利なエラーと警告メッセージを発行するために設計されています。

コントロール パネル アプリケーションのデバッグは、注意が必要です。 次の手順を使用して、Microsoft Developer Studio 5.0 以降のカスタム プロパティ シート ページをデバッグする (他のコンパイラがある同様の動作)。

1.  **プロジェクト**メニューの **設定**します。

2.  選択、**デバッグ**タブ。

3.  デバッグ セッションで実行可能ファイル、c:」と入力します。\\WINDOWS\\RUNDLL32 します。実行可能ファイル (c: と仮定すると\\WINDOWS では、Windows 95/98/Me ディレクトリ) Windows 95/98/Me、または c: を実行している場合\\WINNT\\SYSTEM32\\RUNDLL32 します。実行可能ファイル (c: と仮定すると\\WINNT はオペレーティング システムのディレクトリ) 4.0 またはそれ以降は、Windows NT を実行している場合。

4.  プログラムの引数に対して入力**shell32.dll,Control\_RunDLL c:\\windows\\システム\\joy.cpl**します。 これでもう一度、c:\\WINDOWS では、Windows ディレクトリ。 小文字を区別し、正確に示すように入力する必要があります。

ブレークポイントを設定し、ビルド メニューから次のように選択します。 その後、**デバッグの開始**、し**移動**します。 カスタム プロパティ シート ページをデバッグする準備が整いました。

 

 




