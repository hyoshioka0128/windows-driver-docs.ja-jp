---
ms.assetid: 3D0CB4E7-D1BC-44AA-93D9-5CCDE98C9691
title: ドライバー プロジェクトのドライバー モデル設定プロパティ
description: WDF ライブラリのバージョン、プリプロセッサ定義など、カーネル モード ドライバーまたはユーザー モード ドライバーの基本的なプロパティを設定します。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 544dc763cc9dde3335928125f4d1850e90ceda17
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56518589"
---
# <a name="driver-model-settings-properties-for-driver-projects"></a>ドライバー プロジェクトのドライバー モデル設定プロパティ

WDF ライブラリのバージョン、プリプロセッサ定義など、カーネル モード ドライバーまたはユーザー モード ドライバーの基本的なプロパティを設定します。

## <a name="setting-driver-model-properties-for-driver-projects"></a>ドライバー プロジェクトのドライバー モデル プロパティの設定


1.  ドライバー プロジェクトのプロパティ ページを開きます。 **ソリューション エクスプローラー**でドライバー プロジェクトを右クリックして、**[プロパティ]** をクリックします。
2.  ドライバー プロジェクトのプロパティ ページで、**[構成プロパティ]** をクリックし、**[Driver Model Settings]** (ドライバー モデル設定) をクリックします。
3.  プロジェクトのプロパティを設定します。

**Type of driver (ドライバーの種類)**  
ドライバーの **[構成の種類]** が **[ドライバー]** である場合は、ドライバーの種類。 このオプションは、プロジェクトが **WindowsKernelModeDriver8.0** ツールセットを使っている場合にだけ利用できます。

設定可能な値は、次のとおりです。

* **[WDM]** (NDIS、StorPort など、すべてのミニポート/ポート ドライバーを含む)。
* **[KMDF]** KMDF ドライバー。
* **[Export driver (WDM) (エクスポート ドライバー (WDM))]** (エクスポート ドライバー (WDM)) 他のドライバーが呼び出せる関数をエクスポートする WDM ドライバー。 詳しくは、「[エクスポート ドライバーの作成](https://msdn.microsoft.com/Library/Windows/Hardware/Ff542891)」をご覧ください。

**KMDF Version Major (KMDF バージョン メジャー)**  
ドライバーの種類が KMDF である場合、このオプションはドライバーのコンパイル時に使われる KMDF のメジャー バージョンを指定します。

KMDF\_VERSION\_MAJOR エントリは、ドライバーを KMDF ライブラリにリンクするように MSBuild ユーティリティに指示します。

詳細については、「[フレームワーク ライブラリのバージョン](https://msdn.microsoft.com/Library/Windows/Hardware/Ff542842)」を参照してください。

**KMDF バージョン マイナー (ターゲット バージョン)** (Windows 10 バージョン 1803 以前では **KMDF バージョン マイナー**でした) ドライバーの種類が KMDF である場合、このオプションにより、ドライバーをコンパイルするときに使用される KMDF のマイナー バージョンが指定されます。

詳細については、「[フレームワーク ライブラリのバージョン](https://msdn.microsoft.com/Library/Windows/Hardware/Ff542842)」を参照してください。 **KMDF バージョン マイナー (ターゲット バージョン)** を指定しない場合、Visual Studio は次の既定値を使用します。
* Windows 10:1.15
* Windows 8/Windows 8.1: 1.11
* Windows 7: 1.9

**KMDF バージョン マイナー (最低要件)** (オプション、Windows 10 バージョン 1803 以降で利用可能) Windows 10 バージョン 1803 (Redstone 4) の KMDF バージョン 1.25 および UMDF バージョン 2.25 以降では、一続きのフレームワーク バージョンをターゲットとする KMDF ドライバーをビルドできます。 このオプションの設定を使用して、この範囲の最小 KMDF バージョンを指定します。

詳細については、「[複数のバージョンの Windows の WDF ドライバーをビルドする](../wdf/building-a-wdf-driver-for-multiple-versions-of-windows.md)」を参照してください。

**UMDF Version Major (UMDF バージョン メジャー)**  
UMDF ドライバーの場合、このオプションはドライバーのコンパイル時に使われる UMDF のメジャー バージョンを指定します。 「[UMDF バージョン履歴](https://msdn.microsoft.com/Library/Windows/Hardware/Ff561356)」をご覧ください。 UMDF ドライバーの場合、**[構成の種類]** は **[ダイナミック ライブラリ (.dll)]** です。

**UMDF バージョン マイナー (ターゲット バージョン)** (Windows 10 バージョン 1803 以前では **UMDF バージョン マイナー**でした) UMDF ドライバーがある場合、このオプションにより、ドライバーをコンパイルするときに使用される UMDF のマイナー バージョンが指定されます。 **UMDF バージョン マイナー (ターゲット バージョン)** を指定しない場合、Visual Studio は次の既定値を使用します。

メジャー バージョン = 2 の場合
* Windows 10:2.15
* その他: 2.0

メジャー バージョン = 1 の場合
* Windows 8 以降: 1.11
* Windows 7: 1.9

**UMDF バージョン マイナー (最低要件)** (オプション、Windows 10 バージョン 1803 以降で利用可能)

Windows 10 バージョン 1803 (Redstone 4) の KMDF バージョン 1.25 および UMDF バージョン 2.25 以降では、一続きのフレームワーク バージョンをターゲットとする UMDF ドライバーをビルドできます。 このオプションの設定を使用して、この範囲の最小 UMDF バージョンを指定します。

詳細については、「[複数のバージョンの Windows の WDF ドライバーをビルドする](../wdf/building-a-wdf-driver-for-multiple-versions-of-windows.md)」を参照してください。

**Allow Date, Time, and Timestamp (日付、時刻、タイムスタンプを許可する)**  
\_\_DATE\_\_、\_\_TIME\_\_、\_\_TIMESTAMP\_\_ に対する標準の C/CPP マクロを定義します。

**Override Target Configuration Preprocessor Definitions (ターゲット構成プリプロセッサ定義を上書きする)**  
次の前処理シンボルに対する既定値を上書きします: ソース ファイルの \_WIN32\_WINNT、WINVER、WINNT、NTDDI\_VERSION。 既定値は現在のターゲット構成によって制御されます。

## <a name="related-topics"></a>関連トピック


* [フレームワーク ライブラリのバージョン](https://msdn.microsoft.com/Library/Windows/Hardware/Ff542842)
* [フレームワーク ベースのドライバーのビルドと読み込み](https://msdn.microsoft.com/Library/Windows/Hardware/Ff540730)
* [UMDF バージョン履歴](https://msdn.microsoft.com/Library/Windows/Hardware/Ff561356)
* [UMDF ドライバーのビルド](https://msdn.microsoft.com/Library/Windows/Hardware/Ff540730)
* [エクスポート ドライバーの作成](https://msdn.microsoft.com/Library/Windows/Hardware/Ff542891)
 

 






