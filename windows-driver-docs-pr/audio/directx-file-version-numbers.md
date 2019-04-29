---
title: DirectX ファイル バージョン番号
description: DirectX ファイル バージョン番号
ms.assetid: 60f840d2-384c-49be-bf05-c16613b4858c
keywords:
- DirectX ファイル バージョン番号の WDK オーディオ
- バージョン番号の WDK オーディオ
- オーディオのミニポート ドライバー WDK、バージョン番号
- ミニポート ドライバー WDK オーディオ、バージョン番号
- オーディオ ドライバー WDK、バージョン番号
- ドライバー バージョン番号の WDK オーディオ
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: b3172713d0d0435ec2d969e7f6cb3c704c09bccc
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63333766"
---
# <a name="directx-file-version-numbers"></a>DirectX ファイル バージョン番号


## <span id="directx_file_version_numbers"></span><span id="DIRECTX_FILE_VERSION_NUMBERS"></span>


Vxd DirectX をサポートするには、ドライバーのバージョン番号、およびドライバーの機能の DirectX のセットアップ要件を満たす必要があります。 DirectX 8.0 プログラマのリファレンスを参照してください。 WDM または Windows NT 4.0 のドライバーには、これらの要件は適用されません。

ドライバーのバージョン番号を確認するのにには、次の手順を使用します。

-   デバイス ドライバーをインストールするのにには、DX でサポートされているゲームに付属するセットアップ アプリケーションを使用します。 ドライバーのインストール パッケージのすべての .dll、.drv、.vxd、および .exe ファイルを含むすべてのインストールされているファイルのバージョン番号を記録します。

-   すべての内部バージョン番号は、外部 (文字列) に対応していることを確認します。 バージョン番号、および数値のバージョン番号付け規則に従うこと (を参照してください[オーディオ ドライバーのバージョン番号](version-numbers-for-audio-drivers.md))。

-   Windows エクスプ ローラーを使用すると、ファイルを含むディレクトリを表示します。 各ファイルを右クリックし、をクリックして**プロパティ**著作権情報が正しいことを確認します。 具体的には、ベンダー名として、ドライバーに"Microsoft"が指定されていないことを確認します。

 

 




