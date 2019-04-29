---
title: 更新プログラムのインストール
description: Windows ドライバーをインストールする任意のツールを使用して、ファームウェアの更新プログラム パッケージをインストールできます。
ms.assetid: 51C50910-8AA3-4ED9-B469-2325BBD2FB31
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5e0f2d08f0cfbd59d55a01c2f925eedaffc3e4e9
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63337537"
---
# <a name="installing-the-update"></a>更新プログラムのインストール


Windows ドライバーをインストールする任意のツールを使用して、ファームウェアの更新プログラム パッケージをインストールできます。 インストール プロセスでは、既知のシステム ディレクトリにファームウェアの更新プログラムのペイロード (firmware.bin) をコピーし、新しい更新プログラムが利用可能なを Windows に通知するために必要なレジストリ キーを作成します。 インストールが完了すると、再起動が、実際のファームウェア更新プロセスをトリガーするために必要になります。

![ファームウェアの更新パッケージのインストール プロセス](images/updateinstallprocess.png)

[次へ] の起動中に、OS ローダーを ExitBootServices() が呼び出されると、前に、新しいファームウェアの更新プログラムのペイロードが使用可能なかどうかを判断するよく知られているレジストリ キーの場所を確認します。 新しい更新プログラムのペイロードを使用できる場合、OS ローダーは、ドライバー パッケージで提供されるセキュリティ カタログに対して firmware.bin のハッシュを検証します。 署名が有効で、その、firmware.bin は UEFI UpdateCapsule() サービスを使用して、プラットフォーム ファームウェアにオフ渡されます。

**重要な**  この時点では、プラットフォーム ファームウェアは、ファームウェアの更新を実行する責任を負うものです。

 

複数のファームウェア更新プログラム パッケージがインストールされている場合、OS ローダーは、使用可能な各更新プログラムのペイロードを持つ UpdateCapsule() を呼び出します。 各ファームウェア ペイロードは別の capsule、ESRT エントリを対象となるファームウェアの更新プログラム パッケージの GUID で識別される各。

EFI システム リソースのテーブルが現在のファームウェア バージョンを提供し、最後の更新の状態にしようとしました。 OS ローダーでは、この情報を使用して、更新プログラムが正常に適用するかどうかを評価します。 Windows で実行されているファームウェアの更新のアプリケーションで使用できるように、OS には、ファームウェアの状態情報を永続化されます。 最後に、OS ローダーは、ブート プロセスを続行します。

## <a name="related-topics"></a>関連トピック
[ファームウェアのドライバー パッケージを使用してシステムとデバイスのファームウェア更新プログラム](system-and-device-firmware-updates-via-a-firmware-driver-package.md)  
[ESRT テーブルの作成](populating-the-esrt-table.md)  
[異なる地理的領域のファームウェアをカスタマイズします。](customizing-firmware-for-different-geographic-regions.md)  
[ファームウェアの更新プログラム パッケージの作成](authoring-a-firmware-update-package.md)  
[認定と更新プログラム パッケージの署名](certifying-and-signing-the-update-package.md)  

